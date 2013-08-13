---
layout: post
title: "encrypt sqlite with sqlcipher"
date: 2013-08-13 18:05
comments: true
categories: 
---
##Get the sqlcipher SourceCode

```
git clone https://github.com/sqlcipher/sqlcipher.git
cd sqlcipher
```
##Complite the source code
动态链接的编译方法（Compiling with dynamic linking）[推荐]:

```
./configure --enable-tempstore=yes CFLAGS="-DSQLITE_HAS_CODEC" LDFLAGS="-lcrypto"
 make
 ln -s /Users/wanyc/sqlcipher/sqlite3 /usr/bin/sqlcipher 
```

静态库的编译方法: (replace /path/to with the path to libcrypto.a)

```
  ./configure --enable-tempstore=yes CFLAGS="-DSQLITE_HAS_CODEC" LDFLAGS="/path/to/libcrypto.a"
  make
```
  

##How to encrypt a sqlite(In Shell)

```
sqlcipher test.db
> PRAGMA key='test'; //必须在打开数据库第一步来执行
> select * from sqlite_master;

//创建一个新数据库
sqlcipher encrypted.db 
>PRAGMA key = '[YourPasswordHere]';
>SELECT * FROM SomeTableName;
```


##为现有数据加密


####1.先导出现有库的数据(In shell)
```
sqlcipher plaintext.db
.output dsa.sql
.dump
```
####将新的数据库导出，并加密，之后导入非加密的库里面的数据
```
sqlcipher another.db
PRAGMA key='aaa';
.read dsa.sql
```
####2.官方做法（推荐,In shell）
```
ATTACH DATABASE 'encrypted.db' as encrypted KEY 'SomePassword'; //encrypted.db是要导出的新的数据库
SELECT sqlcipher_export('encrypted');
DETACH DATABASE encrypted;
```
#####3.Object-c代码实现对一个非加密库导入到加密库的方法(已经验证)(Xcode)
```
NSString *documentPath = [NSSearchPathForDirectoriesInDomains(NSDocumentDirectory,NSUserDomainMask, YES) 
						objectAtIndex:0];
NSString *attachPath = [documentPath stringByAppendingPathComponent:@"new.db"];

if (sqlite3_open([path_u UTF8String], &convert_DB) == SQLITE_OK) {
NSString *sql = [NSString stringWithFormat:@"ATTACH DATABASE '%@' AS encrypted KEY '1234';",
				attachPath];
//执行Attach操作
  sqlite3_exec(convert_DB, [sql UTF8String] , NULL, NULL, NULL);
  
  // 导出数据库
  sqlite3_exec(convert_DB, "SELECT sqlcipher_export('encrypted');", NULL, NULL, NULL);
  
  // 执行分离
  sqlite3_exec(convert_DB, "DETACH DATABASE encrypted;", NULL, NULL, NULL);
  
  NSLog (@"End database copying at %@",[NSDate date]);
  sqlite3_close(convert_DB);
}
else {
    sqlite3_close(convert_DB);
    NSAssert1(NO, @"Failed to open database with message '%s'.", sqlite3_errmsg(convert_DB));
}
```

#### 为加密后的sqlite执行解密(其实步骤与加密一样，只要把key设置为空就实现了不加密)
```
ATTACH DATABASE 'encrypted.db' as encrypted KEY ''; //encrypted.db是要导出的新的数据库
SELECT sqlcipher_export('encrypted');
DETACH DATABASE encrypted;
```


##参考
* sqlcipher配置 [http://sqlcipher.net/ios-tutorial/](http://sqlcipher.net/ios-tutorial/)  
* sqlcipher API [http://sqlcipher.net/sqlcipher-api/](http://sqlcipher.net/sqlcipher-api/)
* sqlcipher 使用 [http://jordy.easymorse.com/?p=970](http://jordy.easymorse.com/?p=970)
* Mac SQLCipher导出工具 [https://github.com/welsonla/SQLCipherExport](https://github.com/welsonla/SQLCipherExport)
title: categories
date: 2015-10-10 21:25:08
type: "categories"
---
<script>
	var Hexo = require('hexo');
	var hexo = new Hexo(process.cwd(),{});
	hexo.init().then(function(){
		console.log(hexo.locals.get('posts'));
	});
</script>
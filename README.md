# vuecode-analyze
第一步：首先找到入口文件
1.1 vue/package.json

 "scripts": {
    "dev": "rollup -w -c scripts/config.js --environment TARGET:web-full-dev",
    }
    运行 node dev 执行的是scripts/config.js文件的内容  执行的是web-full-dev
    
    打开scripts/config.js 发现
    
    // Runtime+compiler development build (Browser)
  'web-full-dev': {
    entry: resolve('web/entry-runtime-with-compiler.js'),
    dest: resolve('dist/vue.js'),
    format: 'umd',
    env: 'development',
    alias: { he: './entity-decoder' },
    banner
  },
  
  发现入口在 web/entry-runtime-with-compiler.js  web是定义好了的别名 在vue/scripts/alias.js中定义 web: resolve('src/platforms/web'),
  打开web/entry-runtime-with-compiler.js
 
 首先是这么一句   
 // 把template如果cached中有，则从缓存中去，如果没有，就先缓存在返回
 const idToTemplate = cached(id => {
  const el = query(id)
  return el && el.innerHTML
})
    
    

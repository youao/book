# 起步

## 安装手脚架

```
npm install -g gitbook-cli
```

注意一定要全局安装 -g
亲测非全局安装跑不起来



# Bug

## if (cb) cb.apply(this, arguments)，cb.apply is not a function

找到文件 `C:\Users\Administrator\AppData\Roaming\npm\node_modules\gitbook-cli\node_modules\npm\node_modules\graceful-fs\polyfills.js`



报错位置

```javascript
function statFix (orig) {
  if (!orig) return orig
  // Older versions of Node erroneously returned signed integers for
  // uid + gid.
  return function (target, cb) {
    return orig.call(fs, target, function (er, stats) {
      if (!stats) return cb.apply(this, arguments)
      if (stats.uid < 0) stats.uid += 0x100000000
      if (stats.gid < 0) stats.gid += 0x100000000
      if (cb) cb.apply(this, arguments)
    })
  }
}
```

这个函数的作用是用来修复node.js的一些bug,但是我就为了学个gitbook,没必要难为我自己！

所以，我就找到这个函数的调用，注释即可

![注释代码](https://img-blog.csdnimg.cn/20200905015630899.png#pic_center)
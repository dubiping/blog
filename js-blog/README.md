## 跨域
- [cors跨域-阮一峰详解](http://www.ruanyifeng.com/blog/2016/04/cors.html)

## 前端监控
- [cqc-代码检查](https://github.com/xcatliu/cqc)

## 时间格式化 
- [时间格式化工具](https://github.com/dubiping/blog/blob/master/js-blog/Date.js)
- [仿微信时间格式化](https://blog.csdn.net/chy555chy/article/details/84325958)

## 禁止视频下载
- [禁止右键下载]
```javascript
  $('#video1').bind('contextmenu',function() { return false; });
```
- [禁止视频标签下载]
```javascript
  <style type="text/css">
      video::-internal-media-controls-download-button {
          display:none;
      }
      video::-webkit-media-controls-enclosure {
          overflow:hidden;
      }
      video::-webkit-media-controls-panel {
          width: calc(100% + 30px);
      }
  </style>
  <video controls controlsList="nodownload"></video>
```


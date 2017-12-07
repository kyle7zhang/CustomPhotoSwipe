## 简介

本库是[PhotoSwipe](https://github.com/dimsemenov/PhotoSwipe)的扩展版，主要扩展了如下的功能：
* (boolean) prependItems/appendItems(Array): 向列表前方添加item项，并会自动修复索引，返回添加是否成功。建议在`mainScrollAnimComplete`事件回调中调用，否则可能失败，失败后需要自行保存要添加的内容，并在下一个时机再添加。
* 增加Matrix模式，自动在Android 7版本下启用，提升流畅性。
* 允许缩放富文本HTML内容

## 参考

* [PhotoSwipe原版](https://github.com/dimsemenov/PhotoSwipe)
* [使用iPad QQ访问我们的iPad版动漫阅读器](http://dm.vip.qq.com/club/client/ipadComic/html/large-scale/comic/reader.html?_wv=1&_secondWebView=1&fromWeb=1&direct=1&platId=110&_nav_bgclr=0x000000&_nav_txtclr=0xFFFFFF&_nav_alpha=178&_nav_shade=1&_wv_bgclr=0x333333&id=531040&sectionId=3&type=3&_pwv=15)：或者模拟UA `Mozilla/5.0 (iPad; CPU OS 9_2_1 like Mac OS X) AppleWebKit/601.1.46 (KHTML, like Gecko) Mobile/13D15 IPadQQ/6.6.1.136 QQ/6.6.1.136` 访问

## 使用

* 页面上先引入`./css/default-skin.css`和`./css/photoswipe.css`
* 引入脚本`./js/CustomPhotoSwipe-4.1.1.js`
* 随后执行

```javascript

var pswpElement = document.querySelectorAll('.pswp')[0];

// build items array
var items = [
    {
        html: '<div style="background-image: url(https://placekitten.com/1200/900)"></div>',
        w: 1200,
        h: 900
    }
];

// define options (if needed)
var options = {
    // optionName: 'option value'
    // for example:
    enableMatrix: false,
    index: 0 // start at first slide
};

// Initializes and opens PhotoSwipe
var gallery = new PhotoSwipe(pswpElement, null, items, options);
gallery.init();

setTimeout(function () {
    var appendQueue = [];

    for (var i = 0; i < 5; i ++) {
        appendQueue.push({
            html: '<div style="background-image: url(https://placekitten.com/1200/900)"></div>',
            w: 1200,
            h: 900
        });
    }

    if (gallery) {
        // 动态添加时建议再`mainScrollAnimComplete`中添加，否则可能添加失败
        // gallery.listen('mainScrollAnimComplete', function () {
        // 	if (gallery) {
        // 		if (appendQueue.length > 0 && gallery.appendItems(appendQueue)) {
        // 			appendQueue = [];
        // 		}
        // 	}
        // });
        if (appendQueue.length > 0 && gallery.prependItems(appendQueue)) {
            appendQueue = [];
        }
    }
}, 3000);

```

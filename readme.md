## Introduction

This is an extension of [PhotoSwipe](https://github.com/dimsemenov/PhotoSwipe), new features added:
* (return boolean) prependItems/appendItems(Array): prepend/append/remove items and will keep current state of current slide. Can only be successful when `!_mainScrollAnimating`. When append/prepend/remove failed, please retry in your project. Recommend using this api in the `mainScrollAnimComplete` event callback.
* Add Matrix mode, automatically enable on android, improve scaling performance.
* Enable scaling rich text html.
* goToAnimated: animated flip page(-1/1).
* Some improvements in QQBrowser which embedded in android QQ or wechat.

## QQ Comic Reader: Flip mode

![](https://raw.githubusercontent.com/icese7en/CustomPhotoSwipe/master/assets/img/snapshot.png)

## References

* [PhotoSwipe Official](https://github.com/dimsemenov/PhotoSwipe)
* [Using iPad QQ to view our comic reader of iPad version](http://dm.vip.qq.com/club/client/ipadComic/html/large-scale/comic/reader.html?_wv=1&_secondWebView=1&fromWeb=1&direct=1&platId=110&_nav_bgclr=0x000000&_nav_txtclr=0xFFFFFF&_nav_alpha=178&_nav_shade=1&_wv_bgclr=0x333333&id=531040&sectionId=3&type=3&_pwv=15)：Or simulate User Agent `Mozilla/5.0 (iPad; CPU OS 9_2_1 like Mac OS X) AppleWebKit/601.1.46 (KHTML, like Gecko) Mobile/13D15 IPadQQ/6.6.1.136 QQ/6.6.1.136` to view our page

## Usage

* Link stylesheet `./css/default-skin.css` and `./css/photoswipe.css`
* Insert script `./js/CustomPhotoSwipe-4.1.1.js`
* Run page

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
        // Dynamic append/prepend/remove only can work during `mainScrollAnimComplete`
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

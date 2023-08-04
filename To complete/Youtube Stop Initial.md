
```JS
(function() {
    'use strict';

    // Function to block video autoplay and buffer
    function blockVideoAutoplayAndBuffer() {
        var observer = new MutationObserver(function(mutations) {
            mutations.forEach(function(mutation) {
                if (mutation.type === "childList") {
                    var videos = document.getElementsByTagName("video");
                    Array.from(videos).forEach(function(video) {                        
                        // Pause video playback
                        video.pause();
                        
                        // Save source URL to restore later
                        var src = video.src;
                        
                        // Remove source URL to prevent buffering
                        video.removeAttribute("src");
                        
                        // Add click event listener to start buffering once clicked
                        video.addEventListener("click", function() { 
                            if (!this.src && !this.srcObject) {  // Buffer only if src is empty and no srcObject exists
                                this.setAttribute("src", src);  // Restore saved source URL before loading

                                this.load();
                            }
                            
                            this.removeEventListener("click", arguments.callee);  // Remove click event listener after first play attempt
                        });
                    });
                }
            });
        });

        observer.observe(document.body, { childList: true, subtree: true });
    }

    // Wait for DOMContentLoaded event before blocking autoplay and buffer
    window.addEventListener('DOMContentLoaded', function() {
        blockVideoAutoplayAndBuffer();
        
        // Optional Styling - Uncomment below lines if needed
        document.body.style.overflow = 'hidden'; 
        document.documentElement.style.height = '100%';
    });
})();
```

What doesn't work:
- The video doesn't play after for some weird reason, even though we reapply the src we removed

---
I'm currently scraping through a plugin and copying the code
This is the injection order
`"js": [

      "data/page.js",
      "data/controls.js",
      "data/no_buffer.js",
      "data/quality.js",
    ],`

This works
```JS
document.documentElement.appendChild(Object.assign(document.createElement('script'), {

textContent: `

var yttools = yttools || [];

  

function onYouTubePlayerReady(e) {

yttools.forEach(c => {

try {

c(e);

} catch (e) {}

});

}

  

{

const observe = (object, property, callback) => {

let value;

const descriptor = Object.getOwnPropertyDescriptor(object, property);

Object.defineProperty(object, property, {

enumerable: true,

configurable: true,

get: () => value,

set: v => {

callback(v);

if (descriptor && descriptor.set) {

descriptor.set(v);

}

value = v;

return value;

}

});

};

  

observe(window, 'ytplayer', ytplayer => {

observe(ytplayer, 'config', config => {

if (config && config.args) {

config.args.jsapicallback = 'onYouTubePlayerReady';

}

});

});

  

yttools.push(e => {

// Method 0

e.stopVideo();

  

// Method 1; prevent polymer from starting video

const playVideo = e.playVideo;

e.playVideo = function() {

const err = new Error().stack;

if (err && err.indexOf('onPlayerReady_') !== -1) {

return e.stopVideo();

}

playVideo.apply(this, arguments);

};

  

// Method 2; stop subsequent plays

document.addEventListener('yt-page-data-fetched', () => e.stopVideo && e.stopVideo());

});

}

`

}));
```

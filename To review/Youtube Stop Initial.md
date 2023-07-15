
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


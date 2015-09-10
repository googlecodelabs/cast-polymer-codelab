Copyright 2014 Google Inc. All Rights Reserved.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

#cast-player-bar-polymer
In the [CastVideos-chrome-material](https://github.com/googlecast/CastVideos-chrome-material) sample, this 
element represents the local video player bar.  It controls local and cast media depending on state.  It does this by observing changes in `localMedia` and `castMedia`.

This element also includes the `cast-button` to start casting.

You can use this player bar with your own video element to easily manage playback/casting.

#Setup
Use [Bower](http://bower.io/) to include the cast-player-bar in your web app.  The following 
command will add the cast-player-bar and it's dependencies to your project.

    bower install --save googlecast/cast-player-bar-polymer

#Integration
The easiest way to integrate is to use the cast-video-polymer element which already integrates the player bar.  The instructions below cover a custom integration.  You'll first need to include [Polymer](https://www.polymer-project.org/0.5/docs/start/getting-the-code.html).

##Including the element
In your html include the element

    <link rel="import"
        href="bower_components/cast-player-bar-polymer/cast-player-bar-polymer.html">

Add the element to your HTML and pass in the `appId`.

    <cast-player-bar appId="{{ appId }}"></cast-player-bar>

In the polymer ready event pass in the castManager object.

    var playerBar = document.querySelector('cast-player-bar');
    playerBar.castManager = castManager;

##Handle playback events
In your player, subscribe to [`core-signals`](https://github.com/Polymer/core-signals) using the polymer element or through attaching an event listener to the DOM.

    <core-signals on-core-signal-media-action="{{ mediaActionHandler }}"></core-signals>
    
Handle the core signal events:

    mediaActionHandler: function(e, data, sender) {
      if (castManager.isCasting) {
        switch (data.action) {
          case 'seek':
            //Your seek code
            break;
          case
          'play':
            //Your play code
            this.castManager.localMedia.state = cast.Media.STATE.PLAY;
            break;
          case
          'pause':
            //Your pause code
            this.castManager.localMedia.state = cast.Media.STATE.PAUSE;
            break;
          case 'volume':
            //Your volume code
            break;
          case 'fullscreen':
            var elem = //[Your element to fullscreend];
            if (elem.requestFullscreen) {
              elem.requestFullscreen();
            } else if (elem.msRequestFullscreen) {
              elem.msRequestFullscreen();
            } else if (elem.mozRequestFullScreen) {
              elem.mozRequestFullScreen();
            } else if (elem.webkitRequestFullscreen) {
              elem.webkitRequestFullscreen();
            }
            this.castManager.isFullScreen = true;
            break;
          case 'exitFullscreen':
            if (document.exitFullscreen) {
              document.exitFullscreen();
            } else if (document.msExitFullscreen) {
              document.msExitFullscreen();
            } else if (document.mozCancelFullScreen) {
              document.mozCancelFullScreen();
            } else if (document.webkitExitFullscreen) {
              document.webkitExitFullscreen();
            }
            this.castManager.isFullScreen = false;
            break;
        }
      }
    }
    
##Update localMedia currentTime
When the video is playing you'll need to update the localMedia currentTime to update the player bar slider and time remaining.

    window.setInterval(function() {castManager.localMedia.setCurrentTime(currentTime);}, 1000);

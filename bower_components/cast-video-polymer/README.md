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

#cast-video-polymer
This element represents the video player in the [CastVideos-chrome-material](https://github.com/googlecast/CastVideos-chrome-material) sample.

[Demo](http://googlecast.github.io/cast-video-polymer/demo.html)

It observes `castManager.localMedia` and automatically loads any HTML5 video that's set as 
localMedia.

It encapsulates the [cast-player-bar](https://github.com/googlecast/cast-player-bar-polymer) element to handle controlling local media and casting.

#Setup
Use [Bower](http://bower.io/) to include the cast-video in your web app.

    bower install --save googlecast/cast-volume-controller-polymer
    
#Integration
You'll first need to include [Polymer](https://www.polymer-project.org/0.5/docs/start/getting-the-code.html).

##Including the element
In your html include the element.

    <link rel="import"
            href="bower_components/cast-volume-controller-polymer/cast-volume-controller-polymer.html">

Add the element to your HTML defining the `appId`.

    <cast-video appId="{{ appId }}"></cast-video>

##Loading media
Currently the video player only supports HTML5 video content.
 
To load media, first create a media object.

    var media = {
      "title": "Big Buck Bunny",
      "description": "Fusce id nisi turpis. Praesent viverra bibendum semper. Donec tristique, orci sed semper lacinia, quam erat rhoncus massa, non congue tellus est quis tellus. Sed mollis orci venenatis quam scelerisque accumsan. Curabitur a massa sit amet mi accumsan mollis sed et magna. Vivamus sed aliquam risus. Nulla eget dolor in elit facilisis mattis. Ut aliquet luctus lacus. Phasellus nec commodo erat. Praesent tempus id lectus ac scelerisque. Maecenas pretium cursus lectus id volutpat.",
      "url": "https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/BigBuckBunny.mp4",
      "studio": "Blender Foundation",
      "thumbnailImageUrl": "//commondatastorage.googleapis.com/gtv-videos-bucket/sample/images_480x270/BigBuckBunny.jpg",
      "largeImageUrl": "//commondatastorage.googleapis.com/gtv-videos-bucket/sample/images_780x1200/BigBuckBunny-780x1200.jpg"
    };

Create a `cast.Media` object.
    
    var castMedia = new cast.Media(media);

##Instiantiate a `CastMedia` object in the polymer ready event.
In the polymer ready event, create the castManager object and pass it to the video element.

    window.addEventListener('polymer-ready', function() {
      var video = document.querySelector('cast-video'); 
      video.castManager = new cast.CastManager(castMedia);
    }

##Loading new media
To set the video, call the `setLocalMedia` method of castManager.  The video element will 
automatically detect the change and update the video content.

    castManager.setLocalMedia(new cast.Media(media));

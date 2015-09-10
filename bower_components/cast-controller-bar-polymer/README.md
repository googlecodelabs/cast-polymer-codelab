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

#cast-controller-bar
In the [CastVideos-chrome-material](https://github.com/googlecast/CastVideos-chrome-material) sample, this element represents the cast controller bar that appears when a user navigates away from the currently casting video.  It automatically displays when it detects that localMedia doesn't match castingMedia.

It publishes a single property the castManager object.

The element will stay pinned to the bottom right of the browser window, but you can easily modify that with CSS.

#Setup
Use [Bower](http://bower.io/) to include the cast-controller-bar in your web app.  The following 
command will add the cast-controller-bar and it's dependencies to your project.

    bower install --save googlecast/cast-controller-bar-polymer
    
#Integration
You'll need to first include 
[Polymer](https://www.polymer-project.org/0.5/docs/start/getting-the-code.html).

##Including the element
In your html include the element.

    <link rel="import"
        href="bower_components/cast-controller-bar-polymer/cast-controller-bar-polymer.html">
        
Add the element to your HTML.

    <cast-controller-bar></cast-controller-bar>
    
In the polymer ready event pass in the castManager object.

    var controllerBar = document.querySelector('cast-controller-bar');
    controllerBar.castManager = castManager;

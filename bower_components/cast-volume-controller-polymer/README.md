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

#cast-volume-controller
This element represents the volume bars in the [CastVideos-chrome-material](https://github.com/googlecast/CastVideos-chrome-material) sample.  

It publishes 2 properties:

castManager - the castManager object
cast - boolean defining if it's purely for cast.

The element uses flexbox to grow to fill up the size of the element.

#Setup
Use [Bower](http://bower.io/) to include the cast-volume-controller in your web app.  The following 
command will add the cast-volume-controller and it's dependencies to your project.

    bower install --save googlecast/cast-volume-controller-polymer
    
#Integration
The easiest way to integrate is to use one of the already provided elements which contain 
cast-volume-controller.  The instructions below cover a custom integration.  You'll need to first 
include 
[Polymer](https://www.polymer-project.org/0.5/docs/start/getting-the-code.html).

##Including the element
In your html include the element

    <link rel="import"
        href="bower_components/cast-volume-controller-polymer/cast-volume-controller-polymer.html">
        
Add the element to your HTML defining whether it'll be used in the cast control bar.  And pass it
 the castManager object.
 
    <cast-volume-controller id="volume_controller"
        cast="true" castManager="{{ castManager }}"></cast-volume-controller>

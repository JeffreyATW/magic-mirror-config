# MagicMirror² config files

This is a repository of my custom config and CSS files for [MagicMirror²](https://github.com/MichMich/MagicMirror).

Here's what it looks like in real life. The background image changes every minute:

![54FFF552-168C-47AA-A7F5-6268010F0C68_1_105_c](https://user-images.githubusercontent.com/266170/177386446-ffdcddcf-0b28-422f-8434-16699e846f32.jpeg)

## Hardware setup

I installed MagicMirror² on a [Raspberry Pi 3B+](https://www.raspberrypi.com/products/raspberry-pi-3-model-b-plus/). It's connected via this [low profile cable](https://www.amazon.com/gp/product/B07RL574BB) to an [Acer S271HL](https://g.co/kgs/Ay74Qs) (although any monitor with a VESA mounting interface will do - it's just what I had lying around) using this [slim mount](https://www.amazon.com/gp/product/B00QOQAHNE). I attached the Pi, adapters, and [power cables](https://www.amazon.com/gp/product/B071XDRQWP) to the back of the monitor using velcro tape. (The Pi's included power adapter is too large to fit comfortably behind the monitor but I found that a 12W iPad adapter and a good micro USB cable did the trick.)

## Software setup

I'm running the latest version of [MagicMirror²](https://github.com/MichMich/MagicMirror). The custom modules I have installed are [`MMM-CalendarExt2`](https://github.com/MMM-CalendarExt2/MMM-CalendarExt2) and [`MMM-GooglePhotos`](https://github.com/aneaville/MMM-GooglePhotos). See each page for installation. The most difficult part was authenticating with Google Photos to access my albums.

If you'd like to use these files, install the above custom modules, and copy `config/config.js` and `css/custom.css` into your MagicMirror² checkout. You'll find some notes in each file, suffixed with `- JeffreyATW`, where you'll have to enter some of your own info.

I made a slight change to `MMM-CalendarExt2` to disable fade-out and fade-in when the calendar refreshes. If you'd like to make the same change, here's the diff:

```diff
diff --git a/CALEXT2_View.js b/CALEXT2_View.js
index 95a6f4f..33e37d5 100644
--- a/CALEXT2_View.js
+++ b/CALEXT2_View.js
@@ -68,7 +68,8 @@ class View {

   destroy() {
     this.hide();
-    setTimeout(() => {
+    // Disable delay in destroying slots
+    // setTimeout(() => {
       if (this.slots) {
         for (let i = 0; i < this.slots.length; i++) {
           this.slots[i].destroy();
@@ -82,7 +83,7 @@ class View {
           }
         }
       }
-    }, 500);
+     // }, 500);
   }

   filterEvents(events) {
diff --git a/MMM-CalendarExt2.js b/MMM-CalendarExt2.js
index cc69324..3af8e4f 100644
--- a/MMM-CalendarExt2.js
+++ b/MMM-CalendarExt2.js
@@ -398,9 +398,10 @@ Module.register("MMM-CalendarExt2", {

     if (this.currentScene) this.currentScene.clearViews();
     this.currentScene = new Scene(uid, this.config);
-    setTimeout(() => {
+    // Disable delay in creating slots
+    // setTimeout(() => {
       this.currentScene.draw(this.events);
-    }, 500);
+    // }, 500);

     if (this.config.rotateInterval > 0) {
       this.rotateTimer = setTimeout(() => {
```

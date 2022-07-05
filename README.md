This is a repository of my custom config and CSS files for [MagicMirror²](https://github.com/MichMich/MagicMirror).

The custom modules I have installed are [`MMM-CalendarExt2`](https://github.com/MMM-CalendarExt2/MMM-CalendarExt2) and [`MMM-GooglePhotos`](https://github.com/aneaville/MMM-GooglePhotos).

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

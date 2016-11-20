# Features to be considered for Next Version

Feature requests and new requirements for the next version of the [Pointer Lock specification](https://w3c.github.io/pointerlock/) are gathered here for consideration in subsiquent versions of the specification.

Submit a feature request by filing a [Pointer Lock Issue](https://github.com/w3c/pointerlock/issues) or submiting a pull request with changes to this document.

## Pointer Clip: Limiting movement of the cursor without hiding it

* Restrict pointer to a rectangle (while either windowed or in fullscreen (relevant for multi-display))
* Suppress any user agent or operating system UI elements that appear when hovering cursor in a region. This prevents e.g. a "hover near top of screen to bring down fullscreen exit instruction reminder" or the Mac OSX Dock that appears at screen edges.
* Security issues would then be essentially the same as pointer lock, the difference being that a) the pointer is not hidden, b) the pointer is not warped, c) the pointer is bounded by the area specified by the web app - not the user agent selected rectangle used as an implementation detail of pointer lock.
* [Notes on Pointer Clip from a Chromium discussion](https://docs.google.com/a/chromium.org/document/d/1lfU5BwiBaC0CeqsbUWLGGKtAr5tho6PBrN2zXk3he6A/edit?pli=1).
* See thread [Problems with mouse-edge scrolling and games](http://lists.w3.org/Archives/Public/public-webapps/2014JanMar/0473.html).


## Raw movement data, not pixel location clamped, and unmodified by operating system 'acceleration' or 'ballistics'

* Operating systems perform conditioning of mouse input data to facilitate use for a system pointer. Typically faster mouse movement results in a larger pointer movement for the same distance traveled. Some articles on this topic:
  * http://blog.codinghorror.com/mouse-ballistics/
  * https://msdn.microsoft.com/en-us/library/windows/desktop/ee418864.aspx
* Sub pixel movement accuracy doesn't offer a pixel based screen pointer an advantage, but may have meaningful interpretation by applications using Pointer Lock.

## Per-pointing device locking

* Different devices may require different operational modes. Extend [`requestPointerLock`](https://w3c.github.io/pointerlock/) with an option to pick devices to pointer lock.
  * A system may have more than one pointing device available to it. Allow the application to lock only some devices.
  * In [Pointer Events API](https://w3c.github.io/pointerevents/#pointerevent-interface), different devices report different `pointerId`'s. Ideally, `requestPointerLock` could accept that device.
  * w3c/pointerevents#49 raises the possibility of multiple concurrent mice, along with a link to [Multi-pointer X](https://wiki.archlinux.org/index.php/Multi-pointer_X) where this is so.
* Examples:
  * A 1st person game might want to use keyboard/mouse to control the camera, but allow a user to manipulate their on-screen inventory via touch-screen if it detects both input devices.
  * Multiple players with mice might have different roles in a game: a ship pilot has a 1st person like pointer lock mode, while a navigator needs a normal cursor interacting with a map.

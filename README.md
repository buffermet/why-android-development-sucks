You can take this to your psychiatrist.

# 1. API

## 1.1 Screen size

Developer: "Hey Google, I got a simple question for you: what is the height of my device's display?"

Google: "This is how to get the height of your display:"

```java
final WindowManager windowManager = (WindowManager) context.getSystemService(Context.WINDOW_SERVICE);
final Display display = windowManager.getDefaultDisplay();
final Point size = new Point();
display.getSize(size);

final int displayHeight = size.y;
```

Developer: "Ok, let me give that a try. Nope! It's about 80dp short, what's going on Google?"

Google: "Well, please describe what display you are talking about. You could be talking about the physical size of the display, but what if you mean the display size minus the status bar height, minus the navigation bar height? Did you perhaps mean the REAL display height?"

Developer: "Jesus Christ..."

Google: "Ok, fine, here you go, this is how to get the REAL display height:"

```java
final WindowManager windowManager = (WindowManager) context.getSystemService(Context.WINDOW_SERVICE);
final Display display = windowManager.getDefaultDisplay();
final Point size = new Point();
display.getRealSize(size);

final int realDisplayHeight = size.y;
```

Developer: "Google, WTF! Why do you differentiate display.getSize() and display.getRealSize()"

Google: "Well, we're not sure if you're competent enough to subtract the status bar height and the navigation bar height yourself, so we prechewed that for you :D cool right?!"

Developer: "What the... Whatever. Speaking of the status bar and navigation bar, how do I get the height of those?"

Google: "It's quite simple, all you need to do is this:"

```java
int statusBarHeight = 0;
final int resourceId = getResources().getIdentifier("status_bar_height", "dimen", "android");
if (resourceId > 0) {
    statusBarHeight = getResources().getDimensionPixelSize(resourceId);
}
```

```java
int navigationBarHeight = 0;
final WindowManager windowManager = (WindowManager) context.getSystemService(Context.WINDOW_SERVICE);
final Display display = windowManager.getDefaultDisplay();
final Point displaySize = new Point();
display.getRealSize(displaySize);
final Point realDisplaySize = new Point();
display.getSize(realDisplaySize);

if (displaySize.x < realDisplaySize.x) {
    navigationBarHeight = new Point(realDisplaySize.x - displaySize.x, displaySize.y).y;
}
if (displaySize.y < realDisplaySize.y) {
    navigationBarHeight = new Point(displaySize.x, realDisplaySize.y - displaySize.y).y;
}
```

# X. IDE

# X. SDK

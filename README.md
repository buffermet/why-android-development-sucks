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

Google: "Well, please describe what display you are talking about. You could be talking about the physical height of the display, but what if you mean the display height minus the status bar height, minus the navigation bar height? Did you perhaps mean the REAL display height?"

Developer: "Jesus Christ..."

Google: "Ok, fine, here you go, this is how to get the REAL display height:"

```java
final WindowManager windowManager = (WindowManager) context.getSystemService(Context.WINDOW_SERVICE);
final Display display = windowManager.getDefaultDisplay();
final Point size = new Point();
display.getRealSize(size);

final int realDisplayHeight = size.y;
```

Developer: "Google, WTF! Why do you differentiate display.getSize() and display.getRealSize() ??"

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
final Point realDisplaySize = new Point();
display.getSize(displaySize);
display.getRealSize(realDisplaySize);

if (displaySize.x < realDisplaySize.x) {
    navigationBarHeight = new Point(realDisplaySize.x - displaySize.x, displaySize.y).y;
}
if (displaySize.y < realDisplaySize.y) {
    navigationBarHeight = new Point(displaySize.x, realDisplaySize.y - displaySize.y).y;
}
```

Developer: \*pukes all over the fucking keyboard\*

# 1.2 Soft keyboard

Holy fucking shit, kill me already... (to be continued)

# 2. SDK

I'll cut right to the chase. Android Studio is the worst fucking dev environment ever devised.

I finally worked out a system to quickly navigate in these damn bloated XML files, and guess what, you fuck it all up when I make 1 little change using the design view. 

1. you don't just add newlines, you add two
2. you don't adopt my style of identation, you use your own (you indent twice for attributes)
3. YOU **INSIST ON MAKING ME EXPAND A TAG TO SEE WHAT ITS ID IS**. DO YOU EVEN USE YOUR OWN SDK????

How much time I have wasted changing this:

![Screenshot from 2019-07-24 22-40-11](https://user-images.githubusercontent.com/29265684/61794774-3a075600-ae65-11e9-9398-b531011b8680.png)


Back to this:

![Screenshot from 2019-07-24 22-41-25](https://user-images.githubusercontent.com/29265684/61794787-455a8180-ae65-11e9-98bc-e223e66ba663.png)

And who the fuck ever thought XML was a good idea? Just take 1 glimpse at CSS and you see that none of this bullshit was ever necessary.

And guess what, if one asks how to disable ONE of these annoyances, one gets the following response: use power save mode (aka disable fucking everything, aka notepad).

Fuck me dead.

## 2.1 Emulator

Google is lazy beyond comprehension. (to be continued)

# 3. DOCS

<img alt="depressing android docs" src="https://user-images.githubusercontent.com/29265684/60115639-b6047480-97b9-11e9-81b6-849641f66156.png">

It surprises me how Google can do so well writing GoDoc, and fail so miserably at writing Android Documentation.

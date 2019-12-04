You can take this to your psychiatrist.

# 1. APIs

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

Developer: \*vomits on keyboard\*

# 1.2 Soft keyboard

Actually this one's not that bad, except hiding the keyboard should simply take `ic.hideKeyboard()` or a global `hideKeyboard()` instead of a combination of hacks...

# 1.3 What the fuck

Ever heard of word wrap?

This is unbelievable: https://stackoverflow.com/questions/45720678/textview-breaks-my-word-by-letters

```
highQuality
normal
none
chrome session restore much appreciate
```

# 1.4 English vocabulary, grammar and binary logic

Dear google, this `_` is horizontal and this `|` is vertical.

When we are talking about horizontal or vertical alignment, we are talking about alignment along the horizontal or vertical **axis**.

# 1.5 Binary logic

When dealing with binary logic (on/off switches), there is no superposition.

When dealing with keyboard input, there is no state inbetween pressing the key and releasing it.

```
// terminology of the current EditText API
beforeTextChanged() // technically this counts as the entire duration from boot until a key press
onTextChanged()     // this would make sense if it did what beforeKeyPressed() currently does, but instead it's redundant and confusing
afterTextChange()   // makes sense, except there seems to be an arbitrary delay of <=500ms

// how it should read following the current logic
() // keypress detected but not parsed yet
() // keypress detected and asynchronously parsed
() // keypress detected and parsing finished

// what it should be
... -> {
    @Override
    public void () {

    }
    @Override
    public void () {

    }
});
```

# 2. SDK

When you finally work out the quickest way to navigate in these prefix:bloated XML files, the battle begins. 

You'll maintain a consistent use of a single indent for function parameters, but Android Studio/IDEA.
2. you don't adopt my style of identation, you use your own (you indent twice for attributes)
3. YOU **INSIST ON MAKING ME EXPAND A TAG TO SEE WHAT ITS ID IS**. DO YOU EVEN USE YOUR OWN SDK????

How much time I have wasted changing this:

![Screenshot from 2019-07-24 22-40-11](https://user-images.githubusercontent.com/29265684/61794774-3a075600-ae65-11e9-9398-b531011b8680.png)


Back to this:

![Screenshot from 2019-07-24 22-41-25](https://user-images.githubusercontent.com/29265684/61794787-455a8180-ae65-11e9-98bc-e223e66ba663.png)

And who thought XML was a good idea? Just take 1 glimpse at CSS and you see that none of this bullshit was ever necessary.

And guess what, if one asks how to disable ONE of these annoyances, one gets the following response: use power save mode (aka disable everything, aka notepad).

## 2.1 Emulator

Google is lazy beyond comprehension. (to be continued)

# 3. DOCS

<img alt="depressing android docs" src="https://user-images.githubusercontent.com/29265684/60115639-b6047480-97b9-11e9-81b6-849641f66156.png">

It surprises me how Google can do so well writing GoDoc, and fail so miserably at writing Android Documentation.

You can take this to your psychiatrist.

# 0. Device Encryption

Android device encryption goes a little something like this:

![gif](https://user-images.githubusercontent.com/29265684/60131122-fecd2500-97db-11e9-90f9-8a756f525a62.gif)

That's right, by default, your encryption key (`default_password`) can decrypt all your personal data. Only after doing research you can find out that this default encryption can be utterly useless, and you are advised to "strengthen" this encryption by setting a secure screen lock password, pattern or PIN. Most manufacturers promise that your device is secured with a TEE (such as TrustZone), however, whether your device is indeed secured with a TEE depends on your manufacturer. There are 1900 registered Android device manufacturers (give or take), there are many unregistered manufacturers, supply chain attackers and second hand sellers. Apple is very determined to avoid these issues by preventing people from getting a root shell, but we're not talking about iOS/iPadOS right now, we're talking about Android.

You don't use a long and complicated key to unlock your phone, do you? Probably not, you would have arthritis by next week, because you unlock your phone tens if not hundreds of times a day.

The way Google treats device encryption is absolutely pathetic, and should learn from Apple. However, Apple should also get their shit together and use people's iCloud password to encrypt their device, which people should ONLY have to enter when their device performs a cold boot.

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

Developer: "I think I need to throw up..."

# 1.2 Soft keyboard

Holy fucking shit, kill me already... (to be continued)

# X. IDE

# X. SDK

# X. DOCS

<img alt="depressing android docs" src="https://user-images.githubusercontent.com/29265684/60115639-b6047480-97b9-11e9-81b6-849641f66156.png">

It surprises me how Google can do so well writing GoDoc, and fail so miserably at writing Android Documentation.

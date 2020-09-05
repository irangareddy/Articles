
# Material Banner in Flutter

![](https://dev-to-uploads.s3.amazonaws.com/i/edaphlhzt6of7qwi3e22.png)

Banners should be displayed at the top of the screen, below a top app bar. They’re persistent and nonmodal, allowing the user to either ignore them or interact with them at any time. Only one banner should be shown at a time.

## What is a Banner

A banner displays an important, succinct message, and provides actions for users to address (or dismiss the banner). It requires a user action to be dismissed.

source: [Material.io](https://material.io/)

### Let's Build a Banner like this

<!-- <p align="center">
<a href="https://github.com/irangareddy/Flutter-UI-Components-Library/blob/master/lib/material/banner.dart">
<img src="https://github.com/irangareddy/Flutter-UI-Components-Library/blob/master/Gifs/MaterialBanner.gif?raw=true" width="250" alt="Material Bannerr" >
</a>
</p> -->

This is actually what we going to make by the end of this article. Load up your energy and let's get started.

### Material Banner

```dart
class BannerScreen extends StatefulWidget {
  @override
  _BannerScreenState createState() => _BannerScreenState();
}

class _BannerScreenState extends State<BannerScreen> {
  

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        backgroundColor: kPrimaryColor,
        title: Text("Material Banner"),
        centerTitle: false,
      ),
      body: SafeArea(
          child: Column(
        children: [
            MaterialBanner(
              leading: CircleAvatar(
                backgroundColor: kPrimaryColor,
                child: Icon(
                  Icons.subscriptions,
                  color: Colors.white,
                ),
              ),
              content: Padding(
                padding: const EdgeInsets.all(4.0),
                child: Column(
                  crossAxisAlignment: CrossAxisAlignment.start,
                  children: [
                    Text('WEEKLY RUNDOWN:',style: kHeadlineLabelStyle),
                    Padding(
                      padding: const EdgeInsets.only(top: 4.0),
                      child: Text('''
                    The case for a six-hour workday, An office model that suits everyone?, and other top news for you''',
                          style: kBodyTextStyle.copyWith(color: Colors.black)),
                    ),
                  ],
                ),
              ),
              actions: [
                FlatButton(
                  child: Text(
                    'DISMISS',
                    style: kActionTextStyle,
                  ),
                  onPressed: () {
                    // Dissmiss Function
                  },
                ),
                FlatButton(
                  child: Text('VIEW', style: kActionTextStyle),
                  onPressed: () {
                    // Custom implemention according to the banner.
                  },
                ),
              ],
            ),
          Spacer(),
          Row(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              FlatButton(
                onPressed: () {
                  // Dissmiss Function
                },
                child: Text(
                  'Toggle Banner',
                  style: kActionTextStyle,
                ),
              ),
            ],
          ),
          Spacer(),
        ],
      )),
    );
  }
}
```

- Create a `Stateful Widget` and name it as `BannerScreen` and add `MaterialBanner`to the `column` of the Screen.

- MaterialBanner has two `@required` properties those are `content` and `actions`.

- `content` is the place where you add your message/context for the Banner.

- `actions` we add buttons here one the them will be for dismissing the banner and other is an detail action related to banner.

### Manage Banner State

```dart
bool showBanner = false;
```

- Declare a `showBanner` property  which manages the appereance of the banner.

```dart
if(showBanner)
MaterialBanner(...)
```

- Write this `if` condition before banner, which shows banner only when `showBanner` is `true`

- we have declared a property but we didn't implement to change the property.

### Toggle Banner

```dart
  void _toggleBanner() {
    setState(() {
      showBanner = !showBanner;
    });
  }
```

- `_toggleBanner` is a private function which changes the value of the `showBanner` property according to the context.

- Add this fucntion to `Dismiss` Button and `Toggle Banner` Button.

- Implement custom code for the other button in `MaterialBanner` `actions` which acts to context of the banner.

### Conclusion

Use Banner when it's necessary that you want to convey an important message to the user otherwise, use notifications.

[GitHub Link](https://github.com/irangareddy/Flutter-UI-Components-Library/blob/master/lib/material/banner.dart)

If you like to improve your App Development Skills, even more in Flutter and SwiftUI. Feel free to dm me on [Instagram](https://www.instagram.com/irangareddy/)  or tweet to me on [Twitter](https://twitter.com/irangareddy) if you have any additional tips or feedback.

Thanks for reading!

# How to Create Context Menu in Flutter

Context Menu's most widely used UI Component in Mobile Development and with Flutter we can build it much more easily but, let's look at what is Contextual Menu is? (Contextual/Context referred as same)⁣

## What is a Contextual Menu

 A contextual menu is a type of menu that appears on demand and contains a small set of relevant actions related to a control, an area of the interface, a piece of data in the application, or a view of the application.⁣
⁣

## Let's Build a Context Menu like this

<p align="center">
<a href="https://github.com/irangareddy/Flutter-UI-Components-Library/blob/master/lib/material/contextMenu.dart">
<img src="https://github.com/irangareddy/Flutter-UI-Components-Library/blob/master/Gifs/ContextMenu.gif?raw=true" width="250" alt="Context Menu" >
</a>
</p>

This is actually what we going to make by the end of this article. Load up your energy and let's get started.

### Create a List

```dart
const List<String> choices = <String>[
"Item 1",
"Item 2",
"Item 3",
];
```

The choices are a list of  String that represents the items in the Context Menu.

### Create a Stateful Widget

```dart
class MainScreen extends StatefulWidget {
  @override
  _MainScreenState createState() => _MainScreenState();
}


class _MainScreenState extends State<MainScreen> {
  @override
  Widget build(BuildContext context) {
    return Container(
        Text("Just Created a Stateful Widget")
    );
  }
}
```

MainScreen is a Stateful widget that manages the state of the context menu selection.

### Add these Variabes to _MainScreenState

```dart
  final GlobalKey<ScaffoldState> _scaffoldkey = new GlobalKey<ScaffoldState>();
  String _selectedChoices;
```

- `_scaffoldKey` is a GlobalKey that provides access to ScaffoldState and this helps identify the state uniquely.
- selected `choices` is a  String to store the current choice.

`
Note: underscore before a variable refers as a private  variable in dart
`

### Adding Context Menu to the MainScreen

```dart
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      key: _scaffoldkey,
      appBar: AppBar(
        title: Text('Context Menu'),
        elevation: 0,
        centerTitle: false,
        backgroundColor: kPrimaryColor,
        actions: <Widget>[
          PopupMenuButton(
            onSelected: _select,
            padding: EdgeInsets.zero,
            // initialValue: choices[_selection],
            itemBuilder: (BuildContext context) {
              return choices.map((String choice) {
                return  PopupMenuItem<String>(
                value: choice,
                child: Text(choice),
              );}
              ).toList();
            },
          )
        ],
      ),
      body: BodyWidget(selection: _selectedChoices),
    );
  }
```

we need to manage three things while adding the Context Menu

1. Assign the `_scaffoldkey` to the `key` property in the Scaffold.
2. [Actions in AppBar](#Actions-in-AppBar)
3. [Body Content in MainScreen](#Body-Content-in-MainScreen)

### Actions in AppBar

`PopupMenuButton` has `itemBuilder` property we use  `choices.map` to load each item into `PopupMenuItem` and display the content with `child` property.

`value` is the property which will be returned to on selection of the item

`PopupMenuButton` has `onSelection` property which gets the choice of the selection from `value` and passes the value to `_select` function.

```dart
  void _select(String choice) {
    setState(() {
      _selectedChoices = choice;
    });
    showSnackBar(choice);
  }
```

`_select` is a function that will be called from `onSelected` property of the `PopupMenuButton` which stores the choice of the user to a `_selectedChoices` and call's the `snowSnackBar`

```dart
void showSnackBar(String selection) {
    final snackBarContent = SnackBar(
            content: Text('Selected: $selection',style: kBodyTextStyle,),
            action: SnackBarAction(
              label: 'Undo',
              textColor: kSecondaryColor,
              onPressed: () {
                // Some code to undo the change.
              },
            ),
          );
    _scaffoldkey.currentState.showSnackBar(snackBarContent);
  }
```

`showSnackBar` is a function that accepts the current `selection` of the context menu  an displays the SnackBar over a Scafolld using `_scaffoldkey.currentState.showSnackBar(snackBarContent)` and we can also add more functionality to the SnackBar with `onPressed` property.

### Body Content in MainScreen

```dart
class BodyWidget extends StatelessWidget {
  const BodyWidget({
    Key key,
    @required String selection,
  }) : _selection = selection, super(key: key);

  final String _selection;

  @override
  Widget build(BuildContext context) {
    return Column(
      crossAxisAlignment: CrossAxisAlignment.center,
      mainAxisAlignment: MainAxisAlignment.center,
      children: <Widget>[
        _selection != null ?
        Center(child: Text("Selected: $_selection",style: kBodyTextStyle,),) :
        Center(child: Text("Welcome to Flutter UI Components Library",style: kBodyTextStyle,),),
      ],
    );
  }
}
```

`BodyWidget` is a StatelessWidget class which accepts the `_selection` of the context menu and displays the current selection of the conext menu if `_selection` is null then display the sample text.

### Conclusion

Adding Context Menu to the Application gives more flexbility to the user for smaller actions. With simple PopupMenuButton you easily add a Context Menu in a few lines of code. The functions helps you add much more functionality to show a SnackBar and changing a state in the body.

[GitHub Link](https://github.com/irangareddy/Flutter-UI-Components-Library/blob/master/lib/material/contextMenu.dart)

If you like to improve your App Development Skills, even more in Flutter and SwiftUI. Feel free to dm me on [Instagram](https://www.instagram.com/irangareddy/)  or tweet to me on [Twitter](https://twitter.com/irangareddy) if you have any additional tips or feedback.

Thanks for reading!

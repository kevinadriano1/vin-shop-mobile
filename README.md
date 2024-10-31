# vin_shop

## assignment 7

### Explain what are stateless widgets and stateful widgets, and explain the difference between them.

Stateless widgets are immutable widgets. Once they are built, their properties cannot change. They do not maintain any internal state and are rebuilt only when their parent widget changes.
example:
```
class MyStatelessWidget extends StatelessWidget {
  final String title;

  MyStatelessWidget(this.title);

  @override
  Widget build(BuildContext context) {
    return Text(title); // This widget will not change after it's created.
  }
}
```

Stateful widgets are mutable widgets that maintain their state over time. They can change their appearance in response to events triggered by user interactions or other changes in data.
example:
```
class MyStatefulWidget extends StatefulWidget {
  @override
  _MyStatefulWidgetState createState() => _MyStatefulWidgetState();
}

class _MyStatefulWidgetState extends State<MyStatefulWidget> {
  int _counter = 0; // Internal state

  void _incrementCounter() {
    setState(() {
      _counter++; // Updating the state
    });
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        Text('Counter: $_counter'),
        ElevatedButton(
          onPressed: _incrementCounter,
          child: Text('Increment'),
        ),
      ],
    );
  }
}
```

### Mention the widgets that you have used for this project and its uses.
1. StatelessWidget
Used in: MyHomePage, InfoCard, ItemCard
Purpose: This is the base class for widgets that do not require mutable state. The UI for these widgets is built once and does not change over time.
2. Scaffold
Purpose: Provides the basic visual structure for the app, including the AppBar and body. It helps to implement the standard material design layout.
3. AppBar
Purpose: Displays a material design app bar at the top of the screen. It can contain titles, icons, and other widgets.
4. Padding
Purpose: Adds padding around its child widget. In your code, it's used to create space around the main content of the page.
5. Column
Purpose: Arranges its children vertically. In your case, it’s used to layout the information cards and other content.
6. Row
Purpose: Arranges its children horizontally. It's used to display the InfoCard widgets side by side.
7. SizedBox
Purpose: Provides a fixed size box, used here to add vertical spacing between widgets.
8. Center
Purpose: Centers its child widget within the available space. Used to align the welcome message and grid of item cards.
9. GridView
Purpose: Creates a scrollable, 2D array of widgets. You used it to display the ItemCard widgets in a grid layout.
10. Card
Purpose: A material design card that provides a surface for displaying content. Used to encapsulate the InfoCard and ItemCard.
11. Container
Purpose: A versatile widget that can be used to create boxes with various styling options (padding, margin, size). Used inside cards and other areas to manage layout.
12. Text
Purpose: Displays a string of text with a single style. Used for titles, labels, and messages throughout the app.
13. Icon
Purpose: Displays a material design icon. Used in the ItemCard to represent actions visually.
14. InkWell
Purpose: A material design widget that responds to touch events. It provides a ripple effect on tap, enhancing user interaction. Used in the ItemCard for clickable actions.
15. SnackBar
Purpose: A lightweight message that displays temporarily at the bottom of the screen. Used to show feedback when an item card is pressed.
16. Material
Purpose: A widget that provides a material design style to its child. Used to give the ItemCard a background color and rounded borders.
17. MediaQuery
Purpose: Provides information about the size and orientation of the screen. Used to determine the width of the device for responsive design.

### What is the use-case for setState()? Explain the variable that can be affected by setState().
Use-Case for setState()
Updating UI in Response to User Interaction: Whenever a user interacts with the UI (like tapping a button or entering text), you might want to change the visual appearance of the widget based on this interaction. For example, if a button is pressed, you may want to change the text displayed or update an image.
Changing State Based on Events: If your application needs to respond to events, such as data fetched from a server or changes in user input, you can use setState() to reflect these changes in the UI.
Animating Widgets: In animations, you can use setState() to update the properties of animated widgets to create smooth transitions and animations.
Variables Affected by setState(): int, double, bool, String, List or Map, Custom Objects

### Explain the difference between const and final keyword.
Const
Definition: const is used to declare compile-time constants. This means that the value must be determined at compile time and cannot be changed afterward.
Immutability: All values assigned to a const variable are immutable.
Usage: When you use const, Dart creates a canonical instance for the value, meaning that if you use the same constant expression multiple times, Dart will only create one instance of that value.

Final
Definition: final is used to declare a variable that can only be set once. The value of a final variable is determined at runtime and can be any expression that is not necessarily a constant.
Immutability: Once a final variable is assigned a value, it cannot be reassigned. However, if the value is a mutable object (like a list or a map), the contents of that object can still be changed.
Usage: You can use final when the value is not known until runtime but should remain constant throughout the lifetime of the variable.

### Create three simple buttons with icons and texts for: Viewing the product list (View Product List) Adding a product (Add Product) Logout (Logout)

make menu.dart in vin_shop/lib, add this in MyHomePage class
```
final List<ItemHomepage> items = [
        ItemHomepage("View Product List", Icons.store, Colors.blue),
        ItemHomepage("Add Product", Icons.add, Colors.green),
        ItemHomepage("Logout", Icons.logout, Colors.red),
     ];
```
the items list serves as a collection of menu items that can be displayed in the UI. Each menu item has a title, an associated icon, and a color, making it visually appealing and informative for users. The final keyword ensures that the reference to this list remains constant throughout the lifecycle of the widget, maintaining the integrity of the menu options.


also add this inside ItemHomePage class
```
    final String name;
    final IconData icon;
    final Color color;

    ItemHomepage(this.name, this.icon, this.color);

```
The ItemHomepage class encapsulates the information required to represent a menu item in your application. It consists of a name, an icon, and a color, and the constructor initializes these properties, ensuring that they are set when an object of the class is created. This structure allows for easy management and representation of menu items in your UI.

add this in ItemCard class
```
Widget build(BuildContext context) {
    return Material(
      // Specify the background color of the application theme.
      color: item.color,
      // Round the card border.
      borderRadius: BorderRadius.circular(12),
      
      child: InkWell(
        // Action when the card is pressed.
        onTap: () {
          // Display the SnackBar message when the card is pressed.
          ScaffoldMessenger.of(context)
            ..hideCurrentSnackBar()
            ..showSnackBar(
              SnackBar(content: Text("You have pressed the ${item.name} button!"))
            );
        },
        // Container to store the Icon and Text
        child: Container(
          padding: const EdgeInsets.all(8),
          child: Center(
            child: Column(
              // Place the Icon and Text in the center of the card.
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                Icon(
                  item.icon,
                  color: Colors.white,
                  size: 30.0,
                ),
                const Padding(padding: EdgeInsets.all(3)),
                Text(
                  item.name,
                  textAlign: TextAlign.center,
                  style: const TextStyle(color: Colors.white),
                ),
              ],
            ),
          ),
        ),
      ),
    );
  }
```
this build method creates a visually appealing card for each menu item that reacts to user taps. The combination of Material, InkWell, and other layout widgets provides a structured and responsive UI element that enhances the user experience in your Flutter application.

### Implement different colors for each button (View Product List, Add Product, and Logout).
add colour in final list
```
final List<ItemHomepage> items = [
        ItemHomepage("View Product List", Icons.store, Colors.blue),
        ItemHomepage("Add Product", Icons.add, Colors.green),
        ItemHomepage("Logout", Icons.logout, Colors.red),
     ];
```
in this example it will use blue, greeen and red

make sure there is color in ItemHomePage class
```
final Color color;

    ItemHomepage(this.name, this.icon, this.color);
```

add this in widget build
```
color: item.color,

```

### Display a Snackbar with the following messages:"You have pressed the View Product List button" when the View Product List button is pressed. "You have pressed the Add Product button" when the Add Product button is pressed. "You have pressed the Logout button" when the Logout button is pressed.

add this in your widget  inside inkwell

```
onTap: () {
          // Display the SnackBar message when the card is pressed.
          ScaffoldMessenger.of(context)
            ..hideCurrentSnackBar()
            ..showSnackBar(
              SnackBar(content: Text("You have pressed the ${item.name} button!"))
            );
        },
```
this onTap implementation effectively handles the tap gesture on the card. When the user taps on the card, the currently visible SnackBar (if any) is dismissed, and a new SnackBar is displayed with a message indicating which button was pressed. This provides immediate feedback to the user about their action, enhancing the user experience.
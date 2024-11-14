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

## assignment 8

### What is the purpose of const in Flutter? Explain the advantages of using const in Flutter code. When should we use const, and when should it not be used?
the const keyword creates compile-time constants and is used to optimize widget performance by marking widgets as immutable when their values won’t change. This can improve the app's efficiency and responsiveness by minimizing rebuilds and memory usage.
When to Use const:
Stateless Widgets with Fixed Data: If a widget (like a Text, Icon, or custom stateless widget) does not change during its lifecycle, use const.
Repeated Widgets: For widgets that appear multiple times with the same configuration, using const avoids creating multiple instances.
Literal Values: When working with literal values that don’t change (like strings, numbers, or colors), marking them as const is beneficial.
When const Should Not Be Used:
Stateful Widgets: Avoid const if the widget depends on state changes. Stateful widgets typically don’t qualify as constants because their values or UI elements can change over time.
Dynamic or Variable Data: If you’re creating widgets that depend on user input, API data, or other runtime variables, const is not suitable since the widget configuration changes with each render.

### Explain and compare the usage of Column and Row in Flutter. Provide example implementations of each layout widget!

Column Widget
Purpose: Arranges child widgets in a vertical layout, from top to bottom.
Main Axis: The main axis is vertical (top to bottom).
Cross Axis: The cross axis is horizontal (left to right).
Usage: Ideal for stacking widgets vertically, like displaying a list of items, creating a vertical form, or aligning widgets within a vertical layout.
Example Implementation of Column
Here’s an example of how to use Column to create a vertically stacked list of widgets.
```
Column(
  mainAxisAlignment: MainAxisAlignment.center, // Center widgets vertically
  crossAxisAlignment: CrossAxisAlignment.start, // Align widgets to the start horizontally
  children: <Widget>[
    Text('Item 1'),
    Text('Item 2'),
    ElevatedButton(
      onPressed: () {},
      child: Text('Press Me'),
    ),
  ],
)
```

Row Widget
Purpose: Arranges child widgets in a horizontal layout, from left to right.
Main Axis: The main axis is horizontal (left to right).
Cross Axis: The cross axis is vertical (top to bottom).
Usage: Ideal for placing widgets side by side, like creating a toolbar, a horizontal button layout, or aligning text next to an icon.
Example Implementation of Row
Here’s an example of using Row to create a horizontal layout.

```
Row(
  mainAxisAlignment: MainAxisAlignment.spaceAround, // Space out widgets evenly horizontally
  crossAxisAlignment: CrossAxisAlignment.center,    // Center widgets vertically
  children: <Widget>[
    Icon(Icons.star, color: Colors.yellow),
    Text('Star'),
    ElevatedButton(
      onPressed: () {},
      child: Text('Press Me'),
    ),
  ],
)
```

### List the input elements you used on the form page in this assignment. Are there other Flutter input elements you didn’t use in this assignment? Explain!

the following Flutter input elements are used:

TextFormField: This element is used for each of the fields to collect data such as name, price, description, and rating. Each TextFormField is configured to:

Show a hint and label.
Validate user input (e.g., to ensure price and rating are numeric).
Collect input based on onChanged events.
ElevatedButton: Used as a submission button to save the form data. When pressed, it triggers validation and, if all fields are valid, shows an AlertDialog confirming the save.

Other Common Input Elements Not Used in This Assignment
Checkbox: Useful for allowing users to select multiple options or toggle a setting.
Radio: Allows a user to select a single option from a list of mutually exclusive choices.
Switch: Commonly used as an on/off toggle for settings.
DropdownButton: Displays a dropdown menu for selecting one option from a list.
Slider: Provides a way for users to select a value within a range, commonly used for setting numeric values like volume or brightness.

### How do you set the theme within a Flutter application to ensure consistency? Did you implement a theme in your application?
To set the theme, use the theme parameter in the MaterialApp widget, which typically resides in the main.dart file. You can define various theme properties here, including colors, fonts, and text styles.

Here’s an example of how to set a theme:

```
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'My App',
      theme: ThemeData(
        primarySwatch: Colors.blue, // Primary color for AppBar, buttons, etc.
        colorScheme: ColorScheme.fromSwatch().copyWith(
          secondary: Colors.amber, // Accent color for highlights, icons, etc.
        ),
        textTheme: TextTheme(
          headline1: TextStyle(fontSize: 24.0, fontWeight: FontWeight.bold),
          bodyText1: TextStyle(fontSize: 16.0, color: Colors.grey[800]),
        ),
        buttonTheme: ButtonThemeData(
          buttonColor: Colors.blue,
          textTheme: ButtonTextTheme.primary,
        ),
      ),
      home: HomePage(),
    );
  }
}
```
im not using theme in my project

### How do you manage navigation in a multi-page Flutter application?
1. Using Navigator.push and Navigator.pop
Navigator.push: Adds a new route (or screen) to the navigation stack, allowing the user to navigate from one screen to another. It enables the user to return to the previous screen by pressing the back button or using Navigator.pop.

Navigator.pop: Removes the current route from the stack, effectively "popping" it, and returning to the previous screen.

2. Using Named Routes
Named routes provide a more organized way to handle navigation in applications with multiple pages. They are defined in the MaterialApp widget, enabling navigation by route name rather than creating new route instances.

3. Using Navigator.pushReplacement and Navigator.pushAndRemoveUntil
Navigator.pushReplacement: Replaces the current screen with a new one, preventing the user from navigating back to the previous screen.

Navigator.pushAndRemoveUntil: Pushes a new route and removes all previous routes from the stack until a specified route is reached.

4. Using Navigator.popUntil
This method pops routes off the navigation stack until a specific condition is met. It’s useful for navigating back to a specific screen without manually tracking the stack.

5. Using WillPopScope to Control Back Navigation
WillPopScope intercepts the back button press and allows you to control whether the user should leave the screen. It’s useful for showing confirmation dialogs or saving data before leaving the screen.

## assignment 9
### Explain why we need to create a model to retrieve or send JSON data. Will an error occur if we don't create a model first?
Using a model to handle JSON data in Django isn’t mandatory but offers significant benefits. A model provides a structured schema, ensuring data consistency and validation, and integrates smoothly with Django’s ORM for efficient data storage and retrieval. It also simplifies JSON serialization and deserialization, especially in API contexts. Without a model, you’d need to manage validation, database interaction, and serialization manually, which complicates development. While you can handle JSON data directly, using a model streamlines data handling and enhances maintainability in Django applications.

### Explain the function of the http library that you implemented for this task.
The http library in this task serves as a toolkit for making HTTP requests and handling responses. Its core functions typically include methods for sending GET, POST, PUT, and DELETE requests, enabling communication between client and server over the HTTP protocol. Here’s a breakdown of its primary functions and components:

GET Requests: This function retrieves data from the specified URL. It's useful for fetching resources or information from an API endpoint without modifying server data.

POST Requests: This function sends data to the server, often used for creating or updating resources. The library formats the data (typically as JSON or form-encoded data) and includes it in the request body.

PUT and DELETE Requests: The PUT function is used to update existing resources, while DELETE removes specified resources. These functions are essential for maintaining and modifying server data.

Response Handling: The library typically includes response-handling functions to decode data (often in JSON format) and manage errors by checking HTTP status codes. This simplifies the process of retrieving information from responses and identifying request errors.

Header and Timeout Management: The library often allows for customizing headers (like authentication tokens) and setting timeouts for requests, adding flexibility and control over HTTP interactions.

### Explain the function of CookieRequest and why it’s necessary to share the CookieRequest instance with all components in the Flutter app.
CookieRequest is a custom class used in a Flutter app to manage HTTP requests that require cookies for session-based authentication. Its primary function is to handle and store cookies, which are often used to maintain user sessions with the server. By preserving cookies across multiple requests, CookieRequest enables the app to remember the user's login status and keep the user authenticated as they navigate between different parts of the app. Without a shared CookieRequest instance, each component would create its own instance, leading to a loss of session cookies between requests. This would break session continuity, forcing users to re-authenticate frequently. Sharing the instance enables a seamless and authenticated experience, keeping the user logged in across all components in the app.

### Explain the mechanism of data transmission, from input to display in Flutter.
In a Flutter app, the process of transmitting and displaying data follows a clear flow, starting from user input, processing the data, and ultimately rendering it on the screen. Here’s a breakdown of each stage:

User Input:
The user enters data via interactive elements like text fields, dropdowns, or buttons. Flutter widgets, such as TextField for text input, capture this input, and listeners or controllers (e.g., TextEditingController) manage it, allowing access to the input for further processing.

Data Processing and Validation:
After capturing the input, the app processes it. This can include validating the input (e.g., checking if required fields are filled or if the data matches a specific format) to ensure correctness before moving forward. Validation can occur locally in the widget or in a separate function to keep the UI and logic separate.

Data Transmission:
Once validated, the data is sent to a backend server or API if needed. For this, Flutter uses libraries like http or dio to make HTTP requests (e.g., a POST request for submitting data or a GET request to retrieve data). CookieRequest or similar classes handle authentication by attaching session cookies or tokens, ensuring that user-specific data is correctly authorized.

Response Handling:
The server responds to the request with data, typically in JSON format. Flutter decodes this JSON data into Dart objects using classes and data models, which makes it easier to work with in the app. The response may include confirmation of data submission, errors, or requested information.

Updating the UI:
Once the data is processed and transformed into the appropriate format, Flutter uses widgets to display it on the screen. Stateful widgets update dynamically when data changes, utilizing setState() or state management solutions (like Provider, Riverpod, or Bloc) to reflect the new data on the UI. This keeps the display responsive to any changes in data, whether from user input or server responses.

Rendering and Display:
Flutter’s rendering engine converts the widget tree into visual elements on the device screen, making it possible for the user to see the inputted or retrieved data in the UI. The process completes the loop, as the displayed data can be re-interacted with or further modified by the user.

### Explain the authentication mechanism from login, register, to logout. Start from inputting account data in Flutter to Django’s completion of the authentication process and display of the menu in Flutter.
1. Registration
The user enters details (e.g., username, email, password) in Flutter. This data is sent via a POST request to Django’s /register/ endpoint.
Django validates and creates the user in the database. A response is sent back to Flutter, confirming success or errors.
2. Login
The user enters their credentials in Flutter, which sends a POST request to Django’s /login/ endpoint.
Django authenticates the credentials and creates a session or returns a token for authentication.
Flutter saves the session cookie or token for future authenticated requests.
3. Menu Display
Upon successful login, Flutter uses the session or token to make authenticated requests to Django, retrieving user-specific data.
The app updates the UI to display the authenticated user’s menu or dashboard.
4. Logout
The user logs out by sending a request to Django’s /logout/ endpoint, which clears the session or invalidates the token.
Flutter clears the session or token and navigates the user back to the login screen.

### Implement the registration feature in the Flutter project. Create a login page in the Flutter project.
add this in django:
```
@csrf_exempt
def login(request):
    username = request.POST['username']
    password = request.POST['password']
    user = authenticate(username=username, password=password)
    if user is not None:
        if user.is_active:
            auth_login(request, user)
            # Successful login status.
            return JsonResponse({
                "username": user.username,
                "status": True,
                "message": "Login successful!"
                # Add other data if you want to send data to Flutter.
            }, status=200)
        else:
            return JsonResponse({
                "status": False,
                "message": "Login failed, account disabled."
            }, status=401)

    else:
        return JsonResponse({
            "status": False,
            "message": "Login failed, check email or password again."
        }, status=401)
    
@csrf_exempt
def register(request):
    if request.method == 'POST':
        data = json.loads(request.body)
        username = data['username']
        password1 = data['password1']
        password2 = data['password2']

        # Check if the passwords match
        if password1 != password2:
            return JsonResponse({
                "status": False,
                "message": "Passwords do not match."
            }, status=400)

        # Check if the username is already taken
        if User.objects.filter(username=username).exists():
            return JsonResponse({
                "status": False,
                "message": "Username already exists."
            }, status=400)

        # Create the new user
        user = User.objects.create_user(username=username, password=password1)
        user.save()

        return JsonResponse({
            "username": user.username,
            "status": 'success',
            "message": "User created successfully!"
        }, status=200)

    else:
        return JsonResponse({
            "status": False,
            "message": "Invalid request method."
        }, status=400)

@csrf_exempt
def logout(request):
    username = request.user.username

    try:
        auth_logout(request)
        return JsonResponse({
            "username": username,
            "status": True,
            "message": "Logged out successfully!"
        }, status=200)
    except:
        return JsonResponse({
        "status": False,
        "message": "Logout failed."
        }, status=401)
```
also dont forget to add login.dart and register.dart in screens directory

### Integrate the Django authentication system with the Flutter project.

add this in login.dart
```
void main() {
  runApp(const LoginApp());
}

class LoginApp extends StatelessWidget {
  const LoginApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Login',
      theme: ThemeData(
        useMaterial3: true,
        colorScheme: ColorScheme.fromSwatch(
          primarySwatch: Colors.deepPurple,
        ).copyWith(secondary: Colors.deepPurple[400]),
      ),
      home: const LoginPage(),
    );
  }
}

class LoginPage extends StatefulWidget {
  const LoginPage({super.key});

  @override
  State<LoginPage> createState() => _LoginPageState();
}

class _LoginPageState extends State<LoginPage> {
  final TextEditingController _usernameController = TextEditingController();
  final TextEditingController _passwordController = TextEditingController();

  @override
  Widget build(BuildContext context) {
    final request = context.watch<CookieRequest>();

    return Scaffold(
      appBar: AppBar(
        title: const Text('Login'),
      ),
      body: Center(
        child: SingleChildScrollView(
          padding: const EdgeInsets.all(16.0),
          child: Card(
            elevation: 8,
            shape: RoundedRectangleBorder(
              borderRadius: BorderRadius.circular(12.0),
            ),
            child: Padding(
              padding: const EdgeInsets.all(20.0),
              child: Column(
                mainAxisSize: MainAxisSize.min,
                children: [
                  const Text(
                    'Login',
                    style: TextStyle(
                      fontSize: 24.0,
                      fontWeight: FontWeight.bold,
                    ),
                  ),
                  const SizedBox(height: 30.0),
                  TextField(
                    controller: _usernameController,
                    decoration: const InputDecoration(
                      labelText: 'Username',
                      hintText: 'Enter your username',
                      border: OutlineInputBorder(
                        borderRadius: BorderRadius.all(Radius.circular(12.0)),
                      ),
                      contentPadding:
                          EdgeInsets.symmetric(horizontal: 12.0, vertical: 8.0),
                    ),
                  ),
                  const SizedBox(height: 12.0),
                  TextField(
                    controller: _passwordController,
                    decoration: const InputDecoration(
                      labelText: 'Password',
                      hintText: 'Enter your password',
                      border: OutlineInputBorder(
                        borderRadius: BorderRadius.all(Radius.circular(12.0)),
                      ),
                      contentPadding:
                          EdgeInsets.symmetric(horizontal: 12.0, vertical: 8.0),
                    ),
                    obscureText: true,
                  ),
                  const SizedBox(height: 24.0),
                  ElevatedButton(
                    onPressed: () async {
                      String username = _usernameController.text;
                      String password = _passwordController.text;

		  // Check credentials
		  // TODO: Change the URL and don't forget to add a trailing slash (/) at the end of the URL!
		  // To connect the Android emulator to Django on localhost,
		  // use the URL http://10.0.2.2/
                      final response = await request
                          .login("http://localhost:8000/auth/login/", {
                        'username': username,
                        'password': password,
                      });

                      if (request.loggedIn) {
                        String message = response['message'];
                        String uname = response['username'];
                        if (context.mounted) {
                          Navigator.pushReplacement(
                            context,
                            MaterialPageRoute(
                                builder: (context) => MyHomePage()),
                          );
                          ScaffoldMessenger.of(context)
                            ..hideCurrentSnackBar()
                            ..showSnackBar(
                              SnackBar(
                                  content:
                                      Text("$message Welcome, $uname.")),
                            );
                        }
                      } else {
                        if (context.mounted) {
                          showDialog(
                            context: context,
                            builder: (context) => AlertDialog(
                              title: const Text('Login Failed'),
                              content: Text(response['message']),
                              actions: [
                                TextButton(
                                  child: const Text('OK'),
                                  onPressed: () {
                                    Navigator.pop(context);
                                  },
                                ),
                              ],
                            ),
                          );
                        }
                      }
                    },
                    style: ElevatedButton.styleFrom(
                      foregroundColor: Colors.white,
                      minimumSize: Size(double.infinity, 50),
                      backgroundColor: Theme.of(context).colorScheme.primary,
                      padding: const EdgeInsets.symmetric(vertical: 16.0),
                    ),
                    child: const Text('Login'),
                  ),
                  const SizedBox(height: 36.0),
                  GestureDetector(
                    onTap: () {
                      Navigator.push(
                        context,
                        MaterialPageRoute(
                            builder: (context) => const RegisterPage()),
                      );
                    },
                    child: Text(
                      'Don\'t have an account? Register',
                      style: TextStyle(
                        color: Theme.of(context).colorScheme.primary,
                        fontSize: 16.0,
                      ),
                    ),
                  ),
                ],
              ),
            ),
          ),
        ),
      ),
    );
  }
}
```

add this in register.dart
```
class RegisterPage extends StatefulWidget {
  const RegisterPage({super.key});

  @override
  State<RegisterPage> createState() => _RegisterPageState();
}

class _RegisterPageState extends State<RegisterPage> {
  final _usernameController = TextEditingController();
  final _passwordController = TextEditingController();
  final _confirmPasswordController = TextEditingController();

  @override
  Widget build(BuildContext context) {
    final request = context.watch<CookieRequest>();
    return Scaffold(
      appBar: AppBar(
        title: const Text('Register'),
        leading: IconButton(
          icon: const Icon(Icons.arrow_back),
          onPressed: () {
            Navigator.pop(context);
          },
        ),
      ),
      body: Center(
        child: SingleChildScrollView(
          padding: const EdgeInsets.all(16.0),
          child: Card(
            elevation: 8,
            shape: RoundedRectangleBorder(
              borderRadius: BorderRadius.circular(12.0),
            ),
            child: Padding(
              padding: const EdgeInsets.all(20.0),
              child: Column(
                mainAxisSize: MainAxisSize.min,
                children: <Widget>[
                  const Text(
                    'Register',
                    style: TextStyle(
                      fontSize: 24.0,
                      fontWeight: FontWeight.bold,
                    ),
                  ),
                  const SizedBox(height: 30.0),
                  TextFormField(
                    controller: _usernameController,
                    decoration: const InputDecoration(
                      labelText: 'Username',
                      hintText: 'Enter your username',
                      border: OutlineInputBorder(
                        borderRadius: BorderRadius.all(Radius.circular(12.0)),
                      ),
                      contentPadding:
                          EdgeInsets.symmetric(horizontal: 12.0, vertical: 8.0),
                    ),
                    validator: (value) {
                      if (value == null || value.isEmpty) {
                        return 'Please enter your username';
                      }
                      return null;
                    },
                  ),
                  const SizedBox(height: 12.0),
                  TextFormField(
                    controller: _passwordController,
                    decoration: const InputDecoration(
                      labelText: 'Password',
                      hintText: 'Enter your password',
                      border: OutlineInputBorder(
                        borderRadius: BorderRadius.all(Radius.circular(12.0)),
                      ),
                      contentPadding:
                          EdgeInsets.symmetric(horizontal: 12.0, vertical: 8.0),
                    ),
                    obscureText: true,
                    validator: (value) {
                      if (value == null || value.isEmpty) {
                        return 'Please enter your password';
                      }
                      return null;
                    },
                  ),
                  const SizedBox(height: 12.0),
                  TextFormField(
                    controller: _confirmPasswordController,
                    decoration: const InputDecoration(
                      labelText: 'Confirm Password',
                      hintText: 'Confirm your password',
                      border: OutlineInputBorder(
                        borderRadius: BorderRadius.all(Radius.circular(12.0)),
                      ),
                      contentPadding:
                          EdgeInsets.symmetric(horizontal: 12.0, vertical: 8.0),
                    ),
                    obscureText: true,
                    validator: (value) {
                      if (value == null || value.isEmpty) {
                        return 'Please confirm your password';
                      }
                      return null;
                    },
                  ),
                  const SizedBox(height: 24.0),
                  ElevatedButton(
                    onPressed: () async {
                      String username = _usernameController.text;
                      String password1 = _passwordController.text;
                      String password2 = _confirmPasswordController.text;

                      // Check credentials
                      // TODO: Change the url, don't forget to add a slash (/) inthe end of the URL!
                      // To connect Android emulator with Django on localhost,
                      // use the URL http://10.0.2.2/
                      final response = await request.postJson(
                          "http://localhost:8000/auth/register/",
                          jsonEncode({
                            "username": username,
                            "password1": password1,
                            "password2": password2,
                          }));
                      if (context.mounted) {
                        if (response['status'] == 'success') {
                          ScaffoldMessenger.of(context).showSnackBar(
                            const SnackBar(
                              content: Text('Successfully registered!'),
                            ),
                          );
                          Navigator.pushReplacement(
                            context,
                            MaterialPageRoute(
                                builder: (context) => const LoginPage()),
                          );
                        } else {
                          ScaffoldMessenger.of(context).showSnackBar(
                            const SnackBar(
                              content: Text('Failed to register!'),
                            ),
                          );
                        }
                      }
                    },
                    style: ElevatedButton.styleFrom(
                      foregroundColor: Colors.white,
                      minimumSize: Size(double.infinity, 50),
                      backgroundColor: Theme.of(context).colorScheme.primary,
                      padding: const EdgeInsets.symmetric(vertical: 16.0),
                    ),
                    child: const Text('Register'),
                  ),
                ],
              ),
            ),
          ),
        ),
      ),
    );
  }
}
```

### Create a custom model according to your Django application project.

add this in models
```
// To parse this JSON data, do
//
//     final productEntry = productEntryFromJson(jsonString);

import 'dart:convert';

List<ProductEntry> productEntryFromJson(String str) => List<ProductEntry>.from(json.decode(str).map((x) => ProductEntry.fromJson(x)));

String productEntryToJson(List<ProductEntry> data) => json.encode(List<dynamic>.from(data.map((x) => x.toJson())));

class ProductEntry {
    String model;
    String pk;
    Fields fields;

    ProductEntry({
        required this.model,
        required this.pk,
        required this.fields,
    });

    factory ProductEntry.fromJson(Map<String, dynamic> json) => ProductEntry(
        model: json["model"],
        pk: json["pk"],
        fields: Fields.fromJson(json["fields"]),
    );

    Map<String, dynamic> toJson() => {
        "model": model,
        "pk": pk,
        "fields": fields.toJson(),
    };
}

class Fields {
    int user;
    String name;
    int price;
    String description;
    String rating;

    Fields({
        required this.user,
        required this.name,
        required this.price,
        required this.description,
        required this.rating,
    });

    factory Fields.fromJson(Map<String, dynamic> json) => Fields(
        user: json["user"],
        name: json["name"],
        price: json["price"],
        description: json["description"],
        rating: json["rating"],
    );

    Map<String, dynamic> toJson() => {
        "user": user,
        "name": name,
        "price": price,
        "description": description,
        "rating": rating,
    };
}

```

### Create a page containing a list of all items available at the JSON endpoint in Django that you have deployed.]

make list_product.dart in screens directory and populate with this

```
import 'package:flutter/material.dart';
import 'package:pbp_django_auth/pbp_django_auth.dart';
import 'package:provider/provider.dart';
import 'package:vin_shop/models/product_entry.dart';
import 'package:vin_shop/screens/product_detail.dart';

import 'package:vin_shop/widgets/left_drawer.dart';

class ProductEntryPage extends StatefulWidget {
  const ProductEntryPage({super.key});

  @override
  State<ProductEntryPage> createState() => _ProductEntryPageState();
}

class _ProductEntryPageState extends State<ProductEntryPage> {
  Future<List<ProductEntry>> fetchProduct(CookieRequest request) async {
    // TODO: Don't forget to add the trailing slash (/) at the end of the URL!
    final response = await request.get('http://localhost:8000/json/');
    
    // Decoding the response into JSON
    var data = response;
    
    // Convert json data to a MoodEntry object
    List<ProductEntry> listProduct = [];
    for (var d in data) {
      if (d != null) {
        listProduct.add(ProductEntry.fromJson(d));
      }
    }
    return listProduct;
  }
  
  @override
  Widget build(BuildContext context) {
    final request = context.watch<CookieRequest>();
    return Scaffold(
      appBar: AppBar(
        title: const Text('Product Entry List'),
      ),
      drawer: const LeftDrawer(),
      body: FutureBuilder(
        future: fetchProduct(request),
        builder: (context, AsyncSnapshot snapshot) {
          if (snapshot.data == null) {
            return const Center(child: CircularProgressIndicator());
          } else {
            if (!snapshot.hasData) {
              return const Column(
                children: [
                  Text(
                    'There is no product data in mental health tracker.',
                    style: TextStyle(fontSize: 20, color: Color(0xff59A5D8)),
                  ),
                  SizedBox(height: 8),
                ],
              );
            } else {
              return ListView.builder(
                itemCount: snapshot.data!.length,
                itemBuilder: (_, index) {
                  var product = snapshot.data![index];
                  return GestureDetector(
                    onTap: () {
                      Navigator.push(
                        context,
                        MaterialPageRoute(
                          builder: (context) => ProductDetail(product: product),
                        ),
                      );
                    },
                    child: Container(
                      margin: const EdgeInsets.symmetric(horizontal: 16, vertical: 12),
                      padding: const EdgeInsets.all(20.0),
                      decoration: BoxDecoration(
                        color: Colors.white,
                        borderRadius: BorderRadius.circular(8.0),
                        boxShadow: [
                          BoxShadow(
                            color: Colors.grey.withOpacity(0.2),
                            spreadRadius: 2,
                            blurRadius: 5,
                          ),
                        ],
                      ),
                      child: Column(
                        crossAxisAlignment: CrossAxisAlignment.start,
                        children: [
                          Text(
                            product.fields.name,
                            style: const TextStyle(
                              fontSize: 18.0,
                              fontWeight: FontWeight.bold,
                            ),
                          ),
                          const SizedBox(height: 10),
                          Text("Price: \$${product.fields.price}"),
                          const SizedBox(height: 10),
                          Text("Rating: ${product.fields.rating}"),
                        ],
                      ),
                    ),
                  );
                },
              );

            }
          }
        },
      ),
    );
  }
}
```

### Create a detail page for each item listed on the Product list page.
add this in detail page

```
import 'package:flutter/material.dart';
import 'package:vin_shop/models/product_entry.dart';

class ProductDetail extends StatelessWidget {
  final ProductEntry product;

  const ProductDetail({Key? key, required this.product}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(product.fields.name),
      ),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Text(
              product.fields.name,
              style: const TextStyle(fontSize: 24, fontWeight: FontWeight.bold),
            ),
            const SizedBox(height: 10),
            Text("Price: \$${product.fields.price}"),
            const SizedBox(height: 10),
            Text("Description: ${product.fields.description}"),
            const SizedBox(height: 10),
            Text("Rating: ${product.fields.rating}"),
            const SizedBox(height: 20),
            ElevatedButton(
              onPressed: () {
                Navigator.pop(context);
              },
              child: const Text('Back to Product List'),
            ),
          ],
        ),
      ),
    );
  }
}

```

### Filter the item list page to display only items associated with the currently logged-in user.

add this in django
```
def create_product_entry(request):
    form = ProductForm(request.POST or None)

    if form.is_valid() and request.method == "POST":
        product_entry = form.save(commit=False)
        product_entry.user = request.user
        product_entry.save()
        return redirect('main:show_main')

    context = {'form': form}
    return render(request, "create_product_entry.html", context)
```
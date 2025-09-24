author: Flutter Developer
summary: Learn how to build a complete Flutter app with bottom navigation, organized into separate files for better code management. Perfect for beginners!
id: flutter-bottom-navigation-codelab
categories: codelab,flutter,mobile-development
environments: Web
status: Published
feedback link: https://github.com/your-repo
analytics account: Google Analytics ID

# Building Flutter Bottom Navigation with Organized File Structure

## Overview
Duration: 0:02:00

Welcome to your Flutter bottom navigation tutorial! In this codelab, we'll build a complete app with bottom navigation, organized into separate files for better code management.

### What We're Making
A complete app with bottom navigation, but organized into separate files for easier management:

* 5 different pages (Home, About, Projects, Gallery, Contact)
* Bottom navigation bar to switch between pages
* Organized file structure for better code management
* Professional UI with cards, lists, and grids

### File Structure
```
lib/
├── main.dart                 (Main app entry point)
├── navigation.dart           (Bottom navigation controller)
└── pages/
    ├── home_page.dart       (Homepage content)
    ├── about_page.dart      (About me page)
    ├── projects_page.dart   (My projects page)
    ├── gallery_page.dart    (Gallery page)
    └── contact_page.dart    (Contact me page)
```

### What you'll learn
* How to organize Flutter code into separate files
* How to create bottom navigation with PageView
* How to build different types of pages (lists, grids, cards)
* How to create data models and reusable components
* How to manage state in navigation

### Prerequisites
* Basic understanding of programming concepts
* Flutter SDK installed on your machine
* An IDE like VS Code or Android Studio with Flutter extensions

## Step 1: Set up the Basic App Structure
Duration: 0:04:00

What we're doing: Creating the main app entry point - this is where our app starts and sets up the basic configuration.

### Create a new Flutter project
First, create a new Flutter project:

```bash
flutter create my_portfolio_app
cd my_portfolio_app
```

### Create the main.dart file
Replace the contents of `lib/main.dart` with the following code:

```dart
import 'package:flutter/material.dart';
import 'navigation.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'My Portfolio App',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: MainNavigationPage(),
    );
  }
}
```

### Why this syntax:
* `import 'navigation.dart';` - We import our navigation file that we'll create next
* `MaterialApp` - This creates our app with Material Design styling and themes
* `theme: ThemeData()` - This sets up the app's color scheme and visual properties
* `primarySwatch: Colors.blue` - This creates a blue color palette for the entire app
* `visualDensity: VisualDensity.adaptivePlatformDensity` - This makes the UI adapt to different screen densities
* `home: MainNavigationPage()` - This sets our navigation page as the main screen

**Expected Output:** App structure ready, but we need to create the other files.

## Step 2: Create the Navigation Controller
Duration: 0:06:00

What we're doing: Creating the navigation system that manages all pages - this handles switching between different screens.

### Create the navigation.dart file
Create a new file `lib/navigation.dart` with the following code:

```dart
import 'package:flutter/material.dart';
import 'pages/home_page.dart';
import 'pages/about_page.dart';
import 'pages/projects_page.dart';
import 'pages/gallery_page.dart';
import 'pages/contact_page.dart';

class MainNavigationPage extends StatefulWidget {
  @override
  _MainNavigationPageState createState() => _MainNavigationPageState();
}

class _MainNavigationPageState extends State<MainNavigationPage> {
  int _selectedIndex = 2; // Start with Homepage (center tab)
  PageController _pageController = PageController(initialPage: 2);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: PageView(
        controller: _pageController,
        children: [
          AboutPage(),
          ProjectsPage(),
          HomePage(),
          GalleryPage(),
          ContactPage(),
        ],
        onPageChanged: (index) {
          setState(() {
            _selectedIndex = index;
          });
        },
      ),
      bottomNavigationBar: BottomNavigationBar(
        type: BottomNavigationBarType.fixed,
        currentIndex: _selectedIndex,
        onTap: _onTabTapped,
        selectedItemColor: Colors.blue,
        unselectedItemColor: Colors.grey,
        elevation: 8.0,
        backgroundColor: Colors.white,
        items: [
          BottomNavigationBarItem(icon: Icon(Icons.person), label: 'About Me'),
          BottomNavigationBarItem(icon: Icon(Icons.work), label: 'Projects'),
          BottomNavigationBarItem(icon: Icon(Icons.home), label: 'Home'),
          BottomNavigationBarItem(icon: Icon(Icons.photo_library), label: 'Gallery'),
          BottomNavigationBarItem(icon: Icon(Icons.contact_mail), label: 'Contact'),
        ],
      ),
    );
  }

  void _onTabTapped(int index) {
    setState(() {
      _selectedIndex = index;
    });
    _pageController.animateToPage(
      index,
      duration: Duration(milliseconds: 300),
      curve: Curves.easeInOut,
    );
  }

  @override
  void dispose() {
    _pageController.dispose();
    super.dispose();
  }
}
```

### Key Concepts Explained:
* `StatefulWidget` - A widget that can change over time (needed for navigation state)
* `PageController` - Controls which page is currently visible in PageView
* `PageView` - A scrollable widget that displays pages horizontally
* `BottomNavigationBar` - The bottom navigation bar with tabs
* `setState()` - Tells Flutter to rebuild the widget when state changes
* `animateToPage()` - Smoothly animates to a specific page
* `dispose()` - Cleans up resources when the widget is destroyed

**Expected Output:** Navigation structure ready, but we need to create the individual page files.

## Step 3: Create the Homepage
Duration: 0:04:00

What we're doing: Creating the homepage content - this is the main landing page of our app.

### Create the pages directory and home_page.dart
First, create the pages directory:

```bash
mkdir lib/pages
```

Create `lib/pages/home_page.dart`:

```dart
import 'package:flutter/material.dart';

class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Welcome Home'),
        backgroundColor: Colors.blue,
        centerTitle: true,
      ),
      body: Center(
        child: Padding(
          padding: EdgeInsets.all(20.0),
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              // Main welcome icon
              Container(
                padding: EdgeInsets.all(20),
                decoration: BoxDecoration(
                  color: Colors.blue.withOpacity(0.1),
                  borderRadius: BorderRadius.circular(50),
                ),
                child: Icon(Icons.home, size: 100, color: Colors.blue),
              ),
              SizedBox(height: 30),
              
              // Welcome title
              Text(
                'Welcome to My Portfolio!',
                style: TextStyle(
                  fontSize: 28,
                  fontWeight: FontWeight.bold,
                  color: Colors.black87,
                ),
                textAlign: TextAlign.center,
              ),
              SizedBox(height: 15),
              
              // Subtitle
              Text(
                'Explore my work and get to know me better',
                style: TextStyle(fontSize: 16, color: Colors.grey[600]),
                textAlign: TextAlign.center,
              ),
              SizedBox(height: 30),
              
              // Quick navigation cards
              Row(
                mainAxisAlignment: MainAxisAlignment.spaceEvenly,
                children: [
                  _buildQuickNavCard(Icons.person, 'About', Colors.green),
                  _buildQuickNavCard(Icons.work, 'Projects', Colors.orange),
                  _buildQuickNavCard(Icons.contact_mail, 'Contact', Colors.purple),
                ],
              ),
            ],
          ),
        ),
      ),
    );
  }

  Widget _buildQuickNavCard(IconData icon, String label, Color color) {
    return Container(
      padding: EdgeInsets.all(16),
      decoration: BoxDecoration(
        color: color.withOpacity(0.1),
        borderRadius: BorderRadius.circular(12),
      ),
      child: Column(
        children: [
          Icon(icon, size: 30, color: color),
          SizedBox(height: 8),
          Text(label, style: TextStyle(fontSize: 12, fontWeight: FontWeight.bold, color: color)),
        ],
      ),
    );
  }
}
```

### Key Concepts Explained:
* `StatelessWidget` - A widget that doesn't change over time (static content)
* `withOpacity(0.1)` - Makes a color semi-transparent (10% opacity)
* `BorderRadius.circular()` - Creates rounded corners
* `MainAxisAlignment.spaceEvenly` - Distributes space evenly between children
* `_buildQuickNavCard()` - A helper method to create reusable UI components
* `IconData` - A data type for Material Design icons

**Expected Output:** Beautiful homepage with welcome message and quick navigation cards.

## Step 4: Create the About Page
Duration: 0:04:00

What we're doing: Creating the about me page - this displays personal information and profile details.

### Create about_page.dart
Create `lib/pages/about_page.dart`:

```dart
import 'package:flutter/material.dart';

class AboutPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('About Me'),
        backgroundColor: Colors.blue,
        centerTitle: true,
      ),
      body: SingleChildScrollView(
        child: Padding(
          padding: EdgeInsets.all(20.0),
          child: Column(
            children: [
              SizedBox(height: 20),
              
              // Profile picture
              Container(
                width: 150,
                height: 150,
                decoration: BoxDecoration(
                  shape: BoxShape.circle,
                  border: Border.all(color: Colors.blue, width: 4),
                  boxShadow: [
                    BoxShadow(
                      color: Colors.black26,
                      blurRadius: 10,
                      offset: Offset(0, 5),
                    ),
                  ],
                ),
                child: ClipOval(
                  child: Image.network(
                    'https://picsum.photos/300/300?random=1',
                    fit: BoxFit.cover,
                  ),
                ),
              ),
              SizedBox(height: 25),
              
              // Name and title
              Text('Alex Johnson', style: TextStyle(fontSize: 28, fontWeight: FontWeight.bold, color: Colors.black87)),
              SizedBox(height: 8),
              Text('Flutter Developer', style: TextStyle(fontSize: 18, color: Colors.blue, fontWeight: FontWeight.w500)),
              SizedBox(height: 30),
              
              // About me card
              Container(
                padding: EdgeInsets.all(20),
                decoration: BoxDecoration(
                  color: Colors.white,
                  borderRadius: BorderRadius.circular(15),
                  boxShadow: [
                    BoxShadow(color: Colors.black12, blurRadius: 8, offset: Offset(0, 3)),
                  ],
                ),
                child: Column(
                  crossAxisAlignment: CrossAxisAlignment.start,
                  children: [
                    Text('About Me', style: TextStyle(fontSize: 20, fontWeight: FontWeight.bold, color: Colors.blue)),
                    SizedBox(height: 15),
                    Text(
                      'Hello! I\'m Alex, a passionate Flutter developer who loves creating beautiful and functional mobile applications. I enjoy turning complex problems into simple, beautiful designs.\n\nWhen I\'m not coding, you can find me exploring new technologies, reading tech blogs, or enjoying a good cup of coffee.',
                      style: TextStyle(fontSize: 16, color: Colors.grey[700], height: 1.6),
                    ),
                  ],
                ),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

### Key Concepts Explained:
* `SingleChildScrollView` - Makes content scrollable when it exceeds screen height
* `BoxShape.circle` - Creates a circular shape for the container
* `ClipOval` - Clips the image into a perfect circle
* `BoxShadow` - Adds shadow effects for depth and visual appeal
* `CrossAxisAlignment.start` - Aligns children to the left side
* `height: 1.6` - Sets line spacing for better text readability

**Expected Output:** Professional about page with circular profile image and detailed description.

## Step 5: Create the Projects Page
Duration: 0:06:00

What we're doing: Creating the projects showcase - this displays a list of projects with detailed information.

### Create projects_page.dart
Create `lib/pages/projects_page.dart`:

```dart
import 'package:flutter/material.dart';

class ProjectsPage extends StatelessWidget {
  final List<Project> projects = [
    Project(title: 'Weather App', description: 'A beautiful weather forecasting app with real-time updates', icon: Icons.cloud, color: Colors.blue),
    Project(title: 'Todo List', description: 'Task management made simple with intuitive design', icon: Icons.check_box, color: Colors.green),
    Project(title: 'Recipe Finder', description: 'Discover amazing recipes from around the world', icon: Icons.restaurant, color: Colors.orange),
    Project(title: 'Chat App', description: 'Real-time messaging with modern UI/UX', icon: Icons.chat, color: Colors.purple),
  ];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('My Projects'),
        backgroundColor: Colors.blue,
        centerTitle: true,
      ),
      body: ListView.builder(
        padding: EdgeInsets.all(16.0),
        itemCount: projects.length,
        itemBuilder: (context, index) {
          return _buildProjectCard(projects[index]);
        },
      ),
    );
  }

  Widget _buildProjectCard(Project project) {
    return Container(
      margin: EdgeInsets.only(bottom: 16.0),
      child: Card(
        elevation: 4,
        shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(12)),
        child: Padding(
          padding: EdgeInsets.all(16.0),
          child: Row(
            children: [
              // Project icon
              Container(
                padding: EdgeInsets.all(12),
                decoration: BoxDecoration(
                  color: project.color.withOpacity(0.1),
                  borderRadius: BorderRadius.circular(10),
                ),
                child: Icon(project.icon, size: 30, color: project.color),
              ),
              SizedBox(width: 16),
              
              // Project details
              Expanded(
                child: Column(
                  crossAxisAlignment: CrossAxisAlignment.start,
                  children: [
                    Text(project.title, style: TextStyle(fontSize: 18, fontWeight: FontWeight.bold, color: Colors.black87)),
                    SizedBox(height: 4),
                    Text(project.description, style: TextStyle(fontSize: 14, color: Colors.grey[600])),
                  ],
                ),
              ),
              
              // Arrow icon
              Icon(Icons.arrow_forward_ios, color: Colors.grey[400], size: 16),
            ],
          ),
        ),
      ),
    );
  }
}

// Project data model
class Project {
  final String title;
  final String description;
  final IconData icon;
  final Color color;

  Project({
    required this.title,
    required this.description,
    required this.icon,
    required this.color,
  });
}
```

### Key Concepts Explained:
* `ListView.builder` - Efficiently builds a scrollable list of items (only creates visible items)
* `itemCount` - Tells the ListView how many items to display
* `itemBuilder` - Function that creates each list item (called for each visible item)
* `Card` - Material Design card widget with elevation and rounded corners
* `RoundedRectangleBorder` - Creates rounded rectangle borders for widgets
* `Expanded` - Takes up remaining space in a Row or Column
* `Data Model (Project class)` - Custom class to structure project data
* `required` - Makes parameters mandatory when creating an instance
* `final` - Makes variables immutable (cannot be changed after assignment)

### Where ListView.builder is commonly used:
* Social media feeds (posts, comments)
* Product catalogs in e-commerce apps
* Search results lists
* Settings pages with multiple options
* Chat message lists
* Any scrollable list with dynamic content

**Expected Output:** Organized project list with colorful icons and descriptions.

## Step 6: Create the Gallery Page
Duration: 0:04:00

What we're doing: Creating the image gallery - this displays images in a grid layout.

### Create gallery_page.dart
Create `lib/pages/gallery_page.dart`:

```dart
import 'package:flutter/material.dart';

class GalleryPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Gallery'),
        backgroundColor: Colors.blue,
        centerTitle: true,
      ),
      body: Padding(
        padding: EdgeInsets.all(8.0),
        child: GridView.builder(
          gridDelegate: SliverGridDelegateWithFixedCrossAxisCount(
            crossAxisCount: 2,
            crossAxisSpacing: 8.0,
            mainAxisSpacing: 8.0,
            childAspectRatio: 1.0,
          ),
          itemCount: 12,
          itemBuilder: (context, index) {
            return _buildGalleryItem(index);
          },
        ),
      ),
    );
  }

  Widget _buildGalleryItem(int index) {
    return Container(
      decoration: BoxDecoration(
        borderRadius: BorderRadius.circular(12),
        boxShadow: [
          BoxShadow(
            color: Colors.black26,
            blurRadius: 4,
            offset: Offset(0, 2),
          ),
        ],
      ),
      child: ClipRRect(
        borderRadius: BorderRadius.circular(12),
        child: Stack(
          fit: StackFit.expand,
          children: [
            Image.network(
              'https://picsum.photos/400/400?random=${index + 10}',
              fit: BoxFit.cover,
            ),
            // Gradient overlay
            Container(
              decoration: BoxDecoration(
                gradient: LinearGradient(
                  begin: Alignment.topCenter,
                  end: Alignment.bottomCenter,
                  colors: [
                    Colors.transparent,
                    Colors.black.withOpacity(0.3),
                  ],
                ),
              ),
            ),
            // Image number
            Positioned(
              bottom: 8,
              right: 8,
              child: Container(
                padding: EdgeInsets.symmetric(horizontal: 8, vertical: 4),
                decoration: BoxDecoration(
                  color: Colors.white.withOpacity(0.8),
                  borderRadius: BorderRadius.circular(12),
                ),
                child: Text(
                  '${index + 1}',
                  style: TextStyle(fontSize: 12, fontWeight: FontWeight.bold, color: Colors.black87),
                ),
              ),
            ),
          ],
        ),
      ),
    );
  }
}
```

### Key Concepts Explained:
* `GridView.builder` - Creates a scrollable grid of widgets (only creates visible items)
* `SliverGridDelegateWithFixedCrossAxisCount` - Defines grid layout with fixed number of columns
* `crossAxisCount: 2` - Sets number of columns in the grid
* `crossAxisSpacing` - Space between columns
* `mainAxisSpacing` - Space between rows
* `childAspectRatio: 1.0` - Makes grid items square (width = height)
* `Stack` - Overlays widgets on top of each other
* `StackFit.expand` - Makes all children fill the entire stack
* `LinearGradient` - Creates a gradient from one color to another
* `Positioned` - Positions a child widget at specific coordinates in a Stack
* `EdgeInsets.symmetric()` - Creates padding with same horizontal and vertical values

### Where GridView.builder is commonly used:
* Photo galleries and image grids
* Product catalogs in e-commerce
* Icon grids in settings pages
* Dashboard widgets
* Social media post grids
* Any grid-based layout with multiple items

**Expected Output:** Beautiful 2-column grid gallery with rounded corners and image numbers.

## Step 7: Create the Contact Page
Duration: 0:04:00

What we're doing: Creating the contact information page - this displays contact details in an organized way.

### Create contact_page.dart
Create `lib/pages/contact_page.dart`:

```dart
import 'package:flutter/material.dart';

class ContactPage extends StatelessWidget {
  final List<ContactInfo> contactItems = [
    ContactInfo(Icons.email, 'Email', 'alex@example.com', Colors.red),
    ContactInfo(Icons.phone, 'Phone', '+1 234 567 8900', Colors.green),
    ContactInfo(Icons.location_on, 'Location', 'San Francisco, CA', Colors.blue),
    ContactInfo(Icons.language, 'Website', 'www.alexjohnson.dev', Colors.purple),
  ];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Contact Me'),
        backgroundColor: Colors.blue,
        centerTitle: true,
      ),
      body: SingleChildScrollView(
        child: Padding(
          padding: EdgeInsets.all(20.0),
          child: Column(
            children: [
              SizedBox(height: 20),
              
              // Contact header
              Container(
                padding: EdgeInsets.all(20),
                child: Column(
                  children: [
                    Icon(Icons.contact_mail, size: 80, color: Colors.blue),
                    SizedBox(height: 20),
                    Text('Get In Touch', style: TextStyle(fontSize: 28, fontWeight: FontWeight.bold, color: Colors.black87)),
                    SizedBox(height: 10),
                    Text('Feel free to reach out to me through any of these channels', style: TextStyle(fontSize: 16, color: Colors.grey[600]), textAlign: TextAlign.center),
                  ],
                ),
              ),
              
              SizedBox(height: 20),
              
              // Contact items
              ...contactItems.map((item) => _buildContactItem(item)).toList(),
            ],
          ),
        ),
      ),
    );
  }

  Widget _buildContactItem(ContactInfo info) {
    return Container(
      margin: EdgeInsets.only(bottom: 16.0),
      padding: EdgeInsets.all(16.0),
      decoration: BoxDecoration(
        color: Colors.white,
        borderRadius: BorderRadius.circular(12),
        boxShadow: [BoxShadow(color: Colors.black12, blurRadius: 4, offset: Offset(0, 2))],
      ),
      child: Row(
        children: [
          // Icon container
          Container(
            padding: EdgeInsets.all(12),
            decoration: BoxDecoration(
              color: info.color.withOpacity(0.1),
              borderRadius: BorderRadius.circular(10),
            ),
            child: Icon(info.icon, color: info.color, size: 24),
          ),
          SizedBox(width: 16),
          
          // Contact details
          Expanded(
            child: Column(
              crossAxisAlignment: CrossAxisAlignment.start,
              children: [
                Text(info.title, style: TextStyle(fontSize: 16, fontWeight: FontWeight.bold, color: Colors.black87)),
                SizedBox(height: 4),
                Text(info.value, style: TextStyle(fontSize: 14, color: Colors.grey[600])),
              ],
            ),
          ),
        ],
      ),
    );
  }
}

// Contact info data model
class ContactInfo {
  final IconData icon;
  final String title;
  final String value;
  final Color color;

  ContactInfo(this.icon, this.title, this.value, this.color);
}
```

### Key Concepts Explained:
* `...contactItems.map()` - Spread operator that expands a list of widgets
* `map()` - Transforms each item in a list to a new item
* `toList()` - Converts the mapped result back to a list
* `EdgeInsets.only()` - Creates padding with specific sides only
* `Constructor shorthand` - ContactInfo(this.icon, this.title, this.value, this.color) is shorthand for a constructor that assigns parameters to instance variables

### Where the spread operator (...) is commonly used:
* Combining multiple lists into one
* Adding multiple widgets to a Column or Row
* Merging arrays in data processing
* Creating dynamic widget lists from data
* Passing multiple arguments to functions

**Expected Output:** Clean contact page with colorful contact cards.

## How to Run This Organized App
Duration: 0:02:00

### Complete Setup Instructions
Now that you have all the files, here's how to run your organized app:

1. Make sure all files are created in the correct locations
2. Run the app:

```bash
flutter run
```

### Benefits of This File Structure
* ✅ **Easy to Maintain:** Each page is in its own file
* ✅ **Team Friendly:** Different developers can work on different pages
* ✅ **Reusable:** Pages can be imported into other projects
* ✅ **Organized:** Clear separation of concerns
* ✅ **Scalable:** Easy to add more pages or features

## What You've Learned
Duration: 0:02:00

### Key Flutter Concepts
* **File organization:** Separating code into logical files for better maintainability
* **Import/Export:** How to use code from different files
* **Data models:** Creating custom classes for structured data
* **Modular design:** Building reusable components
* **Clean architecture:** Separating navigation from page content
* **ListView.builder:** Efficient list creation for dynamic content
* **GridView.builder:** Grid layout for organized content display
* **State management:** Managing navigation state with StatefulWidget

### Congratulations! 🎉
You now have a well-organized, professional Flutter app with bottom navigation! You've learned how to structure code properly and create different types of pages.

### Next Steps
* Add more interactive features like navigation between pages
* Implement state management solutions like Provider or Bloc
* Add animations and transitions
* Create more complex data models
* Build custom widgets for reusable components

### Resources
* [Flutter Documentation](https://flutter.dev/docs)
* [Flutter Codelabs](https://docs.flutter.dev/codelabs)
* [Flutter Package Repository](https://pub.dev)
* [Flutter Community](https://flutter.dev/community)







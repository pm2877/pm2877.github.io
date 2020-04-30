---
layout: single
title:  "Android Development Basics"
date:   2018-01-17 03:20:06 -0500
categories: Tech
toc: true
toc_label: "On this page"
toc_icon: "list"
excerpt: "Notes taken during 'Grow with Google - Android Development course' on Udacity"
---
***Notes taken during Grow with google Android Dev course on Udacity***

{:toc}

## General Notes

1. Important project settings can be found in File —> Project Structure —> app —> flavors

2. **HAXM** is the kernel driver used for hardware virtualization by AVDs on Windows and Mac

   

## Lesson 2

### What happens when you hit run in Android Studio?

When you hit run in Android studio, first the code is compiled into byte code that can be run in the run time on the device. Gradle builds this code and packages this byte code along with the application's resources into an **android application package** (.apk) file (apk is a specialized zip format). Android studio then signs it and pushes it to the device using the android debug bridge (adb).

### What is Gradle?

Gradle is the build system of choice for Android Studio. Because of that, there's various functionality available within the platform. When you make a project, there are a few gradle build scripts automatically generated for you. Gradle scripts are also run before running the project, if anything has changed since the last build. A gradle task represents a single, atomic piece of work for a build.

### Components

An Android Application is a collection of components that interact with each other. There are 4 types of components that make up an app:

- Activity - window that your app uses to receive events from the system
- Service
- Content Providers
- Broadcast Receivers

<u>Android knows about each of these because they are registered in the **android manifest.**</u>

### Activity

- An activity is a single focused thing that the user can do. Activities are responsible for creating the window that your application uses to draw and receive events from the system.
- From the user's perspective, an application is a series of linked activities, starting from the one that is started from the launcher.
- An activity is registered with the launcher by specifying an intent filter in the application —> activity tag in the android manifest file.
- An activity creates views to show the user information, and to let the user interact with the activity. An activity determines what views to create (and where to put them), by reading an XML layout file. `setContentView(R.layout.activity_main)` **causes the XML layout to be inflated, converting everything in the XML file to a heirarchy of view objects in memory.**

### Views

- Views are a class in the Android UI framework. They occupy a rectangular area on the screen and are responsible for drawing and handling events.

- There are two major categories of views: UI Components and Container Views.

- Examples of Container Views:

  ![containerView Examples](/images/containerViews.png)

### How do the XML Layouts relate to the Java Activites?

After you create your XML Layout you need to associate it with your activity. This is done in the onCreate method of the Activity using the method setContentView. You pass a reference to the layout file as R.layout.name_of_layout

### The R Class

When your application is compiled the R class is generated. It creates constants that allow you to dynamically identify the various contents of the res folder, including layouts.

### setContentView()

So what is the setContentView method doing? It inflates the layout. Essentially what happens is that Android reads your XML file and generates Java objects for each of the tags in your layout file. You can then edit these objects in the Java code by calling methods on the Java objects.

### Responsive Design

The android UI needs to scale to different resolutions and device widths used by various devices. FrameLayout, ConstraintLayout and LinearLayout are the 3 basic layouts we should be using. Always use the simplest layout that gets the job done.

- FrameLayout: use for simple layouts when we have only one child view. (example a list view which would fill the entire screen content area)
- LinearLayout: use for stacking views horizontally or vertically against each other, and to break up the display proporationally between them.
- ConstraintLayout: This is a more complicated, but a very powerful layout. We can position each child view relative to the parent or relative to each other.


### ConstraintLayout Basics

Useful links: 

[google codelabs](https://codelabs.developers.google.com/codelabs/constraint-layout/#8)

[building responsive UI with constraint layout](https://developer.android.com/training/constraint-layout/index.html)

#### a. Use a baseline constraint

By using a baseline constraint, you can vertically align elements that have text, such as a TextView, EditText, or Button, so that the text baselines are aligned. Use baseline constraints to align elements that use different text sizes. Baseline constraints are also useful for aligning the text baselines of elements of different sizes.  Click the **ab** button to show the text baseline. Then click and drag from the TextView's baseline, which is blinking in green, to the baseline of the `Plain Text` element, as shown in the following animated figure

#### b. The Infer Constraints tool

The Infer Constraints tool *infers*, or figures out, the constraints you need to match a rough layout of elements. It works by taking into account the positions and sizes of the elements. Drag elements to the layout in the positions you want them, and use the Infer Constraints tool to automatically create the constraint connections.

##### - What's the difference between Inference and Autoconnect?

The Infer Constraints ![img](https://codelabs.developers.google.com/codelabs/constraint-layout/img/762af6efa02c9471.png) tool calculates and sets constraints for *all* of the elements in a layout, rather than just the selected element. It bases its calculations on inferred relationships between the elements.The Autoconnect ![img](https://codelabs.developers.google.com/codelabs/constraint-layout/img/dd3846009e393c48.png) tool creates constraint connections for a selected element to the element's parent.

#### c. Use ratios to size elements

You can quickly resize elements by aspect ratio if at least one of the element's dimensions is set to match constraints.

#### d. Constrain to a guideline

You can add a vertical or horizontal guideline to which you can constrain views, and the guideline will be invisible to app users. You can position the guideline within the layout based on either dp units or percent, relative to the layout's edge.

To create a guideline, click **Guidelines** in the toolbar, and then click either **Add Vertical Guideline** or **Add Horizontal Guideline**.

Drag the dotted line to reposition it and click the circle at the edge of the guideline to toggle the measurement mode.

#### e. Use barriers to align elements that dynamically vary in size

Barriers allow you to specify a constraint based on multiple UI elements. You'll want to use barriers any time that multiple elements could dynamically change their size based on user input or language.

The `barrierDirection` is an attribute that controls how the barrier is positioned relative to the referenced views.

*A constraint to a barrier is just like a constraint to another element. However, users don't see barriers, and barriers don't add a level to the app's view hierarchy, which means they don't affect performance.*

#### f. Use chains to position multiple elements

A *chain* is a group of elements that are linked to each other with bi-directional position constraints. When you create a chain, you can position all of the elements as a group. For example, you can center all of your chained elements as if they were a single element. Some chain modes:

- Packed: The elements are packed together, as shown above.
- Spread: The elements are spread out over the available space.
- Spread inside: Similar to Spread, but the endpoints of the chain are not spread out.




## Lesson 3

### Logging

A good practice is to have the class name as the TAG in logs.

<u>Log levels</u>: *WTF*, ERROR, WARN, INFO, DEBUG, VERBOSE


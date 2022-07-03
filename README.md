

# SustrainableWorkshop

**Group work**: 2-3 elements.
**Duration**: 90 mins.

## Installation / Setup


### 1. Requirements:
- Linux / Mac OS pc/workstation. 
- Python >= 3.6;
- Java >= 8;
- Android Studio IDE (and consequently, Android SDK);
- 1 Android device;
- E-Manafa profiler;
- Demo Android application;
- BasiC Java / OOP knowledge.



### 2. Android device setup
 You will need an Android device (at least one per group) to do all the exercises proposed in this workshop. You can use your personal Android device since the software that will be executed does not deal with or extracts any sensitive information and is completely open-source. It only extracts battery-related metrics that are obtained during the exercises. In order to activate the developer features on your Android device and establish a communication channel with your PC, you need to activate the developer's options in your device's settings. The procedure for enabling the necessary settings differs slightly between vendors and platform versions.
 The process can be performed by following these steps:
 
 1. Go to "Settings", then tap "About device" or "About phone". Scroll down, then tap "Build number" seven times. Depending on your device and operating system, you may need to tap "Software information", then tap "Build number" seven times. 3 Enter your pattern, PIN or password to enable the Developer options menu. This process will give you access to a wide set of features that are available in **Settings** -> **Developer Options**.
 2. Go to these settings and enable the following features: **USB debugging** and **Install via USB**.
 3. Increase the **Logger Buffer Size** to at least 4MB.
 
### 3.  Computer setup

You also going to need a *Nix OS with Android Studio and Android SDK 30 (Android 10) (it can be selected during the Android Studio installation process). The rest of the installation process can be performed by following these steps: 
1. **Install Android Studio IDE:** Go to the [Android Studio Web Page](https://developer.android.com/studio),  download the latest stable version, and follow the installation instructions. 
2. **Install E-Manafa Profiler:**  `pip install manafa`
3. Clone Android application: `git clone https://github.com/greensoftwarelab/SampleAndroidApp.git`
4. Finally, open the app on the Android Studio IDE and try to execute it on your device (Click on run), connected via USB to your computer. If the application main screen appears on your Android device, everything worked as supposed.
5. Try to execute E-Manafa with your device (once again, connected via USB). Try to replicate the process illustrated in this [demo video](https://www.youtube.com/watch?v=vklLgv2_iNo). if everything works like in the video, you are ready to go.  Note: If the installation process or the commands fails, try executing E-Manafa by especifying the full path of the executable (something like `python3 /usr/local/lib/python3.9/site-packages/manafa/main.py`) or from the [sources](https://greensoftwarelab.github.io/e-manafa).


## Exercise I: Black-Box testing

 In this exercise, we intend to see potentially interesting results that can be gathered from the dynamic execution of the proposed procedure in different devices and setups. In this procedure, it is intended to use some of the previously installed tools to measure the energy consumption associated with sending instant messages using real-world applications. In order to be able to estimate the energy of this task, we need  the following toolset:
	- An instant messaging application (WhatsApp, Facebook Messenger, Google Chat, Telegram, Slack, etc);
	- A tool capable of estimating the energy consumption of a task or system during its execution (E-Manafa);
	- A set of guidelines to avoid interference in the measurements: Close other apps, disable notifications, turn off unused sensors and hardware components, mute notifications, etc.

Furthermore, in order to estimate the energy consumed by the process, follow the following steps:
	
1. Select one of the suggested messaging apps. Monitor the consumption of sending a message to a random subject (preferably, a subject that unlikely will see the message and respond to it during the execution of the process). The testing process must include the step of opening the application from the menu, selecting a receiver, and sending the following message, typed using your default keyboard: ”Hi. Please ignore this message. I'm participating in an empirical study aiming to analyze the energy performance of instant messaging apps”. To monitor the energy consumption of the process, invoke the following command using a CLI and press any key right after sending the message: `emanafa`.
After the monitoring process, some results are reported on the command line. These results can also be seen in a visually appealing format, by submitting the results file (manafa_resume xxx.yyyy.json) to the dashboard available at https://greensoftwarelab.github.io/manafa-inspector).
3. Repeat the process 2 more times.
4. Fill the table available at with the values of CPU and wi-fi energy consumption and runtime obtained in the 3 tests. Fill the form available at https://forms.gle/ZdZWrtZWQxwWWSVm8.


# Exercise II Detecting and Repairing Energy Smells in Android source code

In this exercise, we will try to show how a developer can detect and repair some energy smells present in his source code using our toolset. Furthermore, you will need the analyze the source code of the demo app previously downloaded. First of all, you must open the application in the Android Studio IDE previously downloaded and build and install the application on your device, to verify that you have all the requirements to compile, build and execute the application on the device.

This application is illustrative of the typical pattern of Android development. It was developed in Java and built using the Gradle build system. It presents several types of views/screens (also known as Activities and Fragments) that are defined in XML format and loaded and transformed through Java classes. Each Java class extending an Activity or Fragment represents a part of the UI of the application. This demo application is a very simple soccer quiz, that loads a set of questions (transformed into Question models) from a questions.json file that is located in a specific resources directory (res/raw). These questions also contain associated images, which are contained in the /res/drawable folder. These questions are loaded into a well-known data structure in the ViewModel class and then used in 2 different views: QuestionListFragment and SingleQuestionFragment.

 Below is a diagram that illustrates the typical pattern of navigation over the various views of the application, as well as which components are used in each view.



Note: The application is currently instrumented with @HunterDebug annotations in order to be able to trace the application methods that are invoked and estimate the energy consumption. Do not remove these annotations and include them in new methods that you might implement during the exercises.

1. This application contains several energy smells reported in the literature and listed in this [catalog](). These smells can be identified manually, through SonarQube's E-Debitum plugin or through the Lint that is used by the Android Studio. The application contains at least 4 smells in its source code, and it also has a false positive according to the information provided by E-debitum and an additional smell in one of the XML files. Identify the smells contained in the application and measure the consumption of the methods where they are embedded. Evaluate if their resolution results in performance gains. To evaluate the impact of the smells in the source code and conduct the energy measurements, execute the following steps: 
	- a) Identify the methods with energy smells.
	- b) Start e-manafa from your CLI.
	- c) Run the application using Android Studio.
	- d) Perform some interactions over the application UI to force the invocation of its methods. 
	- e) stop e-manafa and collect the relevant results (the consumption of the *smelly* methods.
	-  f) Refactor the smells using the proposed solutions in the catalog. 
	- g) Repeat the previous steps until f) and compare the consumption of the methods. 
	-  h) Justify the obtained results. 

2. In addition to the smells found, several energy hotspots can be improved through simple refactorings. Identify these hotspots with the help of E-Manafa (by examining the consumption of the application methods) and propose or implement improvements that benefit your energy consumption. Hints: change of image loading method, object caching.

3. The application uses some auxiliary APIs to manipulate data files and images. Evaluate the impact of any changes in the energy consumption of the application. Suggestions:

- Changed Image loading method in the onBindViewHolder method (suggestion: use [Picasso](https://square.github.io/picasso/) or [Glide](https://github.com/bumptech/glide));
- Change JSON loading and handling library([GSON](https://github.com/google/gson), [others](https://www.appbrain.com/stats/libraries/tag/json/json-parsing-libraries));
- Change of data loading strategy (CSV, DB with sqlite);

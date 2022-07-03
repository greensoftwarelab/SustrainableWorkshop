
# SustrainableWorkshop

**Group work**: 2 -3 elements.
**Duration**: 90 mins.

## Installation / Setup


### 1. Requirements:
- Linux / Mac OS;
- Python >= 3.6;
- Java >= 8;
- 1 Android device;
- Android Studio (and consequently, Android SDK);
- E-Manafa;
- Demo app;



### 2. Android device setup
 In order to activate the developer features on your Android device and be able to establish a communication channel with your PC, it is necessary to activate the developers options in your device's settings. The procedure for enabling the necessary settings differs slightly between vendors and platform versions.
 The process can be performed by following these steps:
 

 1. Go to "Settings", then tap "About device" or "About phone". Scroll down, then tap "Build number" seven times. Depending on your device and operating system, you may need to tap "Software information", then tap "Build number" seven times. 3 Enter your pattern, PIN or password to enable the Developer options menu. This process will give you access to a wide set of features that are available in **Settings** -> **Developer Options**.
 2. Go to these settings and enable the following features: **USB debugging** and **Install via USB**.
 3. Increase the **Logger Buffer Size** to at least 4MB.
 
### 3.  Workstation setup

The process can be performed by following these steps: 
1. **Install Android Studio:** Go to the [Android Studio Web Page](https://developer.android.com/studio),  download the latest stable version and follow the installation instructions. 
2. **Install E-Manafa Profiler:**  `pip install manafa`
3. Clone Android application: `git clone https://github.com/RRua/sampleapp.git`


## Exercise I: Black-Box testing

 In this exercise, it is intended to use some of the previously installed tools to  measure the energy consumption associated with sending instant messages using  real applications. In order to be able to estimate the energy of this task, we need  the following tool set:
	 -   An instant messaging application (WhatsApp, Messenger, Google Chat, etc,  Discord, etc);
	-   A tool capable of estimating the energy consumption of the task or the  system during its execution (E-Manafa).
	- A set of guidelines to avoid interference in the measurements: Close other  apps, turn off unused sensors and hardware components, mute notifications,  etc.

Furthermore, in order to estimate the energy consumed by the process, follow the  following steps:
	
1. Select one of the suggested messaging apps. Monitor the consumption of  sending a message to a random subject. The process must include the step of  opening the application from the menu, select a receiver and send the  following message, typed using your default keyboard: ”Hi. Please ignore this message. This message was in the scope of a study that aims to estimate the  energy consumption of sending instant messages with different instant  messaging apps”. In order to monitor the energy consumption of the process,  invoke the following command using a CLI and press any key right after  sending the message: `emanafa` Note: If the installation process or the commands failed, try executing E-Manafa from the [sources].(https://greensoftwarelab.github.io/e-manafa).
After the monitoring process, some results are reported in the command line.  These results can also be seen in a visually appealing format, by submitting  the results file (manafa resume xxx.yyyy.json) to the dashboard available at https://greensoftwarelab.github.io/manafa-inspector .
3. Repeat the process 2 more times.
4. Fill the table available at  https://gdrive....sdasdas  with the values  obtained in the 3 tests.  


# Exercise II Detecting and Repairing Energy Smells in Android source code

In this exercise it is intended to detect and repair some energy smells present in  the source code of the sample app previously downloaded. First of all, you must open the  application in the Android Studio IDE previously downloaded and build and  install the application on your device, in order to verify that you have all the necessary requirements to compile, build and execute the application in the device.

-- image or gif showing the result of the execution

This application is illustrative of the typical pattern of Android development. It was developed in Java and built using the build system grid. It presents several types of views/screens that are defined in XML format and loaded and transformed through Java classes. This application loads a set of questions (transformed into Question models) contained in a questions.json file that is located in a resources directory (res/raw). These questions also contain associated images, which are also contained in the /res/drawable folder. These questions are loaded into a data structure in the ViewModel class, and then used in 2 different views: QuestionListFragment and SingleQuestionFragment.

 Below is a diagram that illustrates the typical pattern of navigation over the various views of the application, as well as which components are used in each view.

- diagram img url

The application is currently instrumented with @HunterDebug annotations in order to be able to trace the application methods that are invoked and estimate the energy consumption. Do not remove these annotations and include them in new methods you implement.

1. This application contains several energy smells reported in the literature and listed in: xx. These smells can be identified manually, through SonarQube's E-debitum plugin or through Lint. The application contains 4 smells in its source code, and it also has a false positive according to the information provided by E-debitum and an additional smell in XML files. Identify the smells contained in the application and measure the consumption of the methods where they are embedded and check if their resolution results in performance gains. To perform the energy measurement, use the following procedure:

 - In addition to the smells found, there are several energy hotspots that can be improved through simple refactorings. Identify these hotspots with the help of E-Manafa (by consulting the consumption of the application methods) and propose or implement improvements that benefit your energy consumption. Hints: change of image loading method, object caching.

 - The application uses some auxiliary APIs to manipulate data files and images. Evaluate the impact of any changes in the energy consumption of the application. Suggestions:

- Changed Image loading method ([Picasso](https://square.github.io/picasso/), [Glide](https://github.com/bumptech/glide));
- Changed JSON loading and handling library([GSON](https://github.com/google/gson), [others](https://www.appbrain.com/stats/libraries/tag/json/ json-parsing-libraries));
- Change of data loading strategy (CSV, DB with sqlite);

[![frontend-repo-header-2.png](https://i.postimg.cc/Jzwjf6Km/frontend-repo-header-2.png)](https://postimg.cc/ykPJ9Twr)

[![license](https://img.shields.io/badge/license-GPLv3-blue)]()
[![platform](https://img.shields.io/badge/platform-IOS%20%7C%20Android-lightgrey)]()
[![react-native](https://img.shields.io/badge/react%20native-0.67.2-blue)]()

## Table of Contents:

- [Before You Start](#before-you-start)
- [Introduction](#introduction)
- [Installation](#installation)
  - [Preparation](#preparation)
  - [Let's Start](#lets-start)
    - [Android](#android)
    - [iOS](#ios)
- [Connect To Server](#connect-to-server)
- [Automated Emergency System](#automated-emergency-system)
  - [Pulse-Based Trigger](#-pulse-based-trigger)
  - [Time-Based Trigger](#-time-based-trigger)
- [Software Overview](#software-overview)
  - [Project Structure](#project-structure)
  - [Services](#services)
  - [State Management](#state-managment)
- [Setup wearables](#setup-wearables)
  - [iOS](#ios-1)
  - [Android](#android-1)
- [Disclaimer](#disclaimer)
- [License](#license)

## Before You Start:

- Read our [contribution](https://github.com/tomorrowbiostasis/tomorrowbiostasis/blob/main/CONTRIBUTING.md) guidance to gain better understanding on how to be a part of the Biostasis development community.
- Please make sure to visit the [Biostasis-Cloud-infrastructure](https://github.com/tomorrowbiostasis/Biostasis-Cloud-infrastructure) repository and create your own cloud and external services. **Otherwise, you won't be able to run the application properly (you need your own .env credentials).**
- If you want to participate in the development of the automated pulse system, you need to own a smart watch to be able to test your implementation or new feature.

## Introduction:

This documentation is for the frontend (Mobile App) part of the Biostasis application. Here you will find all the information to build and install the application on your machine and run it on both development/production environments. Included in this documentation is a short summary of the main features of our application and the services that we are using to implement and execute the app.

## Tech Stack:

<a href="https://reactnative.dev/" title="react native"><img height="50" src="https://user-images.githubusercontent.com/25181517/183897015-94a058a6-b86e-4e42-a37f-bf92061753e5.png" alt="React-native" title="React-native" /></a>
<a href="https://firebase.google.com/" title="firebase"><img height="50" src="https://user-images.githubusercontent.com/25181517/189716855-2c69ca7a-5149-4647-936d-780610911353.png" alt="Firebase" title="Firebase" /></a>
<a href="https://www.typescriptlang.org/" title="Typescript"><img height="50" src="https://user-images.githubusercontent.com/25181517/183890598-19a0ac2d-e88a-4005-a8df-1ee36782fde1.png" alt="TypeScript" title="TypeScript" /></a>
<a href="https://aws.amazon.com/cognito/" title="aws"><img height="50" src="https://user-images.githubusercontent.com/25181517/183896132-54262f2e-6d98-41e3-8888-e40ab5a17326.png" alt="AWS" title="AWS" /></a>
<a href="https://redux.js.org/" title="redux"><img height="50" src="https://user-images.githubusercontent.com/25181517/187896150-cc1dcb12-d490-445c-8e4d-1275cd2388d6.png" alt="Redux" title="Redux" /></a>
<a href="https://developer.apple.com/swift/" title="swift"><img height="50" src="https://user-images.githubusercontent.com/25181517/121406389-6267a300-c95e-11eb-8d67-f1e22afe8aea.png" alt="Swift" title="Swift" /></a>
<a href="https://nodejs.org/" title="node.js"><img height="50" src="https://user-images.githubusercontent.com/25181517/183568594-85e280a7-0d7e-4d1a-9028-c8c2209e073c.png" alt="Node.js" title="Node.js" /></a>

The Biostasis mobile application is built using the following technologies:

- **React Native:** A framework for building mobile applications using JavaScript and React. React Native enables building native apps for iOS and Android platforms from a single codebase.
- **Firebase:** A cloud-based platform that provides a wide range of services, including authentication, real-time database, storage, and analytics. We use Firebase for cloud messaging and crashlytics.
- **TypeScript:** A superset of JavaScript that adds static type checking and other features to the language. TypeScript enables easier maintenance and scaling of the application.
- **AWS Cognito:** A service that provides user authentication and authorization. We use AWS Cognito for user authentication and management.
- **Redux:** A state management library that enables managing the state of the application in a predictable and scalable way. We use Redux for state management in the Biostasis mobile application.
- **Swift**: Swift is a powerful and intuitive programming language for iOS, iPadOS, macOS, tvOS, and watchOS. Used in our application to build the emergency system on IOS devices.

In combination, these technologies provide a powerful and scalable frontend architecture for our application.

## Installation:

### Preparation:

There are multiple steps you should take before you start the installation stage:

1.  If you want to participate in the development of our app on the Android platform, Make sure that you have [Android Studio](https://developer.android.com/studio) installed on your machine. Then, set up the [Android 14 SDK](https://developer.android.com/about/versions/14/setup-sdk).
2.  If you have a Mac device and want to participate in the development of our app on the iOS platform, make sure to install [Xcode](https://developer.apple.com/xcode/).
3.  Make sure that you have [Node.js](https://nodejs.org/) installed.
4.  We use [yarn](https://yarnpkg.com/) as package manager for node.js, so make sure to install yarn using this command:

        npm install --global yarn

5.  You need to have a [Firebase](https://firebase.google.com/) account, if not, please create a new account. Then, create new project under the name `Biostasis`:

    - First, pick the platform that you want to work on (Android or iOS).
    - Then, add a new app for that platform.
    - Make sure that the package name for your app is `app.biostasis`

      **or else you need to change the local package name inside `build.gradle` file to match your input name.**

    - - (Android) Download `google-services.json` file and move it inside `/android/app`.
      - (iOS) Download `GoogleService-Info.plist` file and move it inside `ios/Biostasis`.
    - Ensure to add **Firebase SDK** (instructions provided during the creation of the new app).
    - - (Android) Ensure that **[Firebase Crashlytics](https://firebase.google.com/docs/crashlytics/get-started?platform=android)** added to your Android project.
      - (IOS) Firebase packages are already installed when you install pods so no need to add packages through Xcode.
    - And you are now ready to go 🎉

    **_PS: you can create two apps for each platform, make sure to follow the instruction carefully._**

### Let's Start:

After you navigate to the project directory. Install all dependencies for the application.

    yarn

### Android:

---

1.  Ensure that [Java](https://www.java.com/) installed on your machine.
2.  Using Android Studio open the application's android folder `~/biostasis-frontend/android`. Android Studio will start building your application automatically.
3.  Wait until Android Studio finishes building your application. Then, set up your Android device:
    - **Android Studio emulator**: follow this [**link**](https://developer.android.com/studio/run/managing-avds) to learn how to create and manage virtual devices.
    - **Physical Android device**: follow this [**link**](https://developer.android.com/studio/run/device) to learn how to run apps on hardware devices. There are a lot of methods and instructions for every operating system.
      - ##### Physical Devices:

      Once you have your hardware device ready, make sure that the connection is forwarded to the right port (Android device port:8081 -> computer port:8081 where metro bundler is running) Either using:

      - **adb command:**

            adb reverse tcp:8081 tcp:8081

      - **chrome dev tool:** visit [this page](https://developer.chrome.com/docs/devtools/remote-debugging/) to learn how to debug Android devices remotely.

        - Visit `chrome://inspect/#devices`
        - Click on `Port forwarding`. Then, add a new port:

          <table>
            <tr>
              <td>Port</td>
              <td>IP addresses and port</td>
            </tr>
            <tr>
              <td>8081</td>
              <td>localhost:8081</td>
            </tr>
          </table>

        - Make sure `Enable port forwarding` is checked.
        - Keep the tab open during your development process.

4.  Run metro bundler:

        yarn start

5.  Run the application `Run > Run'app'`, this will install the application on your Android device and run it automatically. After that, it will take some time until metro bundler finishes bundling all project files into one main file.

=================================== **Alternatively** ===================================

You can run the application outside Android Studio.

- Make sure that you have `local.properties` file in your `android` directory (usually this file will be created automatically by Android Studio). It should contain the path to your Android SDK directory.

  - Mac: `sdk.dir = /Users/[username]/Library/Android/sdk`
  - Windows: `sdk.dir=C\:\\Users\\[username]\\AppData\\Local\\Android\\Sdk`

- Add JDK path `org.gradle.java.home=<PATH_TO_JDK_OR_JBR_DIR>` (you can find the path where java is installed) to `gradle.properties` file
- Run:

      yarn android:dev

  **_PS: Don't forget to forward to the right port [(step 4)](#physical-devices)._**

### iOS:

---

1.  Install [Cocoapods](https://cocoapods.org/) on your Mac machine using:

        sudo gem install cocoapods

2.  Navigate to the project's ios folder using terminal `cd ~/Biostasis-FrontEnd/ios`, you will see a ruby file called `Podfile`. Then, install pods into the project by typing in the terminal:


        pod install

    or (For Apple Silicon chip)

        arch -x86_64 pod install (TODO(remonechev): Is this still correct?)

3.  Once completed, there will be a message that says:

    > Pod installation complete! There are X dependencies from the Podfile and X total pods installed.

4.  Using Xcode open the application's iOS folder `~/biostasis-frontend/ios`. Xcode will start building your application automatically.
5.  Then, after Xcode finishes building the project, you can run the application. Visit [this page](https://developer.apple.com/documentation/xcode/running-your-app-in-simulator-or-on-a-device) to learn more about how you can run the application on a simulator or physical device.

**_PS: if you faced an error with the `Yoga` file just add `|` where the error is mentioned._**

## Connect To Server:

- If you want to connect the biostasis frontend application to a backend server you need to build the [backend side of the application](https://github.com/tomorrowbiostasis/Biostasis-Backend) and then run the server.
- The `API_URL` in the `.env.(env-type)` file should match the host that your backend server is running on:

  eg. `API_URL="http://localhost:<server-port>"`

- (Physical Devices) You need to forward device's to the server's port [**step4**](#physical-devices).

**PS: You need to replace the `localhost` with your Mac's WiFi IP Address if you are developing on iOS (`localhost` works on Android)**

## Automated Emergency System:

This is the main feature for our application. we can implement it by turning the automated emergency **ON** in the Automated Emergency Settings screen inside the application.

There are two types of triggering for the automated emargency system:

### 💗 Bio-Based Trigger:

---

This section provides an overview of the Bio-Based Trigger feature implemented in this GitHub repository. The Bio-Based Trigger enables the monitoring of user health by utilizing (heart rate - resting heart rate - movement) data obtained from Google Fit.

#### Activation Process:

To activate the Bio-Based Trigger in the app, follow these steps:

1. Mark the additional checks, including the (Google Fit - HealthKit) check, which initiates an authentication modal.
2. Other checks, such as the companion app connection to Google Fit and background service enablement, rely on user trust and cannot be directly verified.
3. Once all the checks are marked, the bio-based trigger is turned on in the backend.

#### Functionality:

Once the trigger is activated, the following processes occur:

1. A non-dismissible notification is displayed on the user's system, indicating that the app is actively monitoring their health.
2. A background service is launched to periodically check the user's bio data from Google Fit at intervals shorter than the selected frequency.

#### Positive Bio Data:

When positive pulse data is detected within the specified time period, the following actions take place:

1. A call is made to the backend with the time of the next scheduled emergency.
2. The backend waits for the next positive information to be sent, extending the emergency time if positive information is received.
3. If no positive information is received within the time period, the emergency is triggered.

#### No Detected Bio:

If no pulse is detected within the specified time period, the following steps occur:

1. No positive information is sent, leading to further escalation.
2. An "Are you okay?" notification is sent, prompting the user for a response.
3. If the user does not respond, a loud alarm is scheduled, and a notification is sent from the backend, followed by a text message.

#### Pause and Nighttime Considerations:

During pauses or nighttime periods, bio data gets checked and positive information can still be sent. However, the backend has the ability to omit processing the information while the pause time is set.

#### Emergency Triggered:

Once the emergency is triggered, the following actions occur:

1. Opening the app will display a modal informing the user about the emergency situation.
2. If the emergency time has not yet arrived, the user can inform the app that they are okay, resulting in a delay of the emergency.
3. If the information has already been sent to contacts, no further action is taken from the backend side, unless a positive status is sent again, which resets the system to its pre-emergency functioning.
4. On the app or device side, the background service continues to be active and send positive status if a pulse is detected.

### ⏰ Time-Based Trigger:

---

This section provides an overview of the Time-Based Trigger feature implemented in this GitHub repository. The Time-Based Trigger does not activate the background service but relies on timed notifications.

#### Functionality:

The Time-Based Trigger operates as follows:

1. The backend sends periodic notifications asking "Are you okay?" at specified time intervals to the user's device.
2. The user has 20 minutes to confirm their well-being, which sends a positive status to the backend.
3. Unlike the pulse-based trigger, the backend only waits for positive information between the "Are you okay?" notification and the actual emergency, instead of continuously.
4. Scheduled pauses and nighttime periods are skipped.
5. If the user does not respond, the emergency message is sent to contacts.
6. No further action is taken from the backend or device once the emergency message is sent.

## Software Overview:

### Project Structure:

This section outlines the structure and organization of the project repository, including its various directories and files.

- **assets:** This directory contains icons, components, and static images used in the project.
- **components:** The components directory contains shared components that can be reused throughout the application.
- **constants:** The constants directory includes files that contain constant values used in the project.
- **hooks:** The hooks directory contains custom hooks that encapsulate reusable logic and can be utilized across different components.
- **i18n:** The i18n directory consists of localization files and configurations that enable internationalization and localization support in the application.
- **models:** The models directory holds type definitions or interfaces that describe the structure and shape of the data used within the project.
- **navigators:** The navigators directory contains stacks and navigator components responsible for handling navigation between different screens or sections of the application.
- **providers:** The providers directory includes various providers used in the project, such as AuthListeners, NotificationListeners, and other providers like SafeArea, PersistGate, and Native Base UI provider. These providers offer context and services that can be accessed by components throughout the application.
- **redux:** The redux directory encompasses the Redux implementation using Redux Toolkit. It includes the store configuration and related files for managing the application's state.
- **screens:** The screens directory contains individual screen components along with their related components. These components represent the different screens or views within the application.
- **services:** The services directory includes modules or classes that handle specific services required by the application, as mentioned in the Services section.
- **theme:** The theme directory consists of files related to the theme configuration for the Native Base UI library. It includes style definitions, colors, typography, and other theme-related settings.
- **utils:** The utils directory contains utility functions or helper modules that provide common functionalities used throughout the project. These utilities serve various purposes and are typically self-explanatory in nature.
- **services**: The services directory houses various services responsible for specific functionalities within the app. Each service performs a specific task and encapsulates the related logic and functionality.

Each directory contains a README file to document the modules and files inside that directory.

Please note that this list may not be exhaustive, but it gives an overview of the services available in the src/services directory.

## State Management:

In this project, Redux Toolkit is utilized for managing the state of the application. The state is stored in the `src/redux/store` folder.

### Redux Store:

The Redux store is the central hub for storing and managing the application state. It acts as a single source of truth, allowing components to access and modify the state. The store is configured using Redux Toolkit.

### State Persistence:

To persist the state, certain slices of the state are stored using the react-native-encrypted-storage library, specifically the EncryptedStorage module. This library provides a secure storage solution for sensitive data, ensuring that the stored state remains encrypted and protected.

By utilizing EncryptedStorage, the application can persist the specified slices of the state across app sessions, allowing for the restoration of state data when the app is relaunched.

Please note that while the state persistence is achieved through react-native-encrypted-storage, other parts of the state that don't require encryption may be stored and managed using regular Redux functionality.

## Set Up wearables

### iOS:

- You need to have an Apple Watch or other type of smart watch, connect it to your iPhone device and then open the [Health app](https://www.apple.com/ios/health/) to make sure that everything works well.
- You can connect other watches to your Health app. However, you need to install the app related to your watch and then connect it to Health app. [Mi Band Example](https://govida.io/faqs/how-do-i-connect-mi-band-to-apple-health/)

### Android:

The process for the Android system is a little bit more complicated. We need a device that has a companion app capable to connect to Google Fit and working in the background. Not every device has this capability. Example with Mi Band 5/6:

- Install the Zepp Life (formerly Mi Band) app on your Android device.
- Open the Zepp Life app and click on the **Connect** button.
- Set up the band connection in the default way.
- Connect the Zepp Life app to your Google Fit account.
- Enable background modes in the Zepp Life app.
- Open Zepp Life Settings and then enable **Show status in the notification bar**.
- Go back to Biostasis app.
- Enable Automated Emergency in the Biostasis app.
- Enable the pulse-based trigger (It should be selected by default).
- Enable the Google Fit switch and pair the Biostasis app with your Google Fit account, the same as you used in the step 4.
- Enable the other switches (**Background modes** from step 4 and **connect app to Google Fit** from step 4).
- You should see **System is ON** and a status in the notification bar.

## Disclaimer

1. The application uses GoogleFit and HealthKit APIs so make sure to have (Android) GoogleFit - (iOS) Health accounts before using the application.

2. Make sure that your smart device is connected to those accounts and that you can see your health data. Some smart watches do not send your health data directly to GoogleFit/HealthKit, So you always need to sync your health data with GoogleFit/Health apps.

3. If you are planning to use short periods (3-6-9) hours. Please, make sure:

    - Your smart device syncs data directly to GoogleFit/HealthKit.
    - Pause the system during your sleep (if the user does not interact with their phone no new health data will be fetched).

4. In the case of a false emergency the system will turn off after contacting your emergency contacts so make sure to turn on the system again.

5. Also, both systems work differently:

    - Android: Runs a background service that fetches data every 15 min from GoogleFit.
    - iOS: It will fetch new data every 1-2 hours and the user needs to unlock their phone (HealthKit and Apple privacy policy).

## License:

Licensed under the [GNU General Public License v3.0](LICENSE)
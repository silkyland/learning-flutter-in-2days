# Setting up the Environment

To start developing with Flutter, you need to set up your environment. This involves installing the necessary tools and configuring your system. Follow these steps to get started:

## Installing Flutter SDK

1. Download the Flutter SDK from the official website: [https://docs.flutter.dev/get-started/install](https://docs.flutter.dev/get-started/install)
2. Extract the downloaded ZIP file and place the `flutter` folder in your desired location (e.g., `C:\src\flutter` for Windows or `~/Developer/flutter` for macOS/Linux).
3. Add the `flutter/bin` directory to your PATH environment variable:

- For Windows: In the search bar, type 'env' and select "Edit the system environment variables". Click on the "Environment Variables" button. Under "User variables" or "System variables", find the "Path" variable, select it, and click "Edit". Click "New" and add the path to your `flutter/bin` directory.
- For macOS/Linux: Add the following line to your `~/.bashrc` or `~/.zshrc` file: `export PATH="$PATH:[PATH_TO_FLUTTER_SDK]/flutter/bin"`

## Installing Android Studio and VS Code

Flutter development requires an IDE. You can choose between Android Studio and Visual Studio Code:

1. Download and install Android Studio from [https://developer.android.com/studio](https://developer.android.com/studio) or VS Code from [https://code.visualstudio.com](https://code.visualstudio.com).
2. Launch your chosen IDE and install the Flutter and Dart plugins:

- For Android Studio: Go to "File" -> "Settings" -> "Plugins". Search for "Flutter" and "Dart", and install both plugins.
- For VS Code: Go to the Extensions view (Ctrl+Shift+X). Search for "Flutter" and "Dart", and install both extensions.

## Creating a New Flutter Project

1. Open your terminal or command prompt.
2. Navigate to the directory where you want to create your Flutter project.
3. Run the following command to create a new Flutter project:

   ```bash
   flutter create my_app
   ```

   Replace `my_app` with your desired project name.

4. Navigate into the project directory:
   ```bash
   cd my_app
   ```
5. Connect a device or start an emulator/simulator.
6. Run the Flutter app with the following command:
   `bash
flutter run
`
   This will launch your Flutter app on the connected device or emulator/simulator.

## Verifying the Setup

To verify that your Flutter setup is complete and working correctly, run the following command in your terminal or command prompt:

    ```bash
    flutter doctor
    ```

This command checks your environment and displays a report of the status of your Flutter installation. Make sure that no issues are reported.

With these steps completed, you're ready to start building Flutter applications!

## References

1. Flutter official installation guide: [https://docs.flutter.dev/get-started/install](https://docs.flutter.dev/get-started/install)
2. Flutter environment setup for beginners: [https://haroonkhan9426.medium.com/flutter-environment-setup-for-a-complete-beginner-261fa225e5a5](https://haroonkhan9426.medium.com/flutter-environment-setup-for-a-complete-beginner-261fa225e5a5)
3. Setting Flutter path in Windows environment variables: [https://stackoverflow.com/questions/60212125/flutter-install-in-windows-environment-variable](https://stackoverflow.com/questions/60212125/flutter-install-in-windows-environment-variable)
4. Step-by-step Flutter development environment setup: [https://medium.com/@sahaj.blup/flutter-development-environment-setup-a-step-by-step-guide-5e457583bc4d](https://medium.com/@sahaj.blup/flutter-development-environment-setup-a-step-by-step-guide-5e457583bc4d)
5. Setting up the Flutter framework development environment: [https://github.com/flutter/flutter/wiki/Setting-up-the-Framework-development-environment](https://github.com/flutter/flutter/wiki/Setting-up-the-Framework-development-environment)

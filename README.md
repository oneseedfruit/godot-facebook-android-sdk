# Facebook Android SDK Plugin for Godot 3.2.2+

*NOTE: This is currently a *WIP* I quickly put together for my own use, which I may or may not continue to maintain, also for my own use, at my day job.*

*Currently tested to be working with Godot 3.4.4, at least in my own use cases.*

This is a Facebook Android SDK plugin ported to the Android plugin system of Godot 3.2.2 (non-Mono) and later Godot 3 versions, modified from the original developed by [DrMoriarty](https://github.com/DrMoriarty/godot-facebook) in the v1 Android plugin system.

## Quick Start

### Part 1: Building and Setting Up the Android Archive Library (aar)

*You can skip this step and obtain the files from the [Releases](https://github.com/oneseedfruit/godot-facebook-android-sdk/releases) page instead.*

1. Open `GodotFacebook` in Android Studio, and wait for gradle to sync completely.
2. Run the `build` task in gradle. Or in `./GodotFacebook/`, in your command line interface, run `./gradlew build`.
3. When it is done, the newly generated build files are in `./GodotFacebook/app/build/outputs/aar/`:
    i. `app-debug.aar`
    ii. `app-release.aar`
4. Rename `app-release.aar` to `GodotFacebook.release.aar`.
5. Copy or move this `GodotFacebook.release.aar` file and the `GodotFacebook.gdap` file into your Godot project, place them in `<Godot project location>/android/plugins/` using your file manager (you can't see those files in the Godot editor).

---

### Part 2: Setting Up the Android Custom Build

1. If you don't already have an existing Android custom build template in `<Godot project location>/android/build/`, in the Godot editor, in the menu, *Project* -> *Install Android Build Template*.
2. Edit the file `<Godot project location>/android/build/AndroidManifest.xml` and add anywhere in between `<application>` and `</application>`:
    
    ```
    <meta-data android:name="com.facebook.sdk.ApplicationId" android:value="@string/facebook_app_id"/>
    <meta-data android:name="com.facebook.sdk.ClientToken" android:value="@string/facebook_client_token"/>
    ```

    but take care that you don't add them in between the `<!--CHUNK ...... -->` begin and end tags.
3. Add or edit (if it already exists) the file `<Godot project location>/android/build/res/values/strings.xml` and place these lines in that file or if you already have some prior string tags, place the two string tags with `facebook_app_id` and `facebook_client_token` and then your Facebook app ID and client token within the respective tags:

    ```
    <?xml version="1.0" encoding="utf-8"?>
    <resources>
            <string name="facebook_app_id">YOUR FACEBOOK APP ID HERE</string>
            <string name="facebook_client_token">YOUR FACEBOOK CLIENT TOKEN HERE</string>
    </resources>
    ```
4. Edit the file `<Godot project location>/android/build/config.gradle`, in `ext.versions`, change the values for both `compileSdk` and `targetSdk` to `31` respectively.

---

### Part 3: Using the Plugin in GDScript

1. In the Godot editor, in the menu, *Project* -> *Export...*, then in your Android export settings, under *Plugins*, check *Godot Facebook*.
2. Add the script in the file `./facebook.gd` to your Godot project as an Autoload and start using the functions in that script.

# SPPermissions

<img align="left" src="https://github.com/ivanvorobei/SPPermissions/blob/main/Assets/Readme/preview-v6.2.0.jpg" width="420"/>

### About
Library for ask permissions.  You can check state of permissions, available `.authorized`, `.denied` & `.notDetermined`.

Available ready-use controllers for reqeust permissions: list, dialog & native. Support iPad, dark mode and RTL. Interface in an Apple style.  For beginner see [Quick Start](#quick-start).

If you like the project, don't forget to `put star ★` and follow me on GitHub:

[![https://github.com/ivanvorobei](https://github.com/ivanvorobei/Readme/blob/main/Buttons/follow-me-ivanvorobei.svg)](https://github.com/ivanvorobei)

### Permissions

<p float="left">
    <img src="https://github.com/ivanvorobei/SPPermissions/blob/main/Assets/Permissions/camera.png" width="38">
    <img src="https://github.com/ivanvorobei/SPPermissions/blob/main/Assets/Permissions/photos.png" width="38">
    <img src="https://github.com/ivanvorobei/SPPermissions/blob/main/Assets/Permissions/notifications.png" width="38">
    <img src="https://github.com/ivanvorobei/SPPermissions/blob/main/Assets/Permissions/location.png" width="38">
    <img src="https://github.com/ivanvorobei/SPPermissions/blob/main/Assets/Permissions/microphone.png" width="38">
    <img src="https://github.com/ivanvorobei/SPPermissions/blob/main/Assets/Permissions/calendar.png" width="38">
    <img src="https://github.com/ivanvorobei/SPPermissions/blob/main/Assets/Permissions/contacts.png" width="38">
    <img src="https://github.com/ivanvorobei/SPPermissions/blob/main/Assets/Permissions/reminders.png" width="38">
    <img src="https://github.com/ivanvorobei/SPPermissions/blob/main/Assets/Permissions/motion.png" width="38">
    <img src="https://github.com/ivanvorobei/SPPermissions/blob/main/Assets/Permissions/music.png" width="38">
    <img src="https://github.com/ivanvorobei/SPPermissions/blob/main/Assets/Permissions/speech.png" width="38">
    <img src="https://github.com/ivanvorobei/SPPermissions/blob/main/Assets/Permissions/bluetooth.png" width="38">
    <img src="https://github.com/ivanvorobei/SPPermissions/blob/main/Assets/Permissions/health.png" width="38">
    <img src="https://github.com/ivanvorobei/SPPermissions/blob/main/Assets/Permissions/tracking.png" width="38">
    <img src="https://github.com/ivanvorobei/SPPermissions/blob/main/Assets/Permissions/faceid.png" width="38">
    <img src="https://github.com/ivanvorobei/SPPermissions/blob/main/Assets/Permissions/siri.png" width="38">
</p>

## Navigate

- [Installation](#installation)
    - [Swift Package Manager](#swift-package-manager)
    - [CocoaPods](#cocoapods)
    - [Manually](#manually)
- [Imports](#imports)
- [Quick Start](#quick-start)
- [Status](#status)
- [Request](#request)
    - [Dialog](#dialog)
    - [List](#list)
    - [Native](#native)
- [DataSource](#datasource)
    - [Denied alert](#denied-alert)
- [Delegate](#delegate)
- [Localizations](#localizations)
- [Keys in Info.plist](#keys-in-infoplist)
- [Apple Review](#apple-review)
- [Сontribution](#сontribution)
- [Other Projects](#other-projects)
- [Russian Community](#russian-community)

## Installation

Ready to use on iOS 11+. Supports iOS, tvOS and SwiftUI. Works with Swift 5+. Requires Xcode 12.5 and higher.

<img align="right" src="https://github.com/ivanvorobei/SPPermissions/blob/main/Assets/Readme/spm-install-preview.png" width="490"/>

### Swift Package Manager

The [Swift Package Manager](https://swift.org/package-manager/) is a tool for managing the distribution of Swift code. It’s integrated with the Swift build system to automate the process of downloading, compiling, and linking dependencies.

To integrate `SPPermissions` into your Xcode project using Xcode 12, specify it in `File > Swift Packages > Add Package Dependency...`:

```ogdl
https://github.com/ivanvorobei/SPPermissions
```

Next choose the permissions you need. But don't add all of them, because apple will reject your app.

### CocoaPods:

[CocoaPods](https://cocoapods.org) is a dependency manager for Cocoa projects. For usage and installation instructions, visit their website. To integrate `SPPermissions` into your Xcode project using CocoaPods, specify it in your `Podfile`:

```ruby
pod 'SPPermissions/Notification'
```

Due to Apple's new policy regarding permission access you need to specifically define what kind of permissions you want to access using subspecs. For example if you want to access `Camera`, `Location` & `Microphone` you define the following:

```ruby
pod 'SPPermissions/Camera'
pod 'SPPermissions/LocationAlways'
pod 'SPPermissions/Microphone'
```

<details><summary>Available subspecs</summary>
<p>

```ruby
pod 'SPPermissions/Camera'
```
```ruby
pod 'SPPermissions/Contacts'
```
```ruby
pod 'SPPermissions/Calendar'
```
```ruby
pod 'SPPermissions/PhotoLibrary'
```
```ruby
pod 'SPPermissions/Notification'
```
```ruby
pod 'SPPermissions/Microphone'
```
```ruby
pod 'SPPermissions/Reminders'
```
```ruby
pod 'SPPermissions/SpeechRecognizer'
```
```ruby
pod 'SPPermissions/LocationWhenInUse'
```
```ruby
pod 'SPPermissions/LocationAlways'
```
```ruby
pod 'SPPermissions/Motion'
```
```ruby
pod 'SPPermissions/Music'
```
```ruby
pod 'SPPermissions/Bluetooth'
```
```ruby
pod 'SPPermissions/Tracking'
```
```ruby
pod 'SPPermissions/FaceID'
```
```ruby
pod 'SPPermissions/Siri'
```
```ruby
pod 'SPPermissions/Health'
```

</p>
</details>

### Manually

If you prefer not to use any of dependency managers, you can integrate `SPPermissions` into your project manually. Copy code and add compile flags from [CONTRIBUTING.md](https://github.com/ivanvorobei/SPPermissions/CONTRIBUTING.md) file.

## Imports

If you install via  [Swift Package Manager](#swift-package-manager), you shoud import each module:

```swift
import SPPermissions
import SPPermissionsCamera
import SPPermissionsPhotoLibrary
```

If you install via [CocoaPods](#cocoapods), you only need to import one class:

```swift
import SPPermissions
```

Its required because library split to modules. After importing you'll see available permissions by typing `SPPermissions.Permission.camera` for example.

## Quick Start

```swift

// MARK: 1. Choose the permissions you need:

let permissions: [SPPermissions.Permission] = [.camera, .notification]

// MARK: 2. Choose present style:

// 2a. List Style
let controller = SPPermissions.list(permissions)
controller.present(on: self)

// 2b. Dialog Style
let controller = SPPermissions.dialog(permissions)
controller.present(on: self)

// 2c. Native Style
let controller = SPPermissions.native(permissions)
controller.present(on: self)

// MARK: 3. Optional: Check permission state (available `authorized`, `denied`, `notDetermined`):

let authorized = SPPermissions.Permission.calendar.authorized
```

For more details check [Request](#Request) section.

## Status

To check the state of any permission, call `SPPermissions.Permission`: 

```swift
let authorized = SPPermissions.Permission.calendar.authorized
```

Also available `denied` & `notDetermined`.

## Request

Now available 3 present styles: `Dialog`, `List` and `Native`. Each interface has delegates and a data source. If you want see an example app, open `Example Apps/SPPermissions.xcodeproj`.

### Dialog

This is a modal alert. I recommend using this alert style when you have less than three requested permissions. Usage example:

```swift
let controller = SPPermissions.dialog([.camera, .photoLibrary])

// Ovveride texts in controller
controller.titleText = "Title Text"
controller.headerText = "Header Text"
controller.footerText = "Footer Text"

// Set `DataSource` or `Delegate` if need. 
// By default using project texts and icons.
controller.dataSource = self
controller.delegate = self

// Always use this method for present
controller.present(on: self)
```

### List

Native `UITableViewController` with support for the iPad. Use it when you have more than two permissions. An example of how it is used:

```swift
let controller = SPPermissions.list([.calendar, .camera, .contacts])

// Ovveride texts in controller
controller.titleText = "Title Text"
controller.headerText = "Header Text"
controller.footerText = "Footer Text"

// Set `DataSource` or `Delegate` if need. 
// By default using project texts and icons.
controller.dataSource = self
controller.delegate = self

// Always use this method for present
controller.present(on: self)
```

### Native

Request permissions with native alerts. You can request many permissions at once:

```swift
let controller = SPPermissions.native([.calendar, .camera, .contacts])

// Set `Delegate` if need. 
controller.delegate = self

// Always use this method for request. 
controller.present(on: self)
```

## DataSource

For data source using protocol `SPPermissionsDataSource`. You can customise the permission cells / provide denied alert texts.

```swift
extension Controller: SPPermissionsDataSource {
    
    func configure(_ cell: SPPermissionsTableViewCell, for permission: SPPermissions.Permission) {
        
        // Here you can customise cell, like texts or colors.
        
        cell.permissionTitleLabel.text = "Title"
        cell.permissionDescriptionLabel.text = "Description"
        
        // If you need change icon, choose one of this:
        
        cell.permissionIconView.setPermissionType(.bluetooth)
        cell.permissionIconView.setCustomImage(UIImage.init(named: "custom-name"))
        cell.permissionIconView.setCustomView(YourView())
    }
}
```

<img align="left" src="https://github.com/ivanvorobei/SPPermissions/blob/main/Assets/Readme/preview-denied-alert.png" width="320"/>

### Denied alert

If permission denied, you can provide alert to user with an option to open settings. Here you can customise the alert text:

```swift
let texts = SPPermissionDeniedAlertTexts()
texts.titleText = "Permission denied"
texts.descriptionText = "Please, go to Settings and allow permission."
texts.actionText = "Settings"
texts.cancelText = "Cancel"
```

Next implement method and return:

```swift
func deniedAlertTexts(for permission: SPPermissions.Permission) -> SPPermissionDeniedAlertTexts? {
    
    // Custom texts:
    return texts
    
    // or default texts:
    // return .default
}
```

## Delegate

To get "hidden", "allowed" or "denied" events , set the delegate with protocol `SPPermissionsDelegate`:

```swift
extension Controller: SPPermissionsDelegate {
    
    func didHidePermissions(_ permissions: [SPPermissions.Permission]) {}
    func didAllowPermission(_ permission: SPPermissions.Permission) {}
    func didDeniedPermission(_ permission: SPPermissions.Permission) {}
}
```

## Localizations

App has ready-use localisation for:

- English `en`
- Arabic `ar`
- German `de`
- Spanish `es`
- French `fr`
- Polish `pl`
- Portuguese `pt`
- Ukrainian `uk`
- Russian `ru`
- Chinese Simplified Han `zh_Hans`
- Italian `it`

If you want add more, please, create folder `language_id.lproj` and make pull request. If you want use your custom strings, check [DataSource](#datasource) section.

## Keys in Info.plist

You need to add some keys to the `Info.plist` file with descriptions. You can get plist keys for permission:

```swift
let key = SPPermissions.Permission.bluetooth.usageDescriptionKey
```

List of keys:

- NSCameraUsageDescription
- NSContactsUsageDescription
- NSCalendarsUsageDescription
- NSMicrophoneUsageDescription
- NSAppleMusicUsageDescription
- NSRemindersUsageDescription
- NSPhotoLibraryUsageDescription
- NSPhotoLibraryAddUsageDescription
- NSSpeechRecognitionUsageDescription
- NSMotionUsageDescription
- NSLocationWhenInUseUsageDescription
- NSLocationAlwaysAndWhenInUseUsageDescription
- NSBluetoothAlwaysUsageDescription
- NSBluetoothPeripheralUsageDescription (iOS 12 and earlier)
- NSUserTrackingUsageDescription
- NSFaceIDUsageDescription
- NSSiriUsageDescription
- NSHealthUpdateUsageDescription
- NSHealthShareUsageDescription

Do not use the description as the name of the key.

If you use xliff localization export, keys will be create automatically. If you prefer do the localization file manually, you need to create `InfoPlist.strings`, select languages in the right side menu and add keys as keys in plist-file. See:

```
"NSCameraUsageDescription" = "Here description of usage camera";
```

## Apple Review

Apple changed its review guidelines. When requesting permissions, apps should users to always request and make a decision whether to allow or decline. For this reason,  the close button is hidden by default. If you want to force show the close button, run the following code:

```swift
// Work for any style
controller.showCloseButton = true
```

Also changed title for button. Instead of  `allow` now using `continue`. The Apple Review Team asked for this. For details, check out[this issue](https://github.com/ivanvorobei/SPPermissions/issues/229). 

## Сontribution

My English is very bad. You can see this once you read the documentation. I would really like to have clean and nice documentation. If you can fix Readme, please contact me hello@ivanvorobei.by or make Pull Request. I'm willing to pay if need.

## Other Projects

#### [SPIndicator](https://github.com/ivanvorobei/SPIndicator)
Floating indicator, mimicrate to indicator which appear when silent mode turn on / off. Support large texts and has ready-use animatable icons like `done` and `error`.

#### [SPAlert](https://github.com/ivanvorobei/SPAlert)
You can find this alerts in AppStore after feedback or after added song to library in Apple Music. Contains popular Done, Heart presets and many other. Done preset present with draw path animation like original. Also available simple present message without icon. Usage in one line code.

#### [SPPerspective](https://github.com/ivanvorobei/SPPerspective)
Animation of widgets from iOS 14. 3D transform with dynamic shadow. Look [video preview](https://ivanvorobei.by/github/spperspective/video-preview). Available deep customisation 3D and shadow. Also you can use static transform without animation.

#### [SPDiffable](https://github.com/ivanvorobei/SPDiffable)
Simplifies working with animated changes in table and collections. Apple's diffable API required models for each object type. If you want use it in many place, you pass time to implement it and get over duplicates codes. This project help do it elegant with shared models and special cell providers. Support side bar iOS14 and already has native cell providers and views.

#### [SparrowKit](https://github.com/ivanvorobei/SparrowKit)
Collection of native Swift extensions to boost your development. Support tvOS and watchOS.

## Russian Community

В телеграм-канале [Код Воробья](https://sparrowcode.by/telegram) пишу о iOS разработке. Помощь можно найти в [нашем чате](https://sparrowcode.by/telegram/chat).
Видео-туториалы выклыдываю на [YouTube](https://sparrowcode.by/youtube):

[![Tutorials on YouTube](https://cdn.ivanvorobei.by/github/readme/youtube-preview.jpg)](https://sparrowcode.by/youtube)



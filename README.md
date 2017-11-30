![IceCream](https://i.loli.net/2017/11/18/5a104e5acfea5.png)

[![CI Status](http://img.shields.io/travis/caiyue1993/IceCream.svg?style=flat)](https://travis-ci.org/caiyue1993/IceCream)
[![Version](https://img.shields.io/cocoapods/v/IceCream.svg?style=flat)](http://cocoapods.org/pods/IceCream)
[![License](https://img.shields.io/cocoapods/l/IceCream.svg?style=flat)](http://cocoapods.org/pods/IceCream)
[![Platform](https://img.shields.io/cocoapods/p/IceCream.svg?style=flat)](http://cocoapods.org/pods/IceCream)
[![contributions welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat)](https://github.com/caiyue1993/icecream/issues)
<a href="https://twitter.com/caiyue5"><img src="https://img.shields.io/twitter/follow/caiyue5.svg?style=social"></a>

IceCream helps you sync Realm Database with CloudKit.

"It works like magic!"

## Features

- Realm Database
    - [x] Off-line First
    - [x] Thread Safety
    - [x] Reactive Programming

- Apple CloudKit
    - [x] Automatical Authentication
    - [x] Silent Push

- [x] Reachability(Support Long-lived Operation) 
- [x] Error Handling
- [x] Sync Automatically
- [x] Manually Synchronization is also supported
- [x] User Account Status Check
- [ ] Complete Documentation 

## Prerequisite
1. Be sure to have enrolled in Apple Developer Program

2. Turn on your iCloud in Capabilities and choose `CloudKit`

3. Turn on Background Modes and check `Background fetch` and `Remote notification` 

## Usage

### Basics
1. Prepare your Realm Object(e.g. Dog)
```swift
class Dog: Object {
    @objc dynamic var id = NSUUID().uuidString
    @objc dynamic var name = ""
    @objc dynamic var age = 0
    @objc dynamic var isDeleted = false

    override class func primaryKey() -> String? {
        return "id"
    }
}
```

2. Do stuffs like that
```swift
extension Dog: CKRecordConvertible {
    // Yep, leave it blank!    
}

extension Dog: CKRecordRecoverable {
    typealias O = Dog
}
```
Is that easy? Protocol Extensions do this trick.

3. Start the Engine!
```swift
var syncEngine: SyncEngine<Dog>?
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
    ...
    syncEngine = SyncEngine<Dog>()
    application.registerForRemoteNotifications()
    ...
}
```

That's all you need to do! Everytime you write to Realm, the SyncEngine will get notified and handle sync stuffs!

For more details, clone the project to see the source code.

### About Object Deletions

Yep, we highly recommend you use **Soft Deletions**. That's why we add a `isDeleted` property to CKRecordConvertible protocol. 

When you want to delete a object, you just need to set its `isDeleted` property to true. And the rest of things are already taken care of.

*You also don't need to worry about the clean-up things. It has also been considered.*

Example project is provided to see the detailed usage.

## Requirements

- iOS 10.0+
- Swift 4
- Realm Swift ~> 3.0

## Debug Suggestions

It's true that debugging CloudKit is hard and tedious. But I have some tips for you guys when facing puzzles.

- You should know how Realm and CloudKit works. 
- Using GUI tools, like [Realm Browser](https://itunes.apple.com/us/app/realm-browser/id1007457278?mt=12) and [CloudKit Dashboard](https://icloud.developer.apple.com/dashboard).
- When you are lost and don't remember where you are, I suggest starting all over again. In CloudKit Dashboard, "Reset..." button is provided. You can also
clear local database by re-install apps.
- Keep calm and carry on!

*Warning: If you're going to launch your app onto App Store, don't forget to deploy your environment settings to production. You can do it easily in the CloudKit Dashboard. Write & Read permissions are also need to be considered.*

### One More Tip
How to debug CloudKit in production mode? See this [post](https://stackoverflow.com/questions/30182521/use-production-cloudkit-during-development).

## Example

To run the example project, clone the repo, and run `pod install` from the Example directory first.

## Installation

IceCream is available through [CocoaPods](http://cocoapods.org). To install
it, simply add the following line to your Podfile:

```ruby
pod 'IceCream'
```

## Make it better
These are the to-do list in IceCream project. You can join us to become a contributor.

- Support CKReference & Realm's LinkingObjects
- Support CloudKit Shared Database 
- Support Other platforms, like macOS, tvOS and watchOS

See the [CONTRIBUTING](https://github.com/caiyue1993/IceCream/blob/master/CONTRIBUTING.md) file for contributing guidelines.

## Live Demo
My app [小目标 - 量化你的进步](https://itunes.apple.com/cn/app/%E5%B0%8F%E7%9B%AE%E6%A0%87-%E9%87%8F%E5%8C%96%E4%BD%A0%E7%9A%84%E8%BF%9B%E6%AD%A5/id1215312957?mt=8&at=1000lvyQ)(A lightweight task management app) is using IceCream. You can download it and try it on your muiltiple devices to see this magic.

<a href="https://itunes.apple.com/cn/app/%E5%B0%8F%E7%9B%AE%E6%A0%87-%E9%87%8F%E5%8C%96%E4%BD%A0%E7%9A%84%E8%BF%9B%E6%AD%A5/id1215312957?mt=8&at=1000lvyQ">
  <img src="https://github.com/caiyue1993/Tiptoes/blob/master/images/appstore.png">
</a>


If your app has adopted IceCream, feel free to raise a PR to add to this page.

## Donation
Crypto currency donation is the best. Even 0.01 BTC helps😄.
### Bitcoin

![BTC Deposit](https://i.loli.net/2017/11/19/5a11078c118b3.png)

14J7KCR2x1Csh52SpPAvMWRh9EyNX5kxhE

### Lisk
[Lisk](https://lisk.io/) is my preferred crypto currency.

Lisk Deposit Address: 10081270051711082114L

## Reference
- [CloudKit Best Practices](https://developer.apple.com/videos/play/wwdc2016/231/)
- [Synchronizing data with CloudKit](https://medium.com/@guilhermerambo/synchronizing-data-with-cloudkit-94c6246a3fda)
- [Mastering Realm Notifications](https://academy.realm.io/posts/meetup-jp-simard-mastering-realm-notifications/)

## License
IceCream is available under the MIT license. See the LICENSE file for more info.

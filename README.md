<p align="center" >
  <img src="SDWebImage_logo.png" title="SDWebImage logo" float=left>
</p>


[![Build Status](http://img.shields.io/travis/SDWebImage/SDWebImage/master.svg?style=flat)](https://travis-ci.org/SDWebImage/SDWebImage)
[![Pod Version](http://img.shields.io/cocoapods/v/SDWebImage.svg?style=flat)](http://cocoadocs.org/docsets/SDWebImage/)
[![Pod Platform](http://img.shields.io/cocoapods/p/SDWebImage.svg?style=flat)](http://cocoadocs.org/docsets/SDWebImage/)
[![Pod License](http://img.shields.io/cocoapods/l/SDWebImage.svg?style=flat)](https://www.apache.org/licenses/LICENSE-2.0.html)
[![Carthage compatible](https://img.shields.io/badge/Carthage-compatible-4BC51D.svg?style=flat)](https://github.com/SDWebImage/SDWebImage)
[![codecov](https://codecov.io/gh/SDWebImage/SDWebImage/branch/master/graph/badge.svg)](https://codecov.io/gh/SDWebImage/SDWebImage)

这个库提供了一个支持缓存的异步图像下载器。方便起见，我们为这些 UI 元素 `UIImageView`， `UIButton`， `MKAnnotationView` 等添加了分类。

## 功能特点

- [x] `UIImageView`, `UIButton`, `MKAnnotationView` 的分类，用于添加网络图片和缓存管理
- [x] 图片异步下载
- [x] 异步内存+磁盘缓存和自动缓存过期处理
- [x] 后台解压图片
- [x] 同一个 URL 不会被多次下载
- [x] 无效的 url 不会被反复重试
- [x] 不会阻塞主线程
- [x] 高效！
- [x] 使用 GCG 和 ARC

## 支持的图片格式

- UIImage支持的图片格式（JPEG，PNG，……），包括 GIF
- WebP 格式，包动 WebP 动画（使用`WebP`子集）

## 使用要求

- iOS 7.0 及以上
- tvOS 9.0 及以上
- watchOS 2.0 及以上
- macOS 10.9 及以上
- Xcode 7.3 及以上

#### Backwards compatibility

- For iOS 5 and 6, use [any 3.x version up to 3.7.6](https://github.com/rs/SDWebImage/tree/3.7.6)
- For iOS < 5.0, please use the last [2.0 version](https://github.com/rs/SDWebImage/tree/2.0-compat).

## Getting Started

- Read this Readme doc
- Read the [How to use section](https://github.com/rs/SDWebImage#how-to-use)
- Read the [Documentation @ CocoaDocs](http://cocoadocs.org/docsets/SDWebImage/)
- Try the example by downloading the project from Github or even easier using CocoaPods try `pod try SDWebImage`
- Read the [Installation Guide](https://github.com/rs/SDWebImage/wiki/Installation-Guide)
- Read the [SDWebImage 4.0 Migration Guide](Docs/SDWebImage-4.0-Migration-guide.md) to get an idea of the changes from 3.x to 4.x
- Read the [Common Problems](https://github.com/rs/SDWebImage/wiki/Common-Problems) to find the solution for common problems 
- Go to the [Wiki Page](https://github.com/rs/SDWebImage/wiki) for more information such as [Advanced Usage](https://github.com/rs/SDWebImage/wiki/Advanced-Usage)

## Who Uses It
- Find out [who uses SDWebImage](https://github.com/rs/SDWebImage/wiki/Who-Uses-SDWebImage) and add your app to the list.

## Communication

- If you **need help**, use [Stack Overflow](http://stackoverflow.com/questions/tagged/sdwebimage). (Tag 'sdwebimage')
- If you'd like to **ask a general question**, use [Stack Overflow](http://stackoverflow.com/questions/tagged/sdwebimage).
- If you **found a bug**, open an issue.
- If you **have a feature request**, open an issue.
- If you **want to contribute**, submit a pull request.

## How To Use

* Objective-C

```objective-c
#import <SDWebImage/UIImageView+WebCache.h>
...
[imageView sd_setImageWithURL:[NSURL URLWithString:@"http://www.domain.com/path/to/image.jpg"]
             placeholderImage:[UIImage imageNamed:@"placeholder.png"]];
```

* Swift

```swift
import SDWebImage

imageView.sd_setImage(with: URL(string: "http://www.domain.com/path/to/image.jpg"), placeholderImage: UIImage(named: "placeholder.png"))
```

- For details about how to use the library and clear examples, see [The detailed How to use](Docs/HowToUse.md)

## Animated Images (GIF) support

- Starting with the 4.0 version, we rely on [FLAnimatedImage](https://github.com/Flipboard/FLAnimatedImage) to take care of our animated images. 
- If you use cocoapods, add `pod 'SDWebImage/GIF'` to your podfile.
- To use it, simply make sure you use `FLAnimatedImageView` instead of `UIImageView`.
- **Note**: there is a backwards compatible feature, so if you are still trying to load a GIF into a `UIImageView`, it will only show the 1st frame as a static image by default. However, you can enable the full GIF support by using the built-in GIF coder. See [GIF coder](https://github.com/rs/SDWebImage/wiki/Advanced-Usage#gif-coder)
- **Important**: FLAnimatedImage only works on the iOS platform. For macOS, use `NSImageView` with `animates` set to `YES` to show the entire animated images and `NO` to only show the 1st frame. For all the other platforms (tvOS, watchOS) we will fallback to the backwards compatibility feature described above 

## Installation

There are three ways to use SDWebImage in your project:
- using CocoaPods
- using Carthage
- by cloning the project into your repository

### Installation with CocoaPods

[CocoaPods](http://cocoapods.org/) is a dependency manager for Objective-C, which automates and simplifies the process of using 3rd-party libraries in your projects. See the [Get Started](http://cocoapods.org/#get_started) section for more details.

#### Podfile
```
platform :ios, '7.0'
pod 'SDWebImage', '~> 4.0'
```

If you are using Swift, be sure to add `use_frameworks!` and set your target to iOS 8+:
```
platform :ios, '8.0'
use_frameworks!
```

#### Subspecs

There are 4 subspecs available now: `Core`, `MapKit`, `GIF` and `WebP` (this means you can install only some of the SDWebImage modules. By default, you get just `Core`, so if you need `WebP`, you need to specify it). 

Podfile example:
```
pod 'SDWebImage/WebP'
```

### Installation with Carthage (iOS 8+)

[Carthage](https://github.com/Carthage/Carthage) is a lightweight dependency manager for Swift and Objective-C. It leverages CocoaTouch modules and is less invasive than CocoaPods.

To install with carthage, follow the instruction on [Carthage](https://github.com/Carthage/Carthage)

#### Cartfile
```
github "rs/SDWebImage"
```

### Installation by cloning the repository
- see [Manual install](Docs/ManualInstallation.md)

### Import headers in your source files

In the source files where you need to use the library, import the header file:

```objective-c
#import <SDWebImage/UIImageView+WebCache.h>
```

### Build Project

At this point your workspace should build without error. If you are having problem, post to the Issue and the
community can help you solve it.

## Author
- [Olivier Poitrey](https://github.com/rs)

## Collaborators
- [Konstantinos K.](https://github.com/mythodeia)
- [Bogdan Poplauschi](https://github.com/bpoplauschi)
- [Chester Liu](https://github.com/skyline75489)
- [DreamPiggy](https://github.com/dreampiggy)

## Licenses

All source code is licensed under the [MIT License](https://raw.github.com/rs/SDWebImage/master/LICENSE).

## Architecture

<p align="center" >
    <img src="Docs/SDWebImageClassDiagram.png" title="SDWebImage class diagram">
</p>

<p align="center" >
    <img src="Docs/SDWebImageSequenceDiagram.png" title="SDWebImage sequence diagram">
</p>

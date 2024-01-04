# Purpose of the mimik Client Library Trial

The purpose of the mimik Client Library is to provide a programmatic way to work with the edgeEngine Runtime to access information about the mobile device on which the application is running, as well as mobile devices running within a cluster of mobile devices that are hosting the edgeEngine Runtime. Also, to allow developers to use edge microservices running within a particular cluster.

By leveraging the Core component of the mimik Client Library, developers can build applications compatible with the edgeEngine Runtime. This not only harnesses the strength of edge computing but also provides an inherent flexibility in its paradigm.

Additionally, this component provides utility APIs that help developers with core operations such as Authentication, edgeEngine Runtime Setup, deployment of edge microservices and handling of Network calls.

Furthermore, the mimik Client Library Engine component provides additional edgeEngine Runtime utility APIs, as well as vendoring the actual edgeEngine Runtime binary into the iOS project.


# Purpose of the Core and Engine components of the mimik Client Library Trial

The edgeEngine Runtime is a compiled binary that's intended to run on actual devices.

The reason for having the mimik Client Library split into its [Core](https://github.com/mimikgit/cocoapod-EdgeCore) and [Engine](https://github.com/mimikgit/cocoapod-EdgeEngine) components is to give developers the choice of having the edgeEngine Runtime bundled in within the iOS application or to have it running on a host platform of their own choosing (ie. macOS, Linux, Windows, etc.)

Normally, when the developers intend to run their iOS application on iOS devices, the mimik Client Library Engine can be used to facilitate the integration of the edgeEngine Runtime binary directly within the iOS application bundle.

However, in order for developers to be able to run their iOS application in an [iOS Simulator](https://developer.apple.com/documentation/xcode/running-your-app-in-simulator-or-on-a-device) or through a [Mac Catalyst](https://developer.apple.com/mac-catalyst/) translation layer, it is necessary for the edgeEngine Runtime to be running on a host platform outside of the iOS application.


# mimik Client Library Trial Content

By importing the EdgeClientLibrary cocoapod into your iOS project, you will be automatically importing the following cocoapods as its dependencies:

  - [EdgeCore](https://github.com/mimikgit/cocoapod-EdgeCore)
  - [EdgeEngineTrial](https://github.com/mimikgit/cocoapod-EdgeEngineTrial)
  - [EdgeUser](https://github.com/mimikgit/cocoapod-EdgeUser)


## Supported Platforms, Targets

* `iOS Devices running iOS 15+`


## iOS Simulator support

For more information about iOS Simulator support see this [article](https://devdocs.mimik.com/tutorials/12-index#workingwithaniossimulator)


## Requirements
```
iOS 15.0+
```


## Installation

To install it, simply add the following lines to your Podfile:


```swift
platform :ios, '15.0'
source 'https://github.com/CocoaPods/Specs.git'
source 'https://github.com/mimikgit/cocoapod-edge-specs.git'

use_frameworks!
inhibit_all_warnings!

def mimik
  pod 'EdgeClientLibraryTrial'
end

target '{target}' do
  mimik()
end

post_install do |installer|
  installer.pods_project.targets.each do |target|
    target.build_configurations.each do |config|
      config.build_settings['ENABLE_BITCODE'] = 'NO'
      config.build_settings['VALID_ARCHS'] = '$(ARCHS_STANDARD_64_BIT)'
      config.build_settings['IPHONEOS_DEPLOYMENT_TARGET'] = '15.0'
      config.build_settings['BUILD_LIBRARY_FOR_DISTRIBUTION'] = 'YES'
    end
  end
end
```


# More Information

* [Integrating](https://devdocs.mimik.com/tutorials/11-index) mimik Client Library into an iOS project
* Working with [edgeEngine](https://devdocs.mimik.com/tutorials/12-index) in an iOS project
* Working with [edge microservices](https://devdocs.mimik.com/tutorials/13-index) in an iOS project


# Key Concepts

In order to get the full benefit of this document, the intended readers should be familiar with the following:

* Understanding the Fundamentals of the [edgeEngine Runtime](https://devdocs.mimik.com/key-concepts/01-index)
* Understanding [edgeEngine Images and Containers](https://devdocs.mimik.com/key-concepts/02-index)
* The basics of using an [edgeEngine Tokens](https://devdocs.mimik.com/key-concepts/03-index) to access and work with the edgeEngine Runtime

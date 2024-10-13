<p><h1 align="left">SVGView</h1></p>

<p><h4>This is a fork of Exyte's SVG parser written in SwiftUI</h4></p>

[![](https://img.shields.io/endpoint?url=https%3A%2F%2Fswiftpackageindex.com%2Fapi%2Fpackages%2Fexyte%2FSVGView%2Fbadge%3Ftype%3Dswift-versions)](https://swiftpackageindex.com/exyte/SVGView)
[![](https://img.shields.io/endpoint?url=https%3A%2F%2Fswiftpackageindex.com%2Fapi%2Fpackages%2Fexyte%2FSVGView%2Fbadge%3Ftype%3Dplatforms)](https://swiftpackageindex.com/exyte/SVGView)
[![SPM Compatible](https://img.shields.io/badge/SwiftPM-Compatible-brightgreen.svg)](https://swiftpackageindex.com/exyte/SVGView)
[![Cocoapods Compatible](https://img.shields.io/badge/cocoapods-Compatible-brightgreen.svg)](https://cocoapods.org/pods/SVGView)
[![Carthage Compatible](https://img.shields.io/badge/Carthage-compatible-brightgreen.svg?style=flat)](https://github.com/Carthage/Carthage)
[![License: MIT](https://img.shields.io/badge/License-MIT-black.svg)](https://opensource.org/licenses/MIT)

# Overview

This is a fork of Exyte's SVGViewer repository, which adds properties that make it easier and more powerful to interact with SwiftUI Paths. The original project brings the power of SVG to Apple platforms, by parsing SVG files and representing their content in SwiftUI.

# Usage

Get started with `SVGView` in a few lines of code:

```Swift
struct ContentView: View {
    var body: some View {
        SVGView(contentsOf: Bundle.main.url(forResource: "example", withExtension: "svg")!)
    }
}
```

## Additional properties

This fork in particular adds additional properties to the rendered paths to animate their trim and control the stroke of the path.

```Swift
struct ContentView: View {
    var body: some View {
        let view = SVGView(contentsOf: Bundle.main.url(forResource: "example", withExtension: "svg")!)
        if let part = view.getNode(byId: id) {
            part.trimTo = 0  // Set the trimTo to 0, so it can be animated to 1 for a "drawn in" effect
            part.pathStroke = SVGStroke(fill: SVGColor(uiColor: .label), width: 5, cap: .round) // Set the property of the Path stroke, using uiColor with an SVGColor extension
        }
        return view
    }
}
```



## Customization

You can change various parameters for the nodes like this:

```Swift
let circle = SVGCircle(cx: 30, cy: 30, r: 30)
circle.fill = SVGColor.black
circle.stroke = SVGStroke(fill: SVGColor(hex: "ABCDEF"), width: 2)
circle.onTapGesture {
    print("tap")
}
```

## Interact with vector elements

You may locate the desired part of your SVG file using standard identifiers to add gestures and change its properties in runtime:

```Swift
struct ContentView: View {
    var body: some View {
        let view = SVGView(contentsOf: Bundle.main.url(forResource: "example", withExtension: "svg")!)
        if let part = view.getNode(byId: "part") {
            part.onTapGesture {
                part.opacity = 0.2
            }
        }
        return view
    }
}
```

## Animation

You can use standard SwiftUI tools to animate your image:

```Swift
if let part = view.getNode(byId: "part") {
    part.onTapGesture {
        withAnimation {
            part.opacity = 0.2
        }
    }
}
```

## Complex effects

SVGView makes it easy to add custom effects to your app. For example, make this <a href="https://www.iconfinder.com/icons/1337497/">pikachu</a> track finger movement:

```Swift
var body: some View {
    let view = SVGView(contentsOf: Bundle.main.url(forResource: "pikachu", withExtension: "svg")!)
    let delta = CGAffineTransform(translationX: getEyeX(), y: 0)
    view.getNode(byId: "eye1")?.transform = delta
    view.getNode(byId: "eye2")?.transform = delta

    return view.gesture(DragGesture().onChanged { g in
        self.x = g.location.x
    })
}
```

<img src="https://i.imgur.com/Ij0Xn4A.gif" width="300" height="300">

# SVG Tests Coverage

Our mission is to provide 100% support of all SVG standards: 1.1 (Second Edition), Tiny 1.2 and 2.0. However, this project is at its very beginning, so you can follow our progress on <a href="w3c-coverage.md">this page</a>. You can also check out <a href="https://github.com/exyte/SVGViewTests">SVGViewTests project</a> to see how well this framework handles every single SVG test case.

# Installation

## Swift Package Manager

```swift
dependencies: [
    .package(url: "https://github.com/exyte/SVGView.git")
]
```

## CocoaPods

```ruby
pod 'SVGView'
```

## Carthage

```ogdl
github "Exyte/SVGView"
```

# Requirements

* iOS 14+ / watchOS 7+ / macOS 11+
* Xcode 12+

## Our other open source SwiftUI libraries
[PopupView](https://github.com/exyte/PopupView) - Toasts and popups library    
[Grid](https://github.com/exyte/Grid) - The most powerful Grid container    
[ScalingHeaderScrollView](https://github.com/exyte/ScalingHeaderScrollView) - A scroll view with a sticky header which shrinks as you scroll    
[AnimatedTabBar](https://github.com/exyte/AnimatedTabBar) - A tabbar with a number of preset animations   
[MediaPicker](https://github.com/exyte/mediapicker) - Customizable media picker     
[Chat](https://github.com/exyte/chat) - Chat UI framework with fully customizable message cells, input view, and a built-in media picker  
[OpenAI](https://github.com/exyte/OpenAI) Wrapper lib for [OpenAI REST API](https://platform.openai.com/docs/api-reference/introduction)    
[AnimatedGradient](https://github.com/exyte/AnimatedGradient) - Animated linear gradient     
[ConcentricOnboarding](https://github.com/exyte/ConcentricOnboarding) - Animated onboarding flow    
[FloatingButton](https://github.com/exyte/FloatingButton) - Floating button menu    
[ActivityIndicatorView](https://github.com/exyte/ActivityIndicatorView) - A number of animated loading indicators    
[ProgressIndicatorView](https://github.com/exyte/ProgressIndicatorView) - A number of animated progress indicators    
[FlagAndCountryCode](https://github.com/exyte/FlagAndCountryCode) - Phone codes and flags for every country    
[LiquidSwipe](https://github.com/exyte/LiquidSwipe) - Liquid navigation animation    


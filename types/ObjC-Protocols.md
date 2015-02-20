---
nav-title: "Objective-C Protocols"
title: "Objective-C Protocols"
description: "Describes how Objective-C protocols are exposed."
position: 0
---

# Objective-C Protocols
Objective-C protocols describe an API Objective-C classes may implement. JavaScript does not have a matching counterpart. For every Objective-C Protocol we expose a JavaScript object that identifies the protocol.

For example given the following Objective-C declarations:
```objective-c
@protocol MyProtocol
- (void)helloWorld;
@end

@interface MyClass : NSObject <MyProtocol>
@end
```

Will be exposed as:
```javascript
console.log(MyClass.conformsToProtocol(MyProtocol)); // true

var instance = MyClass.alloc().init();
console.log(instance.conformsToProtocol(MyProtocol)); // true
instance.helloWorld();
```

These objects can be used in the extension API to create derived Objective-C classes that implement the protocols:
```javascript
var protocol = NSProtocolFromString("MyProtocol");
console.log(NSStringFromProtocol(protocol)); // "MyProtocol"
console.log(protocol === MyProtocol); // true
```

In case of conflicts with other types, the name has the `Protocol` suffix.
```javascript
var klass = NSObject;
var protocol = NSObjectProtocol;
```
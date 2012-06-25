JSReachability
==============

Easy to use class for iOS to asynchronously monitor the reachability of a host using a delegate or the Notification Center.

Usage
==============

- **Get a reachability object** calling the class method:

```objc
JSReachability *reachability = [JSReachability reachabilityWithHost:@"myhost.com" delegate:self];
```

optionally with a delegate. You can **pass nil**, and register to changes to changes in the reachability to the host **using the notifications**:

```
extern NSString * const kJSReachabilityHostDidBecomeReachableNotification;
extern NSString * const kJSReachabilityHostDidBecomeUnReachableNotification;
```

or **pass ```self``` as the delegate** and implement this method from the ```JSReachabilityDelegate``` protocol:

```objc
- (void)reachabilityService:(JSReachability *)reachability host:(NSString *)host didBecomeReachable:(BOOL)reachable;
```

- **Call start** and it will start monitoring **asynchronously** the host to check for changes in the reachability (for example, if the device internet connectivity goes up or down)

```objc
[reachability start];
```

Dependencies
==============

JSReachability requires your application to be linked against the ```SystemConfiguration.framework``` framework.

License
==============
Copyright 2012 [Javier Soto](http://twitter.com/javisoto) (ios@javisoto.es)

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
 limitations under the License. 

Attribution is not required, but appreciated.
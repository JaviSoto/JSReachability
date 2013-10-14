## JSReachability
Easy to use iOS class to asynchronously monitor the reachability of a host.

This allows you to **know at any given time** not only **whether the iPhone / iPad is connected to the internet**, but also if that connection is working.
You can check for the *reachability* of internet in general, or of your own backend server, and that way you can **detect also if the API the app connects to is down**.

## Usage
- **Get a reachability object** calling the class method:

```objc
JSReachability *reachability = [[JSReachability reachabilityWithHost:@"myhost.com" delegate:self] retain];
```

or if you don't want to specify a host:

```objc
JSReachability *reachability = [[JSReachability reachabilityForInternetConnectionWithDelegate:self] retain];
```

- You can **pass nil as the delegate**, and register to changes to changes in the reachability to the host **using the ```NSNotificationCenter```**:

```
extern NSString * const kJSReachabilityHostReachabilityDidChangeNotification;
```

like this:

```objc
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(hostReachabilityChanged:) name:kJSReachabilityHostReachabilityDidChangeNotification object:reachability];
```

and then implement the method to check the new value:

```objc
- (void)hostReachabilityChanged:(NSNotification *)note
{
	JSReachability *reachability = note.object;

	BOOL hostIsReachable = reachability.hostIsReachable;

	// Do something with hostIsReachable
}
```

- Or **pass ```self``` as the delegate** and implement this method from the ```JSReachabilityDelegate``` protocol:

```objc
- (void)reachability:(JSReachability *)reachability host:(NSString *)host didBecomeReachable:(BOOL)reachable;
```

- Then **call start** and it will start monitoring **asynchronously** the host to check for changes in the reachability (for example, if the device internet connectivity goes up or down)

```objc
[reachability start];
```

## Dependencies
JSReachability requires your application to be linked against the ```SystemConfiguration.framework``` framework.

## ARC Support
```JSReachability``` doesn't support ARC at the moment. If you want to integrate it in your ARC project, simply add the ```-fno-objc-arc``` linker option to the ```JSReachability.m``` file. [Quick tutorial](http://maniacdev.com/2012/01/easily-get-non-arc-enabled-open-source-libraries-working-in-arc-enabled-projects/)

## License
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

[![Bitdeli Badge](https://d2weczhvl823v0.cloudfront.net/JaviSoto/jsreachability/trend.png)](https://bitdeli.com/free "Bitdeli Badge")


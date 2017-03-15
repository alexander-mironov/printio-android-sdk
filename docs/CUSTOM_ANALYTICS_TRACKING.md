Custom Analytics Tracking
===============

Since version 3.2.8 there is an option to set custom analytics tracking mechanism to the SDK.  
In version 3.3.0 this mechanism has been updated. 

Version 3.3.14 adds an additional method `trackItem()` for tracking Items within Transactions. 

## AnalyticsTracker interface

The core of custom analytics tracking is `AnalyticsTracker` interface located in `print.io.analytics` package. It is an interface for object used to track user behaviour in the SDK. `AnalyticsTracker` interface exposes four methods `trackAction()`, `trackScreenView()`, `trackTransaction()` and `trackItem()` which are called whenever the user performs a trackable event. These events could be screen views, various button clicks, etc...

Classes implementing AnalyticsTracker interface must be serializable. More precisely, SDK will use Gson library for serialization and deserialization. 

To simplify usage of the SDK, we have already implemented AnalyticsTracker for Google Analytics service. You can use this implementation as your tracking mechanism or if you want to develop your own AnalyticsTracker you can use this implementation as a reference. Mentioned implementation is `print.io.analytics.impl.GoogleAnalyticsTracker`.  

To use our default implementation of Google Analytics, create an instance of `GoogleAnalyticsTracker` and add it to your config:
```java
//import print.io.analytics.impl.GoogleAnalyticsTracker;

GoogleAnalyticsTracker tracker = new GoogleAnalyticsTracker("YOUR_GA_CLIENT_ID");
config.setAnalyticsTracker(tracker);
```

## Events

Event is passed to appropriate `track` method every time the user performs a trackable action. All events implement `print.io.analytics.BaseEvent` interface.

#### Event types
We recognize three different types of events.

 - `print.io.analytics.ScreenViewEvent` - For tracking screen views
 - `print.io.analytics.ActionEvent` - For tracking various user actions
 - `print.io.analytics.TransactionEvent` - For tracking purchases
 - `print.io.analytics.ItemEvent` - For tracking individual items in a transaction (matched by transactionID)

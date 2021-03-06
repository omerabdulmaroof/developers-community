---
pagename: LivePerson Callbacks Interface
redirect_from:
  - android-callbacks-interface.html
Keywords:
sitesection: Documents
categoryname: "Messaging Channels"
documentname: Mobile App Messaging SDK for Android
subfoldername: Configuration

order: 30
permalink: mobile-app-messaging-sdk-for-android-configuration-liveperson-callbacks-interface.html

indicator: messaging
---

The SDK provides a callback mechanism to keep the host app updated on events related to the conversation. There are two ways to register to LivePerson events via Local Intents (Recommended) or via Callbacks.

### Local Intents

Using Local Intents, you can register to a specific Action or to all of them. All the Actions are defined in the `LivePersonIntents.ILivePersonIntentAction` Interface. All the additional data provided using Extras on the intents is defined in the ``LivePersonIntents.ILivePersonIntentExtras`` Interface.

LivePersonIntents class provides several methods that help get the data out of the intent, without dealing with the Extras. For a full list of all possible Intents, click [here](android-callbacks-index.html#livepersonintents).

To easily register to all the intent Actions, we provide an `IntentFilter` that contains them all in `LivePersonIntents.getIntentFilterForAllEvents()`.

**Note**: These Intents are local only and must by registered via LocalBroadcastManager.

To register `BroadcastReceiver` for all Intents, use this code::

```java
LocalBroadcastManager.getInstance(
  getApplicationContext()).registerReceiver(<your receiver>,
  LivePersonIntents.getIntentFilterForAllEvents()
);
```

To register `BroadcastReceiver` for a specific set of Intents, use this example:

```java
IntentFilter filter = new IntentFilter();
filter.addAction(LivePersonIntents.ILivePersonIntentAction.LP_ON_AGENT_DETAILS_CHANGED_INTENT_ACTION);
filter.addAction(LivePersonIntents.ILivePersonIntentAction.LP_ON_CONVERSATION_RESOLVED_INTENT_ACTION);

LocalBroadcastManager.getInstance(
  getApplicationContext()).registerReceiver(<your receiver>,filter
);
```

Then,to catch the Broadcast:



```java
BroadcastReceiver <your receiver> = new BroadcastReceiver(){
  @Override
  public void onReceive(Context context, Intent intent) {
    Log.d(TAG, "Got LP intent event with action " + intent.getAction());
    switch (intent.getAction()){
      //handle the relevant actions from LivePersonIntents.ILivePersonIntentAction
      ...
    }
  }
};
```

**Note**: if you registered for multiple **Intents**, you'll have to filter each one, using a **switch**.

### Callbacks

To register the callback call:

```java
public static void setCallback(final LivePersonCallback listener)
```

To remove a callback call:

```java
public static void removeCallBack()
```

Click [here](android-callbacks-index.html) for more information.

---
id: version-0.60-backhandler
title: BackHandler
original_id: backhandler
---

Detect hardware button presses for back navigation.

Android: Detect hardware back button presses, and programmatically invoke the default back button functionality to exit the app if there are no listeners or if none of the listeners return true.

tvOS: Detect presses of the menu button on the TV remote. (Still to be implemented: programmatically disable menu button handling functionality to exit the app if there are no listeners or if none of the listeners return true.)

iOS: Not applicable.

The event subscriptions are called in reverse order (i.e. last registered subscription first), and if one subscription returns true then subscriptions registered earlier will not be called.

Example:

```javascript
BackHandler.addEventListener('hardwareBackPress', function() {
  // this.onMainScreen and this.goBack are just examples, you need to use your own implementation here
  // Typically you would use the navigator here to go to the last state.

  if (!this.onMainScreen()) {
    this.goBack();
    return true;
  }
  return false;
});
```

Lifecycle example:

```javascript
  componentDidMount() {
    this.backHandler = BackHandler.addEventListener('hardwareBackPress', this.handleBackPress);
  }

  componentWillUnmount() {
    this.backHandler.remove()
  }

  handleBackPress = () => {
    this.goBack(); // works best when the goBack is async
    return true;
  }
```

Lifecycle alternative:

```javascript
  componentDidMount() {
    this.backHandler = BackHandler.addEventListener('hardwareBackPress', () => {
      this.goBack(); // works best when the goBack is async
      return true;
    });
  }

  componentWillUnmount() {
    this.backHandler.remove();
  }
```

### Methods

- [`addEventListener`](backhandler.md#addeventlistener)
- [`exitApp`](backhandler.md#exitapp)
- [`removeEventListener`](backhandler.md#removeeventlistener)

---

# Reference

## Methods

### `addEventListener()`

```javascript
static addEventListener(eventName, handler)
```

---

### `exitApp()`

```javascript
static exitApp()
```

---

### `removeEventListener()`

```javascript
static removeEventListener(eventName, handler)
```

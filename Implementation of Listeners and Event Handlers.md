# Implementation of Listeners and Event Handlers

### Swift
Apps receive and handle events using responder objects. A responder object is any instance of the UIResponder class, and common subclasses include UIView, UIViewController, and UIApplication. Responders receive the raw event data and must either handle the event or forward it to another responder object. When your app receives an event, UIKit automatically directs that event to the most appropriate responder object, known as the first responder. Unhandled events are passed from responder to responder in the active responder chain, which is a dynamic configuration of your app’s responder objects. There is no single responder chain within your app. UIKit defines default rules for how objects are passed from one responder to the next, but you can always change those rules by overriding the appropriate properties in your responder objects.Figure 1 shows the default responder chains in an app whose interface contains a label, a text field, a button, and two background views. If the text field does not handle an event, UIKit sends the event to the text field’s parent UIView object, followed by the root view of the window. From the root view, the responder chain diverts to the owning view controller before directing the event to the window. If the window does not handle the event, UIKit delivers the event to the UIApplication object, and possibly to the app delegate if that object is an instance of UIResponder and not already part of the responder chain.
![ALt Text](https://docs-assets.developer.apple.com/published/7c21d852b9/f17df5bc-d80b-4e17-81cf-4277b1e0f6e4.png)
### Kotlin
Event listeners/handlers are similar to those in Java. In Kotlin anonymous classes (lambdas can be used for these) and named classes can be used as listeners in Kotlin:
```Kotlin
cancelImage.setOnClickListener(object : View.OnClickListener { //1
    override fun onClick(v: View?) { // 2
        dismiss()
    }
})
```

```Kotlin
class OnCancelSnackListener(
    val snackbar: Snackbar
): View.OnClickListener {
    override fun onClick(v: View?) {
        snackbar.dismiss()
    }
}
```
Lambda expression example:
```Kotlin
cancelImage.setOnClickListener { dismiss() }
```



---

# addEventListener_method

This method allows the registration of event listeners on the event target. If an EventListener is added to an EventTarget while it is processing an event, it will not be triggered by the current actions but may be triggered during a later stage of event flow, such as the bubbling phase.

If multiple identical EventListener s are registered on the same EventTarget with the same parameters the duplicate instances are discarded. They do not cause the EventListener to be called twice and since they are discarded they do not need to be removed with the removeEventListener method.



---

# dispatchEvent_method

This method allows the dispatch of events into the implementations event model. Events dispatched in this manner will have the same capturing and bubbling behavior as events dispatched directly by the implementation. The target of the event is the EventTarget on which dispatchEvent is called.



---

# removeEventListener_method

This method allows the removal of event listeners from the event target. If an EventListener is removed from an EventTarget while it is processing an event, it will not be triggered by the current actions. EventListener s can never be invoked after being removed.

Calling removeEventListener with arguments which do not identify any currently registered EventListener on the EventTarget has no effect.
---
title: ifPerfetto
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
## Implemented by

| Name                             | Description                                                                                                                                                                      |
| :------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [roPerfetto](doc:roperfetto)     | Adds custom events and heap graph captures to a Perfetto trace of your app.                                                                                                      |

> The ifPerfetto methods record events only when tracing is enabled for the app and a trace is being captured. For the requirements and the steps to enable and record a trace, see [Roku app tracing (with Perfetto)](doc:app-tracing).
>
> Perfetto tracing is available only for apps that run as a process. For a sideloaded app, set `run_as_process=1` in the manifest.

## Supported methods

### BeginEvent(name as String, params as Object) as Void

_Available since Roku OS 15.1_

##### Description

Records the start of an event that has a duration, such as a long function. Call [endEvent()](#endevent-as-void) to record the end of the event.

##### Parameters

| Name   | Type               | Description                                                                                          |
| :----- | :----------------- | :--------------------------------------------------------------------------------------------------- |
| name   | String             | The name of the event in the trace.                                                                  |
| params | roAssociativeArray | Key-value pairs to attach to the event. In the Perfetto UI, select the event to view these values. |

##### Return Value

None.

##### Example

```brightscript
sub myfunc()
    tracer = CreateObject("roPerfetto")
    params = {debug_1: 42, debug_2: "hello"}
    tracer.beginEvent("my_duration_event", params)
    do_stuff()
    tracer.endEvent()
end sub
```

### CaptureHeapGraph(name as String) as Void

_Available since Roku OS 15.2_

##### Description

Captures a heap graph of the BrightScript and SceneGraph objects in your app at the time of the call. You can use heap graphs to find which objects use the most memory, which objects are kept alive longer than expected, and what keeps them alive.

Call captureHeapGraph() while a trace is being recorded. If no websocket client is attached to receive the trace, the heap graph is not recorded. You can capture more than one heap graph in a single trace, for example to compare memory use before and after an operation. Each heap graph appears in the Perfetto UI as a selectable **Heap Profile** event. See [Capturing heap graphs](doc:app-tracing#capturing-heap-graphs).

Each capture takes a couple of seconds to write to the trace, and the call does not return until the capture is complete.

##### Parameters

| Name | Type   | Description                                                                                                                              |
| :--- | :----- | :--------------------------------------------------------------------------------------------------------------------------------------- |
| name | String | A name that identifies the heap graph. In the current release, this value is ignored and is not included in the captured trace. |

##### Return Value

None.

##### Example

```brightscript
tracer = CreateObject("roPerfetto")
tracer.captureHeapGraph("my-heap-graph")
```

### CreateScopedEvent(name as String, params as Object) as Object

_Available since Roku OS 15.1_

##### Description

Records the start of an event that has a duration. Unlike [beginEvent()](#beginevent-name-as-string-params-as-object-as-void), you do not call a method to end the event. The end of the event is recorded automatically when the returned object is released.

Keep a reference to the returned object for as long as you want to measure. If the object is released earlier, for example when the variable that holds it goes out of scope, the event ends at that point.

##### Parameters

| Name   | Type               | Description                                                                                          |
| :----- | :----------------- | :--------------------------------------------------------------------------------------------------- |
| name   | String             | The name of the event in the trace.                                                                  |
| params | roAssociativeArray | Key-value pairs to attach to the event. In the Perfetto UI, select the event to view these values. |

##### Return Value

An object that represents the scope of the event. The event ends when this object is released.

##### Example

```brightscript
sub myfunc()
    tracer = CreateObject("roPerfetto")
    params = {debug_1: 42, debug_2: "hello"}
    scoped_event = tracer.createScopedEvent("my_scoped_event", params)
    do_stuff()
    ' The end of the event is recorded when scoped_event is released.
end sub
```

### EndEvent() as Void

_Available since Roku OS 15.1_

##### Description

Records the end of the event started by the most recent call to [beginEvent()](#beginevent-name-as-string-params-as-object-as-void).

##### Return Value

None.

### FlowEvent(flowId as Integer, name as String) as Void

_Available since Roku OS 15.1_

##### Description

Records an event that belongs to a flow. A flow connects events in different parts of your code, for example from a Task thread to the render thread, so that you can follow the work across threads in the Perfetto UI.

Call flowEvent() with the same flow ID in each place the flow passes through. End the flow with [terminateFlow()](#terminateflow-flowid-as-integer-name-as-string-as-void).

##### Parameters

| Name   | Type    | Description                                                                |
| :----- | :------ | :------------------------------------------------------------------------- |
| flowId | Integer | A unique unsigned integer that you choose to identify the flow.            |
| name   | String  | The name of the event in the trace.                                        |

##### Return Value

None.

### InstantEvent(name as String) as Void

_Available since Roku OS 15.1_

##### Description

Records an event that has no duration, such as a key press.

##### Parameters

| Name | Type   | Description                         |
| :--- | :----- | :---------------------------------- |
| name | String | The name of the event in the trace. |

##### Return Value

None.

##### Example

```brightscript
tracer = CreateObject("roPerfetto")
tracer.instantEvent("my_instant_event")
```

### InstantEvent(name as String, params as Object) as Void

_Available since Roku OS 15.1_

##### Description

Records an event that has no duration, and attaches additional data to the event.

##### Parameters

| Name   | Type                  | Description                                                                                          |
| :----- | :-------------------- | :--------------------------------------------------------------------------------------------------- |
| name   | String                | The name of the event in the trace.                                                                  |
| params | roAssociativeArray    | Key-value pairs to attach to the event. In the Perfetto UI, select the event to view these values. |

##### Return Value

None.

##### Example

```brightscript
tracer = CreateObject("roPerfetto")
tracer.instantEvent("my_instant_event", {debug_1: 42, debug_2: "hello"})
```

### TerminateFlow(flowId as Integer, name as String) as Void

_Available since Roku OS 15.1_

##### Description

Records the final event of a flow and ends the flow.

##### Parameters

| Name   | Type    | Description                                                     |
| :----- | :------ | :-------------------------------------------------------------- |
| flowId | Integer | The unique unsigned integer that identifies the flow to end.    |
| name   | String  | The name of the event in the trace.                             |

##### Return Value

None.

##### Example

```brightscript
sub func1()
    flowId = 42 ' A unique unsigned integer that you choose
    tracer = CreateObject("roPerfetto")
    tracer.flowEvent(flowId, "my_flow_event_1")
end sub

sub func2()
    flowId = 42
    tracer = CreateObject("roPerfetto")
    tracer.flowEvent(flowId, "my_flow_event_2")
end sub

sub func3()
    flowId = 42
    tracer = CreateObject("roPerfetto")
    tracer.terminateFlow(flowId, "my_flow_event_3")
end sub
```

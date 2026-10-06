# SMSHub Login Load Test: Evaluating Activation Performance at Higher Volumes

Performance changes when the workload changes.

A single activation is relatively easy to monitor. A larger group introduces concurrent requests, different delivery times, multiple pending states, and more complicated error handling.

For an SMSHub Login performance test, the main objective should therefore be to understand how the activation workflow behaves as the number of simultaneous requests increases.

## Establishing the Starting Point

Every load test needs a baseline.

Begin with a relatively small workload and document the normal timing for each stage of the activation.

The baseline should answer a few basic questions:

* How quickly is a request created?
* How long does number assignment take?
* When does the SMS arrive?
* How long until completion?

These results become the reference for higher workloads.

## Moving From One Request to Many

The next step is to introduce concurrency.

Instead of sending a large batch immediately, increase the number of active requests in stages.

This can reveal when performance begins to change.

For example, the initial workload may show consistent delivery, while a larger group may produce greater variation in SMS arrival times.

The transition itself is useful information.

## Watch the Queue, Not Just the Average

A large activation workload can contain many different states simultaneously.

Some requests may have just been created. Others may already be waiting for an SMS, while another group may have completed.

A monitoring system should make these states visible.

Otherwise, a high number of pending requests can look like one generic performance problem even when the individual workflows are progressing normally.

## Measuring Concurrency

Concurrency should be treated as one of the main test variables.

For each workload level, record the number of simultaneously active requests and compare it with:

* Assignment time
* SMS delivery time
* Completion percentage
* Expiration frequency
* Error count

This makes it possible to see whether higher concurrency is associated with measurable changes.

## Request Timing Needs More Detail

Total duration is useful but incomplete.

Break the workflow into stages:

**Request creation → Assignment**

**Assignment → SMS**

**SMS → Completion**

This allows the test to identify which part of the workflow changes as the workload grows.

If only the final duration is recorded, important differences can disappear inside the overall average.

## Handling Out-of-Order Results

Concurrent requests rarely finish in perfect sequence.

The activation created first may be completed after several later requests.

This means every request needs a unique identifier.

The identifier should connect the activation with all relevant timestamps and status changes.

This prevents one request's SMS or completion event from being accidentally associated with another request.

## Failure Isolation

Large-scale testing should not treat an entire batch as one result.

If one request fails, the remaining requests should retain their own statuses.

This is important for both accurate reporting and automated recovery.

A load test should therefore preserve request-level results even when many activations are running simultaneously.

## Monitoring Automation Errors

There are two different types of problems to watch.

The first involves the activation workflow itself.

The second comes from the software managing that workflow.

An automation layer might experience a timeout or fail to process a response correctly even when the underlying activation is still active.

These cases should be logged separately.

Otherwise, the performance report may incorrectly attribute every problem to the service being tested.

## A Useful Load-Test Record

A structured dataset could contain:

| Data point           | Why it matters               |
| -------------------- | ---------------------------- |
| Workload size        | Defines test level           |
| Request ID           | Tracks individual activation |
| Creation timestamp   | Establishes start            |
| Assignment timestamp | Measures allocation          |
| SMS timestamp        | Measures delivery            |
| Final state          | Defines outcome              |
| Error type           | Classifies failures          |
| Retry count          | Tracks recovery              |

With this structure, results from different workload levels can be compared directly.

## Looking for Saturation

The purpose of increasing the workload is not simply to find a maximum number.

More useful is identifying when the behavior starts to change.

Possible signals include:

* Increasing delivery delays
* More expired requests
* Greater variation between activations
* Higher automation error frequency
* Longer recovery periods

These changes can indicate that the workflow behaves differently under heavier conditions.

## Repeating the Test

One run provides limited evidence.

The same workload should be repeated when possible, using the same measurements and definitions.

If a particular pattern appears consistently, it becomes much more meaningful.

If it appears only once, it may simply be an isolated event.

## Final Report

An SMSHub Login load test should ultimately answer a practical question: how does the activation workflow change as the number of simultaneous requests grows?

The answer should come from request-level timing, concurrency measurements, delivery results, state monitoring, and failure data.

This approach produces a more useful performance report than simply recording the fastest activation or calculating one overall average.


# Concept: Probes

## Overview

The certification of a device is abstracted into a concept of probes. Each probe should check one feature against the device and generate an output.

Since the certification process usually involves checking of multiple features, a probe runner is used to select and execute the appropriate probes and return the results.

So the main two classes which implement this logic 

* ProbeRunner
* Probe

### ProbeRunner

* The `ProbeRunner` can execute one or more probes, and aggregates the probe results
* Probes can be dynamically selected via a predicate (i.e. used together with a feature specification etc.)
* Probes are automatically discovered by the `ProbeRunner`


### Probe

A probe has only one goal, and that is to check if a "feature" is implemented or not

A probe is a relative simple class, where all other probes should inherit from, and each subclassed probe only needs to implement the `check` method.

* Each probe SHOULD only check one "feature"
* Each probe MUST have a unique name/id (`.type_name`)
* Each probe returns a `ProbeResult`
* Each probe receives a `context` which the probe should be run against. Most likely this will be a managed object id (but each probe needs to check/validate the context itself)

#### Making assertions in a probe

* Probes should raise an exception when a criteria is not met
* Exceptions will be automatically captured by the probe runner and the exception details and overall probe result
* Probe duration (how long did the probe take) is automatically tracked in the probe result (using python contexts: `__enter__/__exit__` methods)

#### Example Probe

The following probe checks if a managed object's owner still exists in Cumulocity.

```python
class DeviceUserProbe(CumulocityProbe):
    """Check if the device owner of an inventory managed object exists"""
    def  __init__(self, *args, **kwargs) -> None:
        super().__init__(InventoryProbeNames.DEVICE_OWNER, *args, **kwargs)

    def check(self, result: ProbeResult, context: any) -> ProbeResult:
        with result:
            managed_object = self._c8y_api.inventory.get(context)
            user = self._c8y_api.users.get(managed_object.owner)
            if not bool(user.username):
                raise ProbeAssertionError('<<non-empty-value>>', user.username, 'Missing owner')

        return result
```

**Note:**

The code in the `check` method is run under a `with` block. This is mandatory to enable clean recording of the result. This means you do not need any exception handling in the check itself (resulting in cleaner, more readable code)

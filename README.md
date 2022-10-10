# Rate limiting client (Redis)

A rate limiting client using Redis.

## Installation

Follow the [instructions](https://docs.halon.io/manual/comp_install.html#installation) in our manual to add our package repository and then run the below command.

### Ubuntu

```
apt-get install halon-extras-rate-redis
```

### RHEL

```
yum install halon-extras-rate-redis
```

## Prerequisites

This HSL module requires that the [hiredis-cluster](https://github.com/halon-extras/hiredis-cluster) plugin is installed.

## Exported functions

These functions needs to be [imported](https://docs.halon.io/hsl/structures.html#import) from the `extras://rate-redis` module path.

### rate(namespace, entry, count, interval)

Check or account for the rate of `entry` in `namespace` during the last `interval`. On error an exception is thrown.

**Params**

- namespace `string` - The namespace
- entry `string` - The entry
- count `number` - The count
- interval `number` - The interval in seconds

**Returns**

If `count` is greater than zero, it will increase the rate and return `true`, or return `false` if the limit is exceeded. If count is zero (`0`), it will return the number of items during the last `interval`.

**Example**

```
import { rate } from "extras://rate-redis";

if (rate("outbound", $connection["auth"]["username"], 3, 60) == false) {
      Reject("User is only allowed to send 3 messages per minute");
}
```

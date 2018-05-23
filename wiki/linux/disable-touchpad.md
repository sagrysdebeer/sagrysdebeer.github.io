---
layout: wiki
title: Disabling the touchpad via the terminal
---
Disabling the goddamned over-sensitive touchpad on my laptop via the terminal.

Firstly execute the following command in bash.

```
xinput list
```

Find the touchpad device in the output, lets say it has the id 14, like mine.

```
ETPS/2 Elantech Touchpad                	id=14	[slave  pointer  (2)]
```

Then disable with

```
xinput set-prop 14 "Device Enabled" 0
```

Re-enable by setting to 1.

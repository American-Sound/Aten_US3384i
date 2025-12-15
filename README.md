Dealer Name: ASEI

System Name: Aten US3384i

Programmer: Pat Santucci

Aten US3384i USB 3.2 Switcher

Full control with feedback via `RS-232` or `RS-485`

Tested against firmware `v1.0.062`

Inputs:

|Input | Description |
-------|-------------|
poll_connected | query each host port for USB connection
poll_status | catch-all query. Updates current selected port and its connection status, auto-switching (Power On Detect) state, and priority fallback port for auto-switching.
priority_none | works with analog input "priority". When auto-switching is active, a fallback port can be set to always take when the active port's host is disconnected. Pulse priority_none to revert to the default behavior and take the next higher number connected port. Priority has no effect when auto-switching is disabled.
auto_switch_enable | Pulse to enable automatic switch to a newly detected USB connection. Called "power on detect" in the ATEN manual, but also works for physical connection of a host. Disconnect behavior is controlled by priority settings.
auto_switch_disable | Pulse to disable automatic switching
host_take[x] | Pulse to switch to host port[x]
RX$ | Connect to rx$ of a COM serial driver. RS-232 settings are fixed in firmware. See below for configuration details. Refer to the device user manual for RS-485 or custom firmware for different serial settings.
host | on change to a value between 1-8 inclusive, switches to that host port like the digital host_take[x] prompts. Included as a convenience for programs that drive switchers with analog vaules.
priority | works with digtial input "priority_none". See that entry for a description of priority port behavior. Setting a value 1-8 inclusive makes that port the priorty and unsets priority_none.

RS-232 Configuration:
| Field | Value |
|-------|-------|
| Baud Rate | 115200 |
Data Bit | 8 bit
Parity | None
Stop Bit | 1 bit
Flow Control | none


Outputs:

Output | Description
-------|------------
priority_none_fb | high when priority is none, low if priority is set to a value 1-8.
auto_switch_enable_fb | high when auto-switching (power on detect) is enabled.
auto_switch_disable_fb | high when auto-switching (power on detect) is disabled.
host_taken_fb[x] | signal [x] is high to reflect the currenly active host port (1-8). Others are low.
host_connected_fb[x] | signal [x] is high for every host port with an connected and powered on host.
TX$ | Connect to tx$ of a COM serial driver. See RX$ for settings.
host_fb | value 1-8 to reflect the currenly active host port. Included as a convenience for programs that drive switchers with analog vaules.
priority_fb | value 1-8 to reflect the current priority port, value 0 if the priority port is set to none. See digital input "priority_none" for a description of priority port behavior.


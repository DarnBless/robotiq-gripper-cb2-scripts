# Robotiq Gripper I/O Coupling URScript
Defines functions for controlling the Robotiq Gripper through a CB-series I/O coupling. Assumes the presets programmed on the I/O coupling follow the pattern of the default settings.

## Summary of usage
| `gripper_activate()` | Must be run before the grippers are used, and any time they have been powered down. Activation will cause the fingers to move. |
| `gripper_open()` | Open the grippers. |
| `gripper_close()` | Close the grippers. |
| `gripper_set_high_force()` | Set the grippers to move with high speed and force. This is the default. |
| `gripper_set_low_force()` | Set the grippers to move with low speed and force. |
| `gripper_object_detected()` | Returns true if the grippers are encountering an obstacle while trying to close, which usually means they're gripping something. |
| `gripper_is_waiting()` | Returns true if the grippers are activated and have completed their last command. False if not activated, not connected, or in the process of opening or closing. Note that grippers do not have to be waiting to receive new commands. Note that it can take a moment for this to change to false after a new command is issued. |
| `gripper_power_on()` | Switches on the power to the grippers. (`gripper_activate()` calls this as part of its startup process, but you may wish to use it separately.) |
| `gripper_power_off()` | Cuts power to the grippers. |


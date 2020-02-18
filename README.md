# Robotiq Gripper I/O Coupling URScript
This repository defines a set of URScript functions for controlling a Robotiq Gripper from a CB2 Universal Robot.

It is intended for use with the [Wrist Connect Kit I/O coupling](https://dof.robotiq.com/discussion/1704/new-wrist-connect-kits-for-ur-cb-series) (part ID IO-CPL-UR-CB-KIT), which has a URCap provided for CB3 robots, but no equivalent for CB2. The implementation follows [information provided on the Robotiq forum](https://dof.robotiq.com/discussion/1704/new-wrist-connect-kits-for-ur-cb-series#Comment_5785), plus a little experimentation.

To use the functions, include `gripper_io_interface.script` in the _BeforeStart_ section of a Universal Robot program.

## Presets
The I/O coupling does not allow a full range of control over the grippers, instead only choosing between one of four preset states. These states can be reprogrammed by connecting the coupling to a PC.

For ease of use, these scripts assume that the presets in the coupling follow [the pattern of the default presets](https://dof.robotiq.com/discussion/1704/new-wrist-connect-kits-for-ur-cb-series#Comment_5175), and define functions like `gripper_open()` rather than `gripper_preset_1()`. Generic preset commands could quickly be added in future.

## List of functions
| Function | Explanation |
| -- | -- |
| `gripper_activate()` | Must be run before the grippers are used, and any time they have been powered down. Activation will cause the fingers to move. NB the current implementation simply hangs if the grippers are absent or do not activate successfully. |
| `gripper_open()` | Open the grippers. |
| `gripper_close()` | Close the grippers. |
| `gripper_set_high_force()` | Set the grippers to move with high speed and force. This is the default. |
| `gripper_set_low_force()` | Set the grippers to move with low speed and force. |
| `gripper_object_detected()` | Returns true if the grippers are encountering an obstacle while trying to close, which usually means they're gripping something. |
| `gripper_is_waiting()` | Returns true if the grippers are activated and have completed their last command. False if not activated, not connected, or in the process of opening or closing. Note that grippers can still receive new commands before they have entered this 'waiting' state. Note that it can take a moment for this to change to false after a new command is issued. |
| `gripper_power_on()` | Switches on the power to the grippers. (`gripper_activate()` calls this as part of its startup process, but you may wish to use it separately.) |
| `gripper_power_off()` | Cuts power to the grippers. |


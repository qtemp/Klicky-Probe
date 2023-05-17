# qtemp's Klicky-Probe-Macros
This is a fork of jlas1's [Klicky-Probe](https://github.com/jlas1/Klicky-Probe) macros to expand the possible movements and actions needed to attach and detach a probe (I'm using a kevinakasams' [KlackEnder](https://github.com/kevinakasam/KlackEnder-Probe) probe on my CR-10S). We do this by establishing an array of commands that you specify for each action.  This gets us past the fixed number of moves that the original macros provide.

It also allows you to specify your desired homing order to be used in the homing_override macro as well as adds variables for attaching or detaching the probe when you aren't using it as a virtual endstop.

variable_safe_z is still utilized to make sure that we are in a safe location before and after doing any move.

# New variables (All are REQUIRED):

## homing_override variabes:
- variable_homing_order: ['X', 'Y', 'Z']
  - This is to allow you to control your axis homing order exactly.  If you specify G28 with only one axis then only that axis will be homed.  If you specify two axis, such as G28 X Y, then those will be both homed in the order established by the variable_homing_order.

- variable_attach_probe_before_z_home: True
  - This has been added if you don't use your probe as a virtual endstop for z (If you use calibrate_z).
  - Possible Values: True / False

- variable_detach_probe_after_z_home: True
  - This has been added if you don't use your probe as a virtual endstop for z (If you use calibrate_z).
  - Possible Values: True / False

## Attach_Probe variables:
- variable_attach_commands: [ *array of commands* ]
  - An array of commands to send to attach your probe and move to a safe place.  Within the brackets each command should be surrounded by double quotes and each command should be separated by a comma.
  - Examples
    - KlackEnder on Ender3: \[ "_Safe_Z", "G0 X245 F3000", "G0 X220 F3000" ]
    - KlackEnder on CR-10S: \[ "_Safe_Z", "G0 X316 F3000", "G0 X258 F3000" ]
  - _**Warning: Before you do this the first time, you may want to do them all manually to make sure that everything is going to work as expected.**_
  - **Note on Servos**: This does away with settings around servo movements, because we make no assumptions about what moves or actions you need to make to attach your probe.  However, the deploy and retract macros still exist and can be utilized in the above array by simply adding a command for "_DeployKlickyDock" or "_RetractKlickyDock".

## Detach_Probe variables:
- variable_detach_commands: [ *array of commands* ]
  - An array of commands to send to attach your probe and move to a safe place. Within the brackets each command should be surrounded by double quotes and each command should be separated by a comma.
  - Examples
    - KlackEnder on Ender3: \[ "_Safe_Z", "G0 X245 F3000", "G0 Z5 F1200", "G0 X220 F3000" ]
    - KlackEnder on CR-10S: \[ "_Safe_Z", "G0 X316 F3000", "G0 Z5 F1200", "G0 X258 F3000" ]
  - _**Warning: Before you do this the first time, you may want to do them all manually to make sure that everything is going to work as expected.**_
  - **Note on Servos**: This does away with settings around servo movements, because we make no assumptions about what moves or actions you need to make to detach your probe.  However, the deploy and retract macros still exist and can be utilized in the above array by simply adding a command for "_DeployKlickyDock" or "_RetractKlickyDock".

## Version Update:
- variable_version: 2

## Deprecated variables from jlas1 Klicky-Probe macro:
- variable_docklocation_x
- variable_docklocation_y
- variable_docklocation_z
- Variable_dockmove_x
- Variable_dockmove_y
- Variable_dockmove_z
- Variable_attachmove2_x
- Variable_attachmove2_y
- Variable_attachmove2_z
- variable_override_homing

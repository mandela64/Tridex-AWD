FOR REFERENCE ONLY

bigtreetech_ebb42_cpap.cfg

[mcu CPAP]
serial: /dev/serial/by-id/usb-Klipper_
#canbus_uuid: 

[manual_stepper flap_stepper]
step_pin: CPAP: PD0
dir_pin: !CPAP: PD1
enable_pin: !CPAP: PD2
microsteps: 16
rotation_distance: 1150
velocity: 4000
accel: 85000
endstop_pin: CPAP: PB8

[tmc2209 manual_stepper flap_stepper]
uart_pin: CPAP: PA15
interpolate: false
run_current: 0.8
stealthchop_threshold: 999999

[fan_generic cpap_fan]
pin: CPAP: PA0

[controller_fan cpap_power]
pin: CPAP: PB13
max_power: 1.0
stepper: manual_stepper flap_stepper

[temperature_sensor BTT_CPAP]
sensor_type: temperature_mcu
sensor_mcu: CPAP
min_temp: 0
max_temp: 100

[gcode_macro _SET_FLAP_ENABLED]
variable_enabled: 0
gcode:
    {% set enabled=params.ENABLED|int %}
	{% set flap_enabled=printer["gcode_macro _SET_FLAP_ENABLED"].enabled|int %}
	{% if enabled!=flap_enabled %}
		SET_GCODE_VARIABLE MACRO=_SET_FLAP_ENABLED VARIABLE=enabled VALUE={enabled}
		{% if enabled==1 %}
			MANUAL_STEPPER STEPPER=flap_stepper ENABLE=1
			MANUAL_STEPPER STEPPER=flap_stepper MOVE=-260 STOP_ON_ENDSTOP=1 SPEED=30
			MANUAL_STEPPER STEPPER=flap_stepper SET_POSITION=0
            MANUAL_STEPPER STEPPER=flap_stepper MOVE=127.5
        {% else %}
			MANUAL_STEPPER STEPPER=flap_stepper MOVE=127.5
			MANUAL_STEPPER STEPPER=flap_stepper ENABLE=0
		{% endif %}
	{% endif %}

[gcode_macro _START_CPAP_FAN]
gcode:
    SET_FAN_SPEED FAN=cpap_fan SPEED=0.06

[gcode_macro _STOP_CPAP_FAN]
gcode:
    SET_FAN_SPEED FAN=cpap_fan SPEED=0

[gcode_macro cpap_enable]
gcode:
    _SET_FLAP_ENABLED ENABLED=1
    
[gcode_macro cpap_disable]
gcode:
    _SET_FLAP_ENABLED ENABLED=0

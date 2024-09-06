# klipper_zoned_hotbed_macros
Klipper macros to support 3D Printers with Zoned Hotbeds

# How to Install
1. Configure each heater used in your hotbed as a `[generic_heater zone<id>]`. Each zone's name should be the same except for a number at the end (`zone0, zone1, zone2...`). Start with 0. Default is `zone` but you can change this with `variable_base_zone_name`.  
2. Copy this macro to your config directory and include it and `exclude_object` in your `printer.cfg` file:
```cfg
# printer.cfg
[include zoned_hotbed.cfg]
[exclude_object]
...
```

3. Then configure the internal variables by changing the variables in the `HEAT_BED_ZONE` macro inside `zoned_hotbed.cfg`:

```
[gcode_macro HEAT_BED_ZONE]
variable_base_zone_name: zone
variable_num_zones_x: 3
variable_num_zones_y: 4
variable_zone_width: 100
variable_zone_height: 100
variable_x_start_pos: 0
variable_y_start_pos: 0
variable_min_set_temp: 40
...
```
This will be moved to a separate config section that will reside inside `printer.cfg` in the future, but testing is needed first. 
# How to Use
Use it like normal (`M140`, `M190`) to heat the entire bed like normal, or specify X_MAX, Y_MAX, X_MIN, and/or Y_MIN to heat only the specified area. Any zone that touches that area will fully heat. Setting `OBJECT_ONLY` to 1 will heat the area around min and max of the current print (which is why we include `exclude_object`). 

The `M140` and `M190` gcodes are overridden in this macro so they support all parameters. You can also directly use the `HEAT_BED_ZONE` macro. 

# How to contribute
You can contribute by building a zoned bed and trying this macro out, or by helping clean up the code. Post any issues, questions, or ideas under [Issues](https://github.com/aamott/klipper_zoned_hotbed_macros/issues) on GitHub.

Also, sharing zoned hotbed designs and PCBs is hugely helpful. Not many people have attempted this and everyone can use a good example.
# Upcoming
- [ ] Ring zones 
- [ ] Custom grids (ex. a large build plate and smaller zones to extend the work area.)
- [ ] 3D Model of my zoned hotbed design
- [ ] 100x100 PCB design for manufacturing (Help?)

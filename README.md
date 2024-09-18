# klipper_zoned_hotbed_macros
Klipper macros to support 3D Printers with Zoned Hotbeds

# How to Install
1. Configure each heater used in your hotbed as a `[generic_heater zone<id>]`. Each zone's name should be the same except for a number at the end (`zone0, zone1, zone2...`). Start with 0. Default is `zone` but you can change this with `variable_base_zone_name`.  
    - To make the first heater `heater_bed`, set `variable_zone_0_is_heater_bed` to `True`. 
2. Copy this macro to your config directory and include it and `exclude_object` in your `printer.cfg` file:
```cfg
# printer.cfg
[include zoned_hotbed.cfg]
[exclude_object]
...
```

3. Then configure the internal variables by changing the variables in the `HEAT_BED_ZONE` macro inside `zoned_hotbed.cfg`. There are comments there to guide you. *For now, you'll have to duplicate all these variables into `_HEAT_BED_ZONE_WAIT` as well. I promise that won't last.*


All configurations will be moved to a separate config section inside `printer.cfg` in the future, but 


# How to Use
Use it like normal (`M140`, `M190`) to heat the entire bed like normal, or specify `X_MAX`, `Y_MAX`, `X_MIN`, and/or `Y_MIN` to heat only the specified area. Any zone that touches that area will fully heat. Setting `OBJECT_ONLY` to 1 will heat the area around min and max of the current print (which is why we include `exclude_object`). 

The `M140` and `M190` gcodes are overridden in this macro so they support all parameters. You can also directly use the `HEAT_BED_ZONE` macro. 

# How to contribute
You can contribute by building a zoned bed and trying this macro out, or by helping clean up the code, or by hopping into any of the [TODO's](#upcoming--todo) down below! Post any issues, questions, or ideas under [Issues](https://github.com/aamott/klipper_zoned_hotbed_macros/issues) on GitHub.

Also, sharing zoned hotbed designs and PCBs is hugely helpful. Not many people have attempted this and everyone can use a good example.

# Upcoming / TODO
- [ ] ❗Change to a klippy extra. Jinja makes the code to start heating all zones then wait for them all *super* inefficient. 
- [ ] Ring zones 
- [ ] Custom grids (ex. a large build plate and smaller zones to extend the work area.)
- [ ] Warm surrounding zones to minimize warping
- [ ] 3D Model of my zoned hotbed design
- [ ] 100x100 PCB design for manufacturing (Help?)
- [ ] When we've heated one zone and want to heat another: Prioritize new full-temp zones, take the greatest temperature of warm zones/already heated zones. 

# Q&A
Q: What if I try to heat a zone partially outside the bed? 
A: It will heat the zone that is inside. This way, if you have a model that hangs over the side of the bed (like a statue) it won't fail to heat. 
Q: What if I try to heat a zone *entirely* outside the bed?
A: It will give an error letting you know nothing is being heated.
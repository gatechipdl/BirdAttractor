RevA - first version
RevB - with correct parts, and partial design for in house milling; through hole parts flipped to bottom
RevC - layout with parts on top for fab house milling
 - problems
 -- smd button melts with 800 degree heat
 -- through-hole 6mm button legs don't fit well into holes
 -- missing a few 1206 sized resistors
 -- battery backwards due to kicad default battery pinout
 -- battery rotated backwards too on board; curved portion is where button slides in
 -- some LEDs on by default; check that is correct; should be able to disable
 -- relays are only monostable, not latching; only has one input; ok bc can be compensated for in code
 -- relays are throughole; should design for smd and tht too
 
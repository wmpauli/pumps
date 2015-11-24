pumps
=====

Tool for controlling syringe pumps with RS-232 connectivity.

See below and inline documentation for usage.

Example
=====

import pumps

def configure_pumps(volume=.75, diameter=26.77, rate=60, direction='INF', address=0):
    ''' configure pumps for the experiment '''
    p = pumps.scan()
    if len(p):
        if len(p) > 1:
            print "Found more than one pump, that's weird!"
        dev_address = p[0][1]
        p = pumps.Pump('/dev/ttyUSB0')

        for address in xrange(3):
            s = p.volume(volume, address=address)  # how much to dispense
            s = p.diameter(diameter, address=address) # diameter of syringe
            s = p.rate(rate, address=address) # how fast
            s = p.direction(direction, address=address) # pump (not suck) liquid
    return p 
	    
p = configure_pumps()
address = 0 # use first pump
p.run(address) 

Note: This may not work on anything but Ubuntu 14.04. 
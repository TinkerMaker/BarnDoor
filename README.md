# Arduino Barn Door Star Tracker 

This is a very basic barn door tracker which is a design I've adopted from many projects on the web to suit materials available to my location and simplicity in construction/coding.
This is not a design to be 100% acccurate and there are many other projects that will take you through the triganometry/mathermatical equations to increase accuracy.  
I used trial and error to calculate RPM values and will require some trial and error to calibrate to the materials you use.

I have successfully taken images up to 3 minutes long with no visible star trails and timelapes over the course of 2 hours without subjects moving in the field of view on the camera so it's accurate for my needs.

To test it's best to take several long exposures eg 2min + and a time lapse.  If you see star trails or the subject slightly moves through the field of view then you need to slightly alter the speed of the motor.


Materials:
Arduino Uno
BYJ-48 5v stepper motor
door hinge
3/16 UNC threaded rod with 24 TPI(threads per inch)
3/16 washers x4 , 2x nuts and 1x wing nuts
3/16 bolt + nut long enough to go through the wood and attach to the tripod
Gear set. I used these https://www.jaycar.com.au/spur-gear-set/p/YG2632
3/8 nut and bolt to attach the upper tripod ball head to.(large gold one in image)

The number of teeth in the gears isn't too important.  I used trial and error to get 1.2 revolutions per minute on the larger gear though there are mathematical equations on other projects to get better accuracy on the web.

Simply super glue a nut to the larger gear and attach the smaller gear to the stepper motor.

For 3/16 UNC rod with 24TPI and a radius of 29cm from the hinge to the rod hole, a RPM of 1.2 is required.
If you use a different size threaded rod use this website to calculate the RPM required to turn the nut https://blarg.co.uk/astronomy/barn-door-tracker-calculator

To bend the rod draw an arc on a piece of paper with a radius of 29cm and bend the rod to match the arc.

Drill a hole 29cm from the hinge using a 3-4mm drill bit, this is where the rod will fit.  you will need to enlarge the hole to allow the bent rod to go through smoothly without rubbing too much once attached.  Sopme friction is ok
and will stop the rod moving around in the hole too much when in use.

A wing nut and another washer/nut secure the rod to the upper piece of wood.

Put 2 washers under the gear with the nut attached to the bent rod before

The location of the bolt for the camera mount doesn't matter and is positioned to help balance the rig once you have the camera/lens attached.  Drill and attach 3/8 bolt to upper piece of wood.

The lower 3/16 nut and bolt attach to the base tripod head, 1 nut is used to join the tripod to the bolt secured to the wood.  It is counter sunk on the bottom to allow the tripod mount to sit flush.  See image.

For the code I used 400 steps per revolution as it smoothed out the action and reduced vibration.  Simply change the line myStepper.setSpeed(12.75); to alter the speed for the gears you use to acheive the desired RPM.

I used digital pins D2,D3,D4 & D5.  Pins 3,4 were reversed due to a known fault with the manufacturing of the stepper motor.  Please try the default setup and use the stepper example 1 rotation to check the motor works forward and reverse.
For some reason during manufacturing these 2 pins are incorrectly made and the motor will only go clockwise.

Code:
#include <Stepper.h>

const int stepsPerRevolution = 400;  // change this to fit the number of steps per revolution
// for your motor

// initialize the stepper library on pins 8 through 11:
Stepper myStepper(stepsPerRevolution, 2, 4, 3, 5);

void setup() {
  // set the speed at 1.2 rpm:
  myStepper.setSpeed(12.75);
}

void loop() {


  myStepper.step(-stepsPerRevolution);

}

Now the rig is complete you need to align to the celestial North/South pole.  If in the northern hemisphere you will need to set the speed to a negative number for it to run anticlockwise and the rig opens counter clockwise.
Southern hemisphere the rig opens clockwise.

First you need to find out what aaltitute angle the celestial pole is in the sky for your specific location.  Using an app like stellarium you enable SCP and like at the alt/AZ.  See attached image.
For my location Brisbane it shows an altitude of approx 28 degrees.  Again using an angle app set the tripod and rig to an angle of 28 degrees.  At time of writing it was 28.9 degrees.

Out in the field I use another app called SkyMap on android to hold the phone perpendicular to the hinge and align to the south pole to check.  Technically you can point the hinge to true south/north not magnetic and you will be aligned to the celestial pole.

Once this is done you are all set to start taking images.

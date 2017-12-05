## Term 2 - Project 2 : Unscented Kalman Filter  
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

In this project, my goal was to use the techniques and code examples presented in the Udacity course to control a car through a circuit using a PID controller.

The goals / steps of this project are the following:
- Complete the PID Controller
- Tuning the PID Gains
- Control the speed of the car (optional)

[//]: # (Image References)

[image1]: ./Output/CTEvsTraj.png.jpg "Better Trajectory for the cures"

## Reflection

### PID Control Dynamics
The Propotional gain (Kp)* error is the main driving force of the control which "propotionally" changes the control signal to minimize the error. For the Self driving car, the control gain changes the steering angle to minimize the erorr, measured as deviation from the center lane. If the car veers left, the steering angle changes  to the right to compensate. Depending on the sytem dynamics, a P controller could be all that is required, however, for the self driving car, the transient response showed a variety of behavior for a P controller. From Unstable osclliations to "laggy" control that could not keep the car on the lane during turns.

The Derative gain (kd) * error rate is the control signal that is propotional to the trasient behavior of the error. If the error increases rapidly, so does the the deravitive control signal. If tuned correctly the Derative gain can work to minimize the oscilations in the system, "a damped response". It should be noted that in pratice PD controllers are highly susceptible to noisy measurements, and should only be used on filtered or non-noisy measurement. For our application, the D gain damped the oscliations of the car's driving.

The Integral gain (Ki) * accumulated error is the control signal that is built up over time which corrects the bias error of the system. Essentially, the system's "inherent" dynamics or minor system biases can plateau the response on a traditional P controller. For the Self driving car, this could be wheel allingment for steer control (as mentioned in the lecture) or it could be the non-linear behavior of the drag on a car that requires a stronger throttle controller signal as the car's speed increases, which a P controller does not provide. For our application, It helps the car steer harder around bends. However,I believe a better way to address the control around the bends, is if the error was based on the trajectory curve on the inside of the bends and not the center lane. In the figure below, the better lane center is highligted in green versus the current one in red. 

![alt text][image1]

### Tuning

I tooked the manual approach with twiddle in mind. Essentially, I tuned the K gain until the response did not improove. On the first trial I tuned the Integral gain second before moving onto the Derative gain. I believe for our application the better route is to tune the Derative gain 2nd and if needed tune the I gain (otherwise leave it zero). During the first tuning cycle, threshold was manually controlled from 0.2 to a maximum of 0.7 (for stable driving) 

For the PD Controller, the final gains selected were.
* Kp: -0.12
* Kd: -3.0

For the PD Controller, the final gains selected were.
* Kp: -0.12
* Ki: -0.001
* Kd: -3.0

### Speed Controller

After trials with P and PI controllers, the final one selected was a PI controller that maintained a resinable speed of 50 mph. It would be noted the fastest successive trial was with a set speed of 70 mph.

For the PI controller the, the final gains selelected were:
* Kp: 1.0 
* Ki: 0.008

## Final Results
### PD Controller
###

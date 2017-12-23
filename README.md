## Term 2 - Project 4 : PID Self Driving Car Controler  
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

In this project, my goal was to use the techniques and code examples presented in the Udacity course to control a car through a circuit using a PID controller.

The goals / steps of this project are the following:
- Complete the PID Controller
- Tune the PID Gains
- Control the speed of the car (optional)

[//]: # (Image References)

[image1]: ./Output/CTEvsTraj.jpg "Better Trajectory for the cures"

## Reflection

### PID Control Dynamics
The Proportional gain (Kp)* error is the main driving force of the controller which "propotionally" changes the control signal to minimize the error, i.e. the distance to the center of the lane. For the Self driving car, the control gain changes the steering angle to minimize CTE. If the car veers left, the steering angle changes  to the right to compensate. Depending on the system dynamics, a P controller could be all that is required, however, for the self driving car, the transient response showed a variety of behavior for a P controller. From Unstable oscillations to "laggy" control that could not keep the car on the lane during turns.

The Derivative gain (kd) * error rate is the control signal that is proportional to the transient behavior of the error. If the error increases rapidly, so does the derivative control signal, if the error decreases rapidly, the derivative control increases ( but negatively). This behavior (in conjunction with a P controller) helps create a damped response.  If tuned correctly the Derivative gain can work to minimize the oscillations in the system, "a damped response". It should be noted that in practice, PD controllers are highly susceptible to noisy measurements, and should only be used on filtered or non-noisy measurements. For our application, the D gain damped the oscillations of the car's driving around the center lane.

The Integral gain (Ki) * accumulated error is the control signal that is built up over time which corrects the bias error of the system. Essentially, the system's "inherent" dynamics or minor system biases can plateau the response on a traditional P controller. For the Self Driving car, this could be wheel alignment for steer control (as mentioned in the lecture) or it could be the non-linear behavior of the drag on a car that requires a stronger throttle controller signal as the car's speed increases, which a P controller does not provide. For our application, it helps the car steer harder around bends. However, I believe a better way to address the control around the bends, is if the error was based on the trajectory curve on the inside of the bends and not the center lane. In the figure below, the trajectory to follow is highlighted in green versus the current one in red. 

![alt text][image1]

### Tuning

When tuning the gains for the controller, I took the manual approach with twiddle in mind. Essentially, I tuned the K gain until the response did not improve. On the first trial I tuned the Integral gain second before moving onto the Derivative gain. I believe for our application the better route is to tune the Derivative gain 2nd and if needed tune the Integral gain (otherwise leave it zero). During the first tuning cycle, throttle was manually controlled from 0.2 to a maximum of 0.7 (for stable driving) 
For the PD Controller, the final gains selected were.
* Kp: -0.1
* Kd: -3.0

For the PID Controller, the final gains selected were.
* Kp: -0.11
* Ki: -0.001
* Kd: -3.0

### Speed Controller

After trials with P and PI controllers, the final one selected was a PI controller that maintained a reasonable speed of 50 mph. It should be noted the fastest successive trial was with a set speed of 70 mph.

For the PI controller the, the final gains selected were:
* Kp: 0.25
* Ki: 0.008

## Final Results
### PD Controller

[![IMAGE ALT TEXT HERE](http://img.youtube.com/vi/rC_4XXDzsUY/0.jpg)](https://www.youtube.com/watch?v=rC_4XXDzsUY)

### PID Controller

[![IMAGE ALT TEXT HERE](http://img.youtube.com/vi/RIlDXTy-Ct0/0.jpg)](https://www.youtube.com/watch?v=RIlDXTy-Ct0)

### PD Controller - In reverse 
For fun I tried completing the course in reverse (same gains but negative).

[![IMAGE ALT TEXT HERE](http://img.youtube.com/vi/UhjPOicWxow/0.jpg)](https://www.youtube.com/watch?v=UhjPOicWxow)


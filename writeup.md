##Udacity MPC Project
This repository is the Udacity Model Prective Control project. 

##the Model
The kinematic model of the car includes:

1:x and y coordinates
2:orientation angle phi(angle between x-axis and heading direction)
3:velocity
4:cross-track error
5:psi error (epsi)

The outputs are acceleration and steering angle. The model calculate the state every timesteps by these equations:

    xt+1 = xt + vt * cos(phit) * dt;
    yt+1 = yt + vt * sin(phit) * dt;
    phit+1 = phit + vt / Lf * deltat * dt;
    vt+1 = vt + at * dt;
    ctet+1 = vt + sin(ephit) * dt;
    ephit+1 = ephit + vt / Lf * deltat * dt

##Timestep Length and Elapsed Duration


dt adjusts the time step of the prediction forecast. N sets the number of time steps the MPC forecasts. Without the latency the default value is OK(N=10, dt=0.1). But with the 100ms latency I have to increase the Value to 22 and 0.2. This is the best Value I chosen.With a high speed and latency the car needs a far forecast to react faster. And with a longer dt, the numbers of time steps need to be increased.


##Polynomial Fitting and MPC Preprocessing
On main.cpp lines 110-118. the cordinate is converted between car and map. this can make the polynomial fitting much easier.

##Model Predictive Control with Latency
A Latency about 100ms happens because of the timestep interval. So I account for this in MPC.cpp lines 101-105. Also, an additional cost function mentioned in the class penalizing the combination of velocity and steering angle was included and make the car cornering better.

---
title: GROUP Assignment 12
subtitle: Motor Selection
class_name: EGR598
bibliography: ../bibliography.bib
csl: ../ieee.csl
figure_alignment: H
---

## Overview

The purpose of this exercise isto use a linear motor model to achieve an optimal motor & geartrain selection.  

## Background: Motor Model
![typical linear speed-torque curve](figures/motor_model.png){width=50%}

Typically, motors are tested at a specified voltage under various loads.  The resulting current, torque, and angular velocity are then experimentally found and recorded.  From these values, a wealth of information can be gleaned about the motor.  Typical permanent-magnet DC motors exhibit a torque-speed relationship that can be modeled as linear, as seen above.

### Motor Modeling Equations

The voltage constant for motors is often given by a KV rating, usually in units of RPM/V. find the SI version.

The torque constant relates the current to torque generated by the motor.  one way to determine this is to find the stall current and the free running current and to find the slope between them.

$$k_v = (KV)2\pi/60$$
This permits one to determine the motor's free-running speed at any voltage using the equation
$$\omega_{free\ running} = k_v V$$

We will use the following equations to compute $k_t$:
$$k_t = \frac{\tau_{stall}}{I_{stall} - I_{free\ running}}$$

With $k_t$ determined you can then calculate the torque at any current and constant voltage using the function
$$\tau(I) = k_t(I-I_{free\ running})$$

Using the assumption of a linear motor model(valid for fixed permanent magnet DC motors), we can find the torque at any speed from $0$ to $\omega_{free\ running}$ using the equation
$$\tau(\omega)=\tau_{stall}\frac{(\omega_{free\ running} - \omega)}{\omega_{free\ running}}$$

The following equations can be used to compute mechanical and electrical power:
$$P_{mechanical}=\tau*\omega$$
$$P_{electrical}=IV$$

The efficiency of your system can be calulated as a function of power out(mechanical) over power in(electrical).  
$$eff = \frac{P_{mechanical}}{P_{electrical}}$$


## Procedure: Find a motor & geartrain
Go online and find a motor, gearmotor, or servo with a full set of specifications.  

1. Find or compute torque and speed constants using the equations above.  Ensure SI units.
<!--1. Write the equation you need to compute mechanical power?
1. Write the equation you need to compute electrical power?-->
1. Using $k_v$ given for the motor and the nominal motor voltage $V$, plot the *linear* speed-torque curve as a function of $w_{motor}$ (put $w_{motor}$ along the x-axis).  This should reproduce figure 1, but with actual values in the axes.
1. Using the expression for $P_{mechanical}$ plot the mechanical power curve as a function of $w_{motor}$ (put $w_{motor}$ along the x-axis). Identify the motor operating point(speed) which produces the most power.
1. Using $\tau(I)$, solve for $I$ and use to compute the electrical power as a function of $w_{motor}$.
1. Using the expression for $eff$, plot the motor efficiency as a function of $w_{motor}$ (put $w_{motor}$ along the x-axis). Identify the motor operating point(speed) which is the most efficient.
1. Using the motor requirements derived from HW11, select an operating speed which balances power, efficiency, and specifications.  Discuss why other operating points do not balance those considerations as effectively.  Consider and discuss how a gear ratio permits an extra degree of freedom in your motor selection.  Also consider total power usage, current limitations, efficiency, size, weight, etc in your answer.
1. Discuss whether the motor selected in the previous group assignment(HW8) satisfied your requirements based on this motor model.  How has the motor requirement changed?  What is the impact on mass?

## Assumptions and Notes
* Try maxon, pololu, or faulhaber for well characterized motors.  For brushless DC motors, try hobbyking or tower hobbies.
* the x axis for your plots should go from 0 to $w_{max}$
* label  axes and title  figures.
* It is possible to plot multiple axes on the same plot with matplotlib.  See <https://matplotlib.org/examples/api/two_scales.html>
* Convert all units to SI before computing your answer.  Answers/expressions in non-SI units will not be considered.  Supply the conversion factor you used.

## Turning In
Submit the jupyter notebook you used to compute this assignment.  
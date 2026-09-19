## 9:1 Planetary Gearbox

The gearbox was constructed in Onshape. In this module (not gear module), each attribute of gearbox construction will be discussed, as well as considerations to design requirements, such as backdrivability.

<img src="https://github.com/user-attachments/assets/de389647-cb18-4862-9d56-fc4ffb5b0157" width="25%"> 

<img src="https://github.com/user-attachments/assets/78f2e698-6419-4be5-bf4b-153fd45b66b4" width="53%"> 

## Gear Teeth Relations

$S$ : Number of Sun Sear Teeth

$P$ : Number of Planet Gear Teeth

$R$ : Number of Ring Gear Teeth

$N$ : Number of Planet Gears

The number of teeth are related by any of the following equations:

$$
R = S + 2P
$$
$$
P = \frac{R-S}{2}
$$
$$
S = R - 2P
$$

The following assembly condition can be used to verify proper meshing of all gears

$$
\frac{R+S}{N} = Integer
$$

For the example provided, S = 12, P = 42, R = 96, and N = 3, the above relations can be verified.

## Gear Geometry
Beyond teeth count and module scaling, tooth geometry can be adjusted to tune mechanical performance, specifically gear contact area and bending characteristics of each tooth. Specifically, _pressure angle_ and _root fillet_ radius:

<img src="https://github.com/user-attachments/assets/e2e8a4a7-ccc4-4949-bd4c-bb188a5c1379" width="40%"> 

<img src="https://github.com/user-attachments/assets/de928047-d59a-4608-a4fe-0706d418c21f" width="42%"> 

### Pressure Angle

<img src="https://github.com/user-attachments/assets/bf2989de-bcab-4701-ad69-efb5f365b6c3" width="42%"> 

<img src="https://github.com/user-attachments/assets/ee59b777-2b2b-4814-97c8-912e4c163487" width="36%"> 

Increase in pressure angle generates a wider tooth base, allowing for a stronger tooth, but a smaller contact area and slightly worse NVH (Noise, Vibration, Harshness) attributes. There is also an increase in radial force transmitted to the shaft and bearings.

<img src="https://github.com/user-attachments/assets/a2748c91-bdab-4f68-acf3-a8a1eb2df213" width="36%"> 

In a 3D-printed drive, it's most likely that the HPSTC, particularly on the ring gear, leading to tooth root bending, is the limiting failure mode. 

### Root Fillet

Root fillet is a more direct fortifier of gear teeth against root bending; a comparison between a 1/3 root fillet vs. a full fillet is provided below:

<img src="https://github.com/user-attachments/assets/f691bc07-7907-4b59-8da4-6662f1e913c0" width="38%">

<img src="https://github.com/user-attachments/assets/99153acf-6953-46ca-9939-28b03c878ebb" width="45%">

The first prototype 9:1 actuator utilizes 1/3 root fillets and PETG print, although a full fillet may be constructed along with Nylon CF.



## 3. Backlash

<img src="https://github.com/user-attachments/assets/d09d7520-20b3-45b2-b4a4-a52b78e3d2b8" width="43%">

Backlash is the amount of play between the gears. One factor to justify its existence is thermal expansion of 3D printed gears if operating under heated conditions, so a required backlash would be higher than that of metal gears. Additionally, it allows for a lubrication spacing and tolerance against jamming if two gear teeth contact simultaneously.

Standard AGMA practice recommends backlash value _B_ as a function of the diametral pitch Pd (or the _module_ (metric) parameter _m_ in the Onshape constructor):

$$
B \approx \frac{0.05}{Pd}
$$

$$
Pd = \frac{25.4}{m}
$$

More simply, in metric units, minimum backlash in mm can be estimated at 0.05 * m:

For a module size of 0.8mm used, this gives a minimum tangential backlash @ pitch line: $B = 0.040mm$.

An initial generous backlash of 0.15mm is used for the FDM-printed ring gear, since this minimum calculation is used for metal gear cuts.

However, this introduces challenges when it comes time for control, as backlash effectively introduces a discontinuity in the transmission. Therefore, an intended position output from the BLDC driver can result in a small window of QDD actuator position. This is accentuated during direction-reversal events, as a gap can prompt the controller to overcompensate, possibly resulting in overshoot.

Additionally, due to the backlash gap, mechanical stiffness can experience large jumps from zero to a large stress over a short period of time, transmitting large forces into the weak links of the ring gear, as well as requiring motor control to account for nonlinearities in stiffness. 

### Backdrivability

One of the most important design goals of a quasi-direct drive actuator is backdrivability. For a backdrivable motor, a reasonably low gear ratio (6:1-10:1) is obvious, but also minimal stiction across the actuator components to overcome when initiating movement from the output end.

The driver board + software side accounts for backdrivability via torque estimation via _current sensing_:

$$
\tau_{motor} = Kt * Iq
$$

Where Kt is the torque constant of the motor, and Iq is the quadrature-axis current, which is utilized in the Field-Oriented Control (FOC) loop, specifically the Clarke/Park transforms. This is how torque is estimated without the need for a specialized torque sensor.

<img src="https://github.com/user-attachments/assets/7d7af51c-d8d8-43fd-b6b9-f5cf4617c46d" width="80%">

Within the FOC control scheme exists casdaced PI controllers. The inner control loop (current loop) regulates the values of Iq and Id to provide a consistent output torque estimate via $\tau_{QDD} = Kt * Iq * N * \eta$, where N is the gear ratio of the QDD, and $\eta$ is the gearbox efficiency.

The outer loop (speed loop), is responsible for "responding" to any backdriving forces back into the actuator. In a backdriving event (a hand pushes against motor movement in the opposite direction), the motor does not resist it rigidly, rather forms a spring-damper system around it to allow the motor to be compliant. 

This is done via impedance control, which models a spring-mass damper to correct the output torque via a PD loop: 

$$
\tau = \tau_{feedforward} + Kp*(\theta_{target} - \theta_{measured}) - Kd*\frac{d\theta}{dt}
$$

Further detail regarding backdrivability control will be described in a separate module.









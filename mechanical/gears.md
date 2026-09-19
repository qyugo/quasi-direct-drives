## 9:1 Planetary Gearbox

The gearbox was constructed in Onshape. In this module (not gear module), each attribute of gearbox construction will be discussed.

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

<img src="https://github.com/user-attachments/assets/f691bc07-7907-4b59-8da4-6662f1e913c0" width="45%">

<img src="https://github.com/user-attachments/assets/99153acf-6953-46ca-9939-28b03c878ebb" width="45%">

The first prototype 9:1 actuator utilizes 1/3 root fillets and PETG print, although a full fillet may be constructed along with Nylon CF.












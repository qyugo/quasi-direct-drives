# 3510 650 KV Motor (General)

Config: 12N14P, stator dim. 35mm x 10mm

<img width="840" height="579" alt="image" src="https://github.com/user-attachments/assets/f85a7e77-1b25-4790-9d75-9046fae04942" />


## 1. Tuning Notes

Tuning config (default: 0.16): Buzzed

Velocity Kp: 0.021 on ODrive S1 - adjustment from default (full tuning specs soon)

Max cont. current = 22A (listing)

## 2. Theoretical Torque Calculation

$ Kt \approx 8.27/KV $

$ Kt \approx 0.0127 Nm*A $ (Default Winding, per amp of peak q-axis current)

Rewinding a 12N14P can possibly give a higher torque capacity per amp, with a lower KV.

## 3. Continuous Torque (with power dissipation factored in)

Even though the listing for the 650KV variant of the motor states 22A continuous current, a more conservative estimation will be made.

Copper loss in FOC is described as follows:

$$
P = 1.5 * I^2R
$$

$$
I_{cont} = \sqrt{ \frac{P_{th}}{1.5 * R_{phase}}}
$$

$$
\tau_{cont} = Kt*I_{cont}
$$

Assumptions:
Line-to-line phase resistance $ R_{phase} = 100 m\Omega $ (Listing stated $65m\Omega$
Non-heatsunk power dissipation: 10W

$$ 
I_{cont} = 11.5A 
$$

$$
\tau_{cont} = 0.15N*m
$$

At 40A peak, peak torque would be 0.5 N*m.







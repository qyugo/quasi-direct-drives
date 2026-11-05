---
title: 3510 Actuator
nav_order: 3
permalink: /
---

# 3510 Actuator V1

<img src = "https://github.com/user-attachments/assets/eb01b441-96db-42cf-a853-b2a51e8ca71e" width="60%" >

Actuator with YVGESC case V1 (looks like a camera...)

<img width="419" height="310" alt="Screenshot 2026-11-05 at 2 38 38 PM" src="https://github.com/user-attachments/assets/8a9377da-d31b-48dd-821c-c3ed703d9e04" />


Mechanical specs: 10:1 QDD, Ø70mm x 56.5mm.

## Theoretical Performance Specs

Using default winding (650KV, 11.5A cont. current):

Kt = 0.0127 Nm/A cont.
Cont. Torque = 0.15 Nm

Assumptions: 
1. L-L phase resistance of 100mOhm - R_phase = 50mOhm
2. 10W of heat dissipation @ 100C

Peak Torque @ 40A = 0.5 N*m

Theoretical Actuator Specs (using 90% gearbox efficiency, 30A cont., 50A peak driver, non-limiting gearbox materials)

$$
\tau_{cont} = 0.15 * 0.9 * 10 = 1.35 N*m
$$

$$
\tau_{peak} = 0.5 * 0.9 * 10 = 4.5 N*m
$$

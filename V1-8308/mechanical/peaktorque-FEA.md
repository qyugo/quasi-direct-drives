# Peak Torque Derivation + Finite Element Analysis on Ring Gear

*Note: Variable nomenclature may be inconsistent across modules. Each page should be self-contained.

In this section, peak worst-case scenario using HPSTC (highest point of single tooth contact) will be calculated as an equivalent static load, and processed in Simscale for FEA analysis.

The calculation flow will be as follows:

Motor KV -> Kt -> Peak Phase Current -> Motor Peak Torque -> Output Torque via Gearbox -> Resultant Load on Ring Gear

### 1. Motor Kt

Using known or tested KV characteristics of the motor (more detailed info, derivations, and examples can be found at https://github.com/qyugo/motormaxxing):

$$
K_t = \frac{9.549}{KV}
$$

Where KV is in units of RPM/V, and Kt is in N*m/A.

The motor used for this project is an LA8308 with a KV of 90, and the torque constant can be obtained:

$$
Kt = \frac{9.5493}{90} = 0.106 N*m/A
$$

### 2. Peak Torque from Motor

$$
T_{peak} = Kt * I_{peak}
$$

Where $I_{peak}$ is the peak motor phase current, in the case of the LA8308 it is 22A, which is a substantially high number that will be used nonetheless.

The peak current can also be limited by the current capabilities of the motor driver, if it is lower than that of the motor.

$$
T_{peak} = 0.106 N*m/A * 22A = 2.33 N * m.
$$

### 3. Resultant Torque Through Gearbox

The output torque can be calculated using the gear ratio Q and gearbox efficiency $\eta$, in which a stand-in efficiency of 0.85 will be used:

$$
T_{out} = T_{peak} * Q * \eta_{gearbox} = 2.33 * 9 * 0.85 = 17.8 N * m.
$$

### 4. Total Ring Reaction Torque

As three planet gears will drive a force into the outer ring gear at approximately one gear tooth contact area each (total of three), the reaction torque can be calculated as follows:
Zr and Zs refer to the number of teeth on the sun and ring gears.

$$
T_{ring} = T_{out} * \frac{Z_r}{Z_s + Z_r} = 17.8 * \frac{96}{108} = 15.82 N*m
$$

### 5. Ft Per Mesh

The force on each mesh is necessary to derive for finite element analysis. For three planets and a ring pitch radius $r_{rp}$.

Ring pitch diameter $d_{rp} = m * Z_r$, where m is the module size (mm). Thus $r_{rp} = d_{rp}/2$.

$$
F_t = \frac{T_ring}{3 * r_{rp}} = \frac{15.82}{3*0.0384} = 137.3 N
$$

This is the force on each of the three contact points between the planets and the ring gear.

### 6. Normal Force

In SimScale, the force Ft is converted to the normal force on the tooth contact area, which is adjusted based on the ring pitch angle $\theta_{pitch}$.

Using $\theta_{pitch} = 20 degrees,

$$
Fn = \frac{Ft}{cos(20)} = \frac{137.3}{0.9397} = 146.1N
$$

Applied normal to the surface.

## SimScale FEA

Anisotropic analysis using Nylon PACF-15 printed layer-by-layer in identical cross sections was used.

Materials: 91.9 MPA X-Y, 48.3 MPa Z, 5136 MPa Modulus







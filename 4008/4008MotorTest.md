Testing using my coupling to verify Kv for a 4008 motor.

# 4008 DUT

Listing: 750 KV
Config: 12N14P

<img src="https://github.com/user-attachments/assets/d563ffac-f21d-4eb6-817e-d432406f8f33" width="22%" />
<img src="https://github.com/user-attachments/assets/580c1f89-2811-43cc-8da9-212a4000c480" width="22%"/>
<img src="https://github.com/user-attachments/assets/3eab481e-66d0-4e30-afd0-3f7a7674d581" width="22%"/>
<img src="https://github.com/user-attachments/assets/3a9b9bee-4f6f-410e-a8e9-c84f77bef945" width="22%"/>

<img src="https://github.com/user-attachments/assets/dbcd1980-7df5-4fb7-a267-5c46ece1c070" width="90%"/>

# KV

Kv is valculated using peak-to-peak voltage/2.


$$KV = \frac{RPM}{Vpp/2}$$

| Speed (rev/s) | rpm | CH1 Vpp (V) | CH2 Vpp (V) | Avg Vpp (V) | CH1 Vavg (V) | CH2 Vavg (V) | CH1 f (Hz) | CH2 f (Hz) |
|---|---|---|---|---|---|---|---|---|
| 3 | 180 | 0.61 | 0.70 | 0.655 | -0.09 | -0.17 | 0.00 (retest) | 0.00 (retest) |
| 5 | 300 | 0.86 | 1.02 | 0.940 | -0.03 | -0.01 | 4.42 (retest) | 0.00 (retest) |
| 7 | 420 | 1.23 | 1.19 | 1.210 | -0.03 | -0.10 | 49.14 | 48.78 |
| 10 | 600 | 1.73 | 1.75 | 1.740 | -0.03 | -0.07 | 70.42 | 70.42 |

ODrive dyno current and speed:
| Command (rev/s) | Rows | Duration (s) | Mean speed (rev/s) | Speed std (rev/s) | Speed min (rev/s) | Speed max (rev/s) | Mean current (A) | Current std (A) |
|---|---|---|---|---|---|---|---|---|
| 3 | 1255 | 15.17 | 3.0017 | 0.0381 | 2.880 | 3.129 | -0.172 | 0.106 |
| 5 | 1327 | 15.99 | 5.0036 | 0.0431 | 4.850 | 5.154 | -0.157 | 0.106 |
| 7 | 1282 | 15.39 | 7.0012 | 0.0514 | 6.840 | 7.128 | -0.128 | 0.125 |
| 10 | 1472 | 17.56 | 10.0042 | 0.0757 | 9.745 | 10.185 | -0.104 | 0.179 |

Pole pairs of 7 is verified via electrical frequency.

KV Test Points

<img width="1690" height="650" alt="image" src="https://github.com/user-attachments/assets/5e86f347-c591-44e1-ae93-c0520c09fb3e" />

| Testpoints | KV (rpm/V) |
|---|---|
| 420 and 600 rpm only, through origin | 691 |
| All 4 points, through origin | 673 |
| All 4 points, straight line (intercept about 0.17 Vpp) | 778 |
| Slope between 300 and 600 rpm only | 750 |
| Slope between 420 and 600 rpm only | 680 |

Result: 673-778 KV.

KV obtains torque constant as well.

$ Kt = 8.27/KV $






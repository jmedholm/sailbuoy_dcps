# Sailbuoy DCPS - Edholm (2022)

Two notebooks to load and correct the Sailbuoy DCPS data. These notebooks are made for the Polar Gliders research group, and adapted for their specific sensor suite on the Sailbuoy.


### 1_correcting_mag_dec_and_gps_vel.ipynb

Firstly, the data is loaded from a datalogger output file, DCPS.txt. This contains data from the sensor itself, and pre-processed data from the Sailbuoy's own datalogger. This notebook uses the sensor's own data.

The data from the sensor is already pre-processed and corrected for tilt and roll, which is fine if it is stationary. The Sailbuoy does move through the water, and therefore we need to correct for that motion. If the Sailbuoy is travelling north over stationary water, i.e. no current, with a speed of 1 m/s, the sensor will read a southbound current of 1 m/s. The solution is therefore to compute the speed and direction of travel, and add that to the measurements. Another complicated feature is the magnetic declination, which is the deflection of in situ compasses relative to absolute north. The sensor does not use GPS to correct its heading, which is why we have to add this as well, prior to correcting for the Sailbuoy's movements.

The notebook runs as follows:
1. Load the data
2. Select the data with proper time and location stamps
3. Correct the current direction for magnetic declination
4. Correct the current direction and speed for the Sailbuoy's movements
5. Add variable names and descriptions to the dataset
6. Save the dataset as an .nc-file

### 2_quality_control.ipynb

The previously saved .nc-file is loaded, and some checks are made. For every time step, cells that have a strength limit lower than -40dB are discarded, this depth correlates well with a rise in the standard deviation for horizontal speed. Then a secondary check of the standard deviation for the sensor's recorded heading. If it is above ±20°, that whole measurement is discarded, and the same is if the maximum tilt is above 80° (90° is equal to the Sailbuoy being completely on its side for at least one of the 150 pings.

1. Load the data
2. Select data with strength > -40dB
3. Select data with standard deviation heading < 20°
4. Select data with maximum tilt < 80°
5. Save the dataset as an .nc-file

The data is now ready for further analysis.

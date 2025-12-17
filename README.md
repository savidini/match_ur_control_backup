# match_ur_control_backup

Backup of the .urcontrol folder for all match URs

## How to Restore Calibration to a New Polyscope Installation

To restore the calibration data from these backups to a new Polyscope installation on an SD card:

### Prerequisites
- A computer with an SD card reader
- The SD card from your UR robot controller
- Basic familiarity with command line or file management

### Step-by-Step Instructions

1. **Identify the correct backup**: Check the table below to find the backup that matches your robot's serial number or characteristics.

2. **Extract the backup**: 
   ```bash
   unzip backup_XXX.zip
   ```
   Replace `XXX` with the appropriate backup number (e.g., `backup_112.zip`).

3. **Prepare the SD card**:
   - Insert the SD card from your UR robot controller into your computer
   - The SD card should have a partition that contains the Polyscope installation

4. **Locate the .urcontrol directory**:
   - On the SD card, navigate to the root directory
   - You should see a directory named `.urcontrol` (it may be hidden)

5. **Backup your current calibration** (recommended):
   ```bash
   cp -r /path/to/sd_card/.urcontrol /path/to/sd_card/.urcontrol_backup_$(date +%Y%m%d)
   ```

6. **Copy the calibration files**:
   ```bash
   cp -r .urcontrol_XXX/* /path/to/sd_card/.urcontrol/
   ```
   Replace `XXX` with the appropriate backup number.

7. **Verify the files were copied correctly**:
   - Check that `calibration.conf` exists in the `.urcontrol` directory
   - Verify other calibration files are present (calibration_trajectory_*.ct files)

8. **Safely eject the SD card** and reinsert it into your UR robot controller.

9. **Power cycle the robot** for the changes to take effect.

### Important Notes
- **Always backup your current calibration** before overwriting it
- **Use the correct backup** for your specific robot - mixing calibrations between robots can cause issues
- **Power cycle required** - the robot needs a full restart to load the new calibration data
- **Test carefully** - after restoring, test the robot's movement in a safe area

## Calibration Data Comparison Table

Below is a comparison of the calibration parameters from each robot backup:

| Robot ID | Calibration Status | Joint Checksums | Key Delta Parameters |
|----------|-------------------|-----------------|---------------------|

### Robot 112
- **Status**: Linearised (2)
- **Joint Checksums**: `[0xb630883c, 0xb61f6e2e, 0xb5484b61, 0xb612c3a2, 0xb62bd7bc, 0xb61c0e94]`
- **Delta Theta**: `[5.64e-07, -1.217, 1.212, 0.00484, -2.81e-07, -8.62e-08]`
- **Delta A**: `[0.000127, 0.4006, 0.000150, 5.37e-05, -9.61e-05, 0]`
- **Delta D**: `[-6.88e-06, 1935.67, -1935.34, -0.3315, -0.000104, -0.000962]`

### Robot 117
- **Status**: Linearised (2)
- **Joint Checksums**: `[0xb459a61e, 0xb45528a6, 0xb53963ab, 0xb41a0255, 0xb417126d, 0xb40d200b]`
- **Delta Theta**: `[-4.30e-07, 0.1814, -0.2489, 0.06749, 9.59e-07, -8.13e-08]`
- **Delta A**: `[0.000111, 0.01038, 0.001519, 5.71e-06, -4.56e-05, 0]`
- **Delta D**: `[6.17e-05, 556.95, -562.19, 5.2409, -0.000201, -0.001058]`

### Robot 118
- **Status**: Linearised (2)
- **Joint Checksums**: `[0xb420f4ad, 0xb4409feb, 0xb553930a, 0xb411c00e, 0xb418cc4f, 0xb417175a]`
- **Delta Theta**: `[-2.12e-08, 0.08526, -0.1634, 0.07814, -5.51e-07, 1.35e-07]`
- **Delta A**: `[0.000119, 0.002574, 0.002024, -3.24e-05, 3.28e-05, 0]`
- **Delta D**: `[0.000286, 76.762, -83.383, 6.6206, -0.000122, -0.000937]`

### Robot 119
- **Status**: Linearised (2)
- **Joint Checksums**: `[0xb455f77a, 0xb437b9f9, 0xb531fd6e, 0xb4249736, 0xb412c748, 0xb4159beb]`
- **Delta Theta**: `[-2.02e-07, 1.1667, -0.8036, -0.3630, 6.26e-07, -6.46e-07]`
- **Delta A**: `[3.599e-05, 0.37187, 0.03761, 2.029e-05, 8.37e-06, 0]`
- **Delta D**: `[-3.65e-05, 435.77, -468.05, 32.2789, -9.01e-05, -0.000990]`

### Robot 124
- **Status**: Linearised (2)
- **Joint Checksums**: `[0xb422f034, 0xb426d1c5, 0xb51f078c, 0xb42cfe2c, 0xb4085ec0, 0xb60c5894]`
- **Delta Theta**: `[-1.08e-07, 1.1680, -1.2557, 0.08772, 5.66e-07, -7.58e-07]`
- **Delta A**: `[8.745e-05, 0.37264, 0.002494, -2.41e-05, 5.98e-05, 0]`
- **Delta D**: `[0.000127, 597.79, -604.85, 7.0589, -0.000134, -0.000920]`

### Robot 125
- **Status**: Linearised (2)
- **Joint Checksums**: `[0xb435bb63, 0xb441d7b1, 0xb5198b08, 0xb40d9f92, 0xb41b2338, 0xb42edc4e]`
- **Delta Theta**: `[-1.42e-07, 0.6731, -0.8223, 0.1492, 1.22e-06, 4.74e-09]`
- **Delta A**: `[0.000105, 0.13394, 0.006690, -1.038e-05, 1.028e-05, 0]`
- **Delta D**: `[0.000248, 681.73, -696.41, 14.6725, -0.000155, -0.000962]`

## Technical Details

### Calibration Status Codes
- `0` = notInitialized
- `1` = notLinearised  
- `2` = Linearised (fully calibrated)

### Parameter Explanations
- **delta_theta**: Joint angle offsets in radians
- **delta_a**: Link length offsets in meters
- **delta_d**: Link offset corrections in meters
- **delta_alpha**: Joint twist angle corrections in radians
- **joint_checksum**: Unique identifiers for each joint's calibration
- **joint_raw_offset**: Raw encoder offset values

### File Contents
Each backup contains:
- `calibration.conf` - Main calibration configuration
- `calibration_trajectory_*.ct` - Calibration trajectory files for different robot models
- `joint_motor_calibration_id*.txt` - Individual joint motor calibration data
- `robot_calibration_summary.txt` - Summary of calibration results
- `calibration.log` - Calibration process log

## Troubleshooting

If you encounter issues after restoring calibration:

1. **Double-check file locations**: Ensure files are in the correct `.urcontrol` directory
2. **Verify file permissions**: Files should be readable by the Polyscope system
3. **Check robot behavior**: Test in reduced speed mode first
4. **Restore from backup**: If issues persist, restore your original calibration

For critical production systems, consider contacting UR support before making calibration changes.
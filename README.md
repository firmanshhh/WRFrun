# Downscaling CMIP6 Data using WRF

This repository contains resources for downscaling CMIP6 data, specifically using the WRF (Weather Research and Forecasting) model. The provided `namelist.wps` and `namelist.input` files are default settings tailored for the MPI-ESM1-2-HR dataset.

## Table of Contents

- [Introduction](#introduction)
- [Requirements](#requirements)
- [Installation](#installation)
- [Data Access](#data-access)
- [Usage](#usage)
- [Configuration](#configuration)
  - [namelist.wps](#namelistwps)
  - [namelist.input](#namelistinput)
- [Contributing](#contributing)
- [License](#license)

## Introduction

This repository aims to provide a streamlined process for downscaling CMIP6 data using the WRF model. Downscaling is crucial for translating coarse global climate model data into high-resolution regional climate information, which is essential for localized climate impact assessments.

## Requirements

- WRF Model (version 4.2 or later recommended)
- WPS (WRF Preprocessing System)
- NetCDF Libraries
- MPI Libraries

## Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/firmanshhh/WRFrun.git
   cd your-repo
   ```

## Data Access

- Intermediate files for the MPI-ESM1-2-HR dataset can be accessed through the following link: [Download Intermediate Files](https://terabox.com/s/1u9iBMcHWD1uDFIm1USo5hg)
- Geog Data files can be accessed through the following link: [Download geog Files](https://terabox.com/s/1qEgdp-seflxi2fT_jo8Ksw)

## Usage

1. Prepare your WRF and WPS is installed.

2. Download the necessary input data from the provided link and place it in the appropriate directory.

3. Edit the `namelist.wps` and `namelist.input` files as needed to suit your specific requirements.

4. Run WPS to preprocess the data:

   ```bash
   export wrfdir=/home/wrf/WRF/WRF #change with the actual WPS directory
   export wpsdir=/home/wrf/WRF/WPS #change with the actual WRF directory

   rm wrfbdy* wrfinput* wrfout*
   ln -sf $wrfdir/run/*.TBL .
   ln -sf $wrfdir/run/ozone* .
   ln -sf $wrfdir/run/RRTMG* .
   ln -sf $wrfdir/run/CAM* .
   ln -sf $wrfdir/run/*.exe .
   ln -sf $wpsdir/*.exe .
   ln -sf $wpsdir/geogrid .
   ln -sf $wpsdir/gmetgrid .
   
   ./geogrid.exe
   ./metgrid.exe
   ```

5. Execute the WRF model:

   ```bash
   mpirun -np <number_of_processors> ./wrf.exe
   ```

## Configuration

### namelist.wps

The `namelist.wps` file contains settings for the WRF Preprocessing System. Key parameters include:

- `start_date` and `end_date`: Define the temporal range of your simulation.
- `max_dom`: Number of domains.
- `interval_seconds`: Time interval of your input data.
- `geog_data_path`: Path to your geographical data.

### namelist.input

The `namelist.input` file includes configurations for the WRF model run. Key sections include:

- `time_control`: Specifies the simulation start and end times, time step, and output frequency.
- `domains`: Contains domain-specific settings such as the number of vertical levels, grid spacing, and domain dimensions.
- `physics`: Specifies the physical parameterization schemes used in the model.

## Contributing

Contributions are welcome! Please fork the repository and create a pull request with your changes. Ensure your code adheres to the project's coding standards and include appropriate documentation.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

# Pangu Weather Project

## Description

The goal of this project is to play with Pangu Weather, infer it and compare the results with [Era 5 Dataset](https://cds.climate.copernicus.eu/cdsapp#!/dataset/reanalysis-era5-single-levels?tab=overview).

## Table of Contents

- [Installation](#installation)
- [Dataset](#dataset)
- [Inference](#inference)

## Installation

To run this project, you will need to run the following commands in your terminal:

```bash
pip install -r Pangu-Weather/requirements_cpu.txt
```

### Downloading trained models

Please download the four pre-trained models (~1.1GB each) from Google drive or Baidu netdisk:

The 1-hour model (pangu_weather_1.onnx): [Google drive](https://drive.google.com/file/d/1fg5jkiN_5dHzKb-5H9Aw4MOmfILmeY-S/view?usp=share_link)/[Baidu netdisk](https://pan.baidu.com/s/1M7SAigVsCSH8hpw6DE8TDQ?pwd=ie0h)

The 3-hour model (pangu_weather_3.onnx): [Google drive](https://drive.google.com/file/d/1EdoLlAXqE9iZLt9Ej9i-JW9LTJ9Jtewt/view?usp=share_link)/[Baidu netdisk](https://pan.baidu.com/s/197fZsoiCqZYzKwM7tyRrfg?pwd=gmcl)

The 6-hour model (pangu_weather_6.onnx): [Google drive](https://drive.google.com/file/d/1a4XTktkZa5GCtjQxDJb_fNaqTAUiEJu4/view?usp=share_link)/[Baidu netdisk](https://pan.baidu.com/s/1q7IB7tNjqIwoGC7KVMPn4w?pwd=vxq3)

The 24-hour model (pangu_weather_24.onnx): [Google drive](https://drive.google.com/file/d/1lweQlxcn9fG0zKNW8ne1Khr9ehRTI6HP/view?usp=share_link)/[Baidu netdisk](https://pan.baidu.com/s/179q2gkz2BrsOR6g3yfTVQg?pwd=eajy)

These models are stored using the ONNX format, and thus can be used via different languages such as Python, C++, C#, Java, etc.

## Dataset

### a - Inputs

Please download the following input files that corresponds to the ERA5 initial fields of at 12:00UTC, 2018/09/27.

`input_surface.npy`: [Google drive](https://drive.google.com/file/d/1pj8QEVNpC1FyJfUabDpV4oU3NpSe0BkD/view?usp=share_link)/[Baidu netdisk](https://pan.baidu.com/s/1i4o5i8guAqmOus6PWncAlA?pwd=4z9s)

`input_upper.npy`: [Google drive](https://drive.google.com/file/d/1--7xEBJt79E3oixizr8oFmK_haDE77SS/view?usp=share_link)/[Baidu netdisk](https://pan.baidu.com/s/1mS8X5MqEdbVfF2u2Us62FQ?pwd=sgx6)

- `input_surface.npy` stores the input surface variables. It is a numpy array shaped (4,721,1440) where the first dimension represents the 4 surface variables (MSLP, U10, V10, T2M in the exact order).

- `input_upper.npy`stores the upper-air variables. It is a numpy array shaped (5,13,721,1440) where the first dimension represents the 5 surface variables (Z, Q, T, U and V in the exact order), and the second dimension represents the 13 pressure levels (1000hPa, 925hPa, 850hPa, 700hPa, 600hPa, 500hPa, 400hPa, 300hPa, 250hPa, 200hPa, 150hPa, 100hPa and 50hPa in the exact order).

In both cases, the dimensions of 721 and 1440 represent the size along the latitude and longitude, where the numerical range is [90,-90] degree and [0,359.75] degree, respectively, and the spacing is 0.25 degrees. For each 721x1440 slice, the data format is exactly the same as the .nc file download from the ERA5 official website.

### b- Era 5 ground truth

Go on [Era 5 Dataset](https://cds.climate.copernicus.eu/cdsapp#!/dataset/reanalysis-era5-single-levels?tab=overview) website :

- from 2018/09/27 12:00UTC to 2018/09/29 12:00UTC
  Download the fields present in `input_surface.npy` and `input_upper.npy`:
- 4 surface variables MSLP, U10, V10, T2M
- 5 surface variables (Z, Q, T, U V) for the 13 pressure levels

## Inference

To infer pangu weather on our input data.

The file ` inference_iterative.py` is part of [Pangu Weather Repository](https://github.com/198808xc/Pangu-Weather/tree/main) that we modified so we can infer pangu weather at different lead times at the same time (1,3,6)

```bash
python Pangu-Weather/inference_iterative.py
```

## Notebook

` visualization_notebook.py` helps you to play with the results of pangu weather at different leadtimes, plot the map of weather fields and retrieve the MSE to asses the hiearchical aggregation model.

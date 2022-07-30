# RIPGeo
![](https://img.shields.io/badge/python-3.8.12-green)![](https://img.shields.io/badge/pytorch-1.8.2-green)![](https://img.shields.io/badge/cudatoolkit-10.2.89-green)![](https://img.shields.io/badge/cudnn-7.6.5-green)

This folder provides a reference implementation of **RIPGeo**, as described in the paper: 

**RIPGeo: Robust Street-Level IP Geolocation**


## Basic Usage

### Requirements

The code was tested with `python 3.8.12`, `pytorch 1.8.2`, `cudatookkit 10.2.89`, and `cudnn 7.6.5`. Install the dependencies via [Anaconda](https://www.anaconda.com/):

```shell
# create virtual environment
conda create --name RIPGeo python=3.8.12

# activate environment
conda activate RIPGeo

# install pytorch & cudatoolkit
conda install pytorch torchvision torchaudio cudatoolkit=10.2 -c pytorch-lts

# install other requirements
conda install numpy pandas
pip install scikit-learn
```

### Run the code
```shell
### we run our model on the New York dataset as an example.
# Open the "RIPGeo" folder
cd RIPGeo

# loda data from the region and execute IP clustering. 
python preprocess.py --dataset "New_York" 

# run the model RIPGeo
python main.py --dataset "New_York" --dim_in 30
```

## Folder Structure

```tex
└── GraphGeo
	├── datasets # contains datasets from three regions for street-level IP geolocation
	│	|── Los_Angeles
	│	|── New_York
	│	|── Shanghai
	├── lib # contains model implementation files
	│	|── layers.py # The code of the attention mechanism.
	│	|── model.py # The core source code of proposed RIPGeo
	│	|── sublayers.py # The support file for layer.py
	│	|── utils.py # Auxiliary functions, including the code of perturbational training
	├── preprocess.py # Load dataset and execute IP clustering the for model running
	├── main.py # Run model for training and test
	└── README.md
```

## Dataset Information

The "datasets" folder contains three subfolders corresponding to the datasets collected from different regions. There are three files in each subfoler:

- data.csv    *# features and labels for street-level IP geolocation* 
- ip.csv    *# IP addresses*
- last_traceroute.csv    # last four routers and coressponding delays for efficient IP host clustering

Since our source data is larger than GitHub's recommended maximum file size of 50.00 MB, we upload a small part of them as samples. When the the process of anonymous review is over, we will upload the full dataset to google drive.

The detailed **columes and description** of each dataset are as follows:

#### New York & Los Angeles

| Column Name                     | Data Description                                             |
| ------------------------------- | ------------------------------------------------------------ |
| ip                              | The IPv4 address                                             |
| as_mult_info                    | The ID of the autonomous system where IP locates             |
| country                         | The country where the IP locates                             |
| prov_cn_name                    | The state/province where the IP locates                      |
| city                            | The city where the IP locates                                |
| isp                             | The Internet Service Provider of the IP                      |
| vp900/901/..._ping_delay_time   | The ping delay from probing hosts "vp900/901/..." to the IP host |
| vp900/901/..._trace             | The traceroute list from probing hosts "vp900/901/..." to the IP host |
| vp900/901/..._tr_steps          | #steps of the traceroute from probing hosts "vp900/901/..." to the IP host |
| vp900/901/..._last_router_delay | The delay from the last router to the IP host in the traceroute list from probing hosts "vp900/901/..." |
| vp900/901/..._total_delay       | The total delay from probing hosts "vp900/901/..." to the IP host |
| longitude                       | The longitude of the IP (as label)                           |
| latitude                        | The latitude of the IP host (as label)                       |

#### Shanghai

| Column Name                       | Data                                                         |
| --------------------------------- | ------------------------------------------------------------ |
| numip                             | The IPv4 address                                             |
| asnumber                          | The ID of the autonomous system where IP locates             |
| scene                             | The IP usage scenario                                        |
| isp                               | The Internet Service Provider of the IP                      |
| asname                            | The name of the autonomous system where the IP locates       |
| orgname                           | The ISP organization of the IP host                          |
| address                           | The address of the ISP                                       |
| port_80/443/..._alive             | The opening status of the IP host's port 80/443/...          |
| aiwen/vp813/..._ping_delay_time   | The ping delay from probing hosts "aiwen/vp813/..." to the IP host |
| aiwen/vp813/..._trace             | The traceroute list from probing hosts "aiwen/vp813/..." to the IP host |
| aiwen/vp813/..._tr_steps          | #steps of the traceroute from probing hosts "aiwen/vp813/..." to the IP host |
| aiwen/vp813/..._last_router_delay | The delay from the last router to the IP host in the traceroute liist from probing hosts "aiwen/vp813/..." |
| aiwen/vp813/..._total_delay       | The total delay from probing hosts "aiwen/vp813/..." to the IP host |
| longitude                         | The longitude of the IP (as label)                           |
| latitude                          | The latitude of the IP host (as label)                       |


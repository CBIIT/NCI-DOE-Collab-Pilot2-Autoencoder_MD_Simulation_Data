# NCI-DOE-Collab-Pilot1-Tumor_Classifier Technical README

## Overview

An autoencoder is a neural network that reduces its inputs to a smaller set of features ("encoder" part) and subsequently builds the features back up ("decoder" part) from the minimally-sized "latent space" while attempting to accurately recreate the inputs. As long as the "reconstruction loss" is small, the encoder part of the model can be trusted to perform just the reduction part of the algorithm in order to minimize the number of "features" of the input data necessary to faithfully describe the input data. Thus, an autoencoder is often used as a dimensionality reduction model. Often the utility of such dimensionality reduction algorithms is to generate from a large input dataset a tractable set of features that you can then feed into additional models used for a variety of purposes; this was the original intent of the P2B1 benchmark.

The P2B1 benchmark performs these steps on a molecular dynamics (MD) simulation state (including Protein Data Bank files resulting from a coarse-grained bead simulation) of a "disordered," three-component system (DPPC-DOPC-CHOL). The default system consists of 3,000 lipids and 3,000 frames simulated for 10 microseconds. The implemented network is a convolutional neural network that very quickly and effectively minimizes the reconstruction loss. For a detailed description of the autoencoder model used, refer to the "Model Summary" section of [p2b1_sample_output.txt](./p2b1_sample_output.txt).

If you want to examine the data without having to run the model, refer to the following assets in the Model and Data Clearinghouse (MoDaC):
* The default dataset is [3k disordered 3-component-system (DPPC-DOPC-CHOL)](https://modac.cancer.gov/searchTab?dme_data_id=NCI-DME-MS01-7654212).
* The converged model is [Autoencoder for MD Simulation Data (P2B1)](https://modac.cancer.gov/searchTab?dme_data_id=NCI-DME-MS01-7681692).

## Setup

Clone this repository to your machine. If you use [NIH's Biowulf supercomputer](https://hpc.nih.gov), be sure to use the data partition. For example:

```bash
# On Biowulf, be sure to use the data partition
cd /data/$USER

# Clone and enter this GitHub repository
git clone git@github.com:CBIIT/NCI-DOE-Collab-Pilot2-Autoencoder_MD_Simulation_Data.git
cd NCI-DOE-Collab-Pilot2-Autoencoder_MD_Simulation_Data
```

Using the default test dataset (`3k_Disordered`), running the model requires a large amount of memory, likely over 100 GB. It is therefore prudent to use a large-memory computer or Biowulf. For example, to test the model using an interactive node on Biowulf, allocate a node as in the following example:

```bash
# On Biowulf
sinteractive --gres=gpu:k80:1 --mem=150G
```

As of May 2021, the default Python environment on Biowulf is sufficient for running the model; you can load this using:

```bash
# On Biowulf
module load python
```

If you are not on Biowulf--or the default Python environment on Biowulf is out of date--you can instead create a sufficient Python environment by installing the [Conda environment manager](https://docs.conda.io/en/latest) and then running:

```bash
conda env create -f python_environment.yml -n P2B1
conda activate P2B1
```

To download the data the model uses for training:
1.	Create an account on the Model and Data Clearinghouse (MoDaC) [login page](https://modac.cancer.gov/loginTab).
2.	Follow the instructions in the Training section below.
3.	When prompted during the training procedure, enter your MoDaC credentials.

## Training

You can use the following script to run the model on the default dataset described above:

```bash
cd ./Pilot2/P2B1
python p2b1_baseline_keras2.py
```

This script trains the model with the parameters set in the file [p2b1_default_model.txt](./p2b1_default_model.txt) on the default dataset. Sample output looks like [p2b1_sample_output.txt](./p2b1_sample_output.txt).

The script outputs to the working directory the model topology files `model.json` (encoder+decoder) and `encoder.json` (encoder only). After each epoch, the script creates a directory with the name `epoch_X` (X=1,2,3,...) containing the corresponding trained weights files (`model_weights.hdf5` and `encoder_weights.hdf5`) calculated at the end of the corresponding epoch. You can use the two full model files to generate reconstructed inputs (on the training or new data); you can use the two encoder files to generate the compressed, latent space (on the training or new data).

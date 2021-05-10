# NCI-DOE-Collab-Pilot2-Autoencoder_MD_Simulation_Data

### Description:
The P2B1 capability (P2B1) is an autoencoder that determines a set of features to most efficiently describe molecular dynamics simulation data.

### User Community:	
Researchers interested in working with efficient representations of molecular dynamics simulation data.

### Usability:	
Data scientists can train the model on their own data and use the resulting reduced set of features as input for further analysis.

### Uniqueness:	
Molecular simulation data consist of many descriptors. This capability shows how you can use an autoencoder to compress these descriptors into a minimal set that faithfully describes the data. This enables downstream analysis using a more tractable dataset as input.

### Components:	
* Data:
  * The default dataset (3k disordered 3-component-system [DPPC-DOPC-CHOL]) used for this asset is stored in [MoDaC](https://modac.cancer.gov/searchTab?dme_data_id=NCI-DME-MS01-7654212).
* Model:
  * The trained weights (for both the full model and just the encoder; `.hdf5` files) and the corresponding model topologies (`.json` files) are stored in [MoDaC](https://modac.cancer.gov/searchTab?dme_data_id=NCI-DME-MS01-7681692).

### Technical Details:
Refer to this [README](./Pilot2/P2B1/README.md).

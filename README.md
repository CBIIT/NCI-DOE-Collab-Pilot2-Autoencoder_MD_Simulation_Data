# NCI-DOE-Collab-Pilot2-Autoencoder_MD_Simulation_Data

### Description
The P2B1 capability (P2B1) is an autoencoder that determines a set of features to most efficiently describe molecular dynamics (MD) simulation data.

### User Community
Scientists interested in working with efficient representations of MD simulation data.

### Usability
Scientists can train the model on their own data and use the resulting reduced set of features as input for further analysis.

### Uniqueness
MD simulation data consist of many descriptors. This capability shows how you can use an autoencoder to compress these descriptors into a minimal set that faithfully describes the data. This enables downstream analysis using a more tractable dataset as input.

### Components
The following components are in the Model and Data Clearinghouse (MoDaC):
* Data:
  * The default dataset is [3k disordered 3-component-system (DPPC-DOPC-CHOL)](https://modac.cancer.gov/searchTab?dme_data_id=NCI-DME-MS01-7654212).
* Converged Model:
  * The trained weights (for both the full model and just the encoder; `.hdf5` files) and the corresponding model topologies (`.json` files) are stored in [Autoencoder for MD Simulation Data (P2B1)](https://modac.cancer.gov/searchTab?dme_data_id=NCI-DME-MS01-7681692).

### Technical Details
Refer to this [README](./Pilot2/P2B1/README.md).

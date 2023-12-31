# High-Resolution Astronomy with X-Rays (HIRAX) Spacecraft Radiation Model

The HIgh-Resolution Astronomy with X-rays mission, HIRAX was conceptualised at the University of Leicester as part of the research phase for the Space Exploration Systems MSc program. It involved a six-month comprehensive feasibility study for an M-class space X-ray interferometer mission with the capability of micro-arcsecond-level resolution in the soft X-ray energy band. The sub-systems directly affecting the science goals and objective of the instrument were studied as part of a feasibility study. 

The shielding and protection sub-system was a part of the thermomechanical work package for HIRAX spacecraft and was conceptualised using first principles and ECSS standards. Only the detectors were considered for shielding against the focused X-ray background and particulate radiation. Validation models in the form of box and sphere models were constructed for the full spacecraft model results verification.

# GRAS: Geant4 Radiation Analysis for Space 

The Geant4 Radiation Analysis for Space (GRAS), a Geant4 (G4) based tool has been used to perform the 
shielding studies for HIRAX XRI detectors. It is an extension that simulates the radiation particle interactions
with matter using the Monte Carlo algorithm focusing on space environment effects. GRAS version 05-00-01 implemented in the NoMachine virtual environment on the University of Leicester’s high-performance 
computing SPECTRE cluster was used to perform reverse Monte Carlo (RMC) simulation at 0.1% precision.  

To simulate radiation transport in three-dimensional geometries, three quantities are defined in Geant4: 
1. Source definitions  
2. Geometry construction 
3. Physics of interaction 
4. Analysis to be done 

Reverse (or adjoint) Monte Carlo simulation techniques which require the definition of targets as adjoint sources to reduce simulation times have a specialised RMC physics class defined in G4 (refer to section 3.4). GRAS/G4 simulate the path of the primary particle and the information relating to the generated particle and its interactions are stored as provided in comma-separated value (CSV) or ROOT files. The simulated radiation transport techniques and related variables are defined in G4 classes by default and can be altered by the user given the open-source nature of the toolkit. An example of the variables discovered to have default limits was the cross-section of individual particles.  

The production thresholds or Cuts can be set for the generation of secondaries as length in millimetres. Low 
production thresholds generate higher secondaries at the expense of computing power. However, RMC doesn’t 
allow changing default threshold energies for secondaries. The cuts are applied for the production of secondaries for gammas (γ) due to inelastic scattering processes, electrons (e-) due to ionisation, positrons (e+) and protons by elastic scattering. 

The GRAS/Geant4 offers a wide range of analysis modules normalised by the number of primary events. The Total Ionising Dose (TID), fluence, Non-Ionising Energy Loss (NIEL), Total Non-Ionising Doses (TNID), path length, Linear Energy Transfer (LET), Charge Collection Analysis (CCA), sensitive detector and source analysis are supported. Point detector adjoint simulation in RMC has been implemented and according to GRAS User Guide, it computes specifically secondary fluence and dose deposited in silicon-sensitive volumes based on stopping powers, mass attenuation coefficients for e-, protons and gamma. 

# Code Assist

### The source definition:
The sources are definite in the files present in the _source_ folder and are generated from SPENVIS for galactic cosmic rays and solar protons using the CREME-96 and the ESP model. The files supported by forward Monte Carlo (FMC) and reverse Monte Carlo (RMC) are present.

The final source particle histograms can also be obtained in the output file by specifying it in the _macros_ file being run.

### The geometry GDML files:
These files can be run on the GRAS graphic window after specifying which file to run in _macros/viewer.g4mac_ and entering the following command:
```
/control/execute macros/viewer.g4mac
```
The geometry files consist of basic spacecraft models in sphere and box configurations and the full spacecraft model of the HIRAX spacecraft given below.

![image](https://github.com/aditikatoch/HIRAX_Radiation_Model/assets/56295364/47542a36-f1eb-4b63-a092-f14bf5d7cc96)

### Physics interactions:
For the interactions of source particles and the spacecraft material, Geant4 physics interactions added were the reverse Monte Carlo (RMC) physics given the complexity of the spacecraft. The files in the _physics_ folder contain the FMC options and the RMC physics file. More information about these can be found on Geant4 and GRAS websites. 

### The analysis files:
These are the main program files in the _macros_ folder that consist of all the definitions, aliases and final outputs that are desired. These files can be run directly in the command window specifying which file to run. The files are named according to which volume is considered as the target volume. Except for _modular_macro.g4mac_ all the other files are coded to run reverse Monte Carlo simulations. _modular_macro_rmc_d.g4mac_ has detector as target and _modular_macro_rm_m1.g4mac_ and the consequent numbers _m2, m3, m4_ are for the mirror configuration 1, 2, 3 and 4 where _m2_ is the slatted mirror configuration.

The code to execute these files, for example for the detector file, is:
```
gras macros/modular_macro_rmc_d.g4mac
```



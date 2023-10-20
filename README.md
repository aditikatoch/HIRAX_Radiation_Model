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


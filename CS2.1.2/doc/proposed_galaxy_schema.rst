This schema is meant to provide definitions for quantities we expect simulated catalogs to contain.  Not every
catalog will contain every quantity in this schema, however, when they do, we hope that they will adhere to the
definitions below.  Put another way: a catalog may not characterize the shapes of galaxies, but if it does, it will
do so as specified below.  The schema is agnostic to the question of how the data is delivered (it can be a database,
a text file, a FITS file, or something else unthought of).  The schema merely speaks to the contents of the files
being delivered.  This is so that DESC science working groups can write their software tools confident in what inputs
they will be receiving.  Quantities are marked as either 'Observed' (in which case they are quantities that we expect
science working groups to be able to use directly at the catalog level) or 'Truth' (in which case they represent
physical truth which may be unobservable, but which we are delivering so that working groups can validate the
results of their analysis tools).

The following metadata will be expected for all cosmological simulations.

- The cosmology used to generate the simulation.
- Definitions (including units) for any columns included beyond the minimal schema.
- Detailed explanation of the dust model internal to galaxies (if any) used.  This should include details of
both implementation and parametrization.
- A library (or a pointer to a library) of SEDs associated with each galaxy (if applicable).
- An indication of the specific version of the LSST bandpass throughputs used to calculate magnitudes.

+-------------------+------------+----------------+-----------------------------+-----------------+------------+----------+
| Quantity          | Units      | Truth/Observed | Definition                  | Working Group   | Input      | Accuracy |
|                   |            |                |                             | Use Case        | For...     | Required |
+===================+============+================+=============================+=================+============+==========+
| ID                | int        | Observed       | A unique identifier for     |                 | PhoSim     |          |
|                   |            |                | every galaxy in the catalog.|                 | optional   |          |
+-------------------+------------+----------------+-----------------------------+-----------------+------------+----------+
| **Comment:** We must determine how to handle unique IDs in the case of compound systems                                 |
| (both multi-component galaxies and multiply-lensed images).  The two most straightforward options are:                  |
|                                                                                                                         |
| 1) Deliver multiple tables/files, one file for each component (and one for the aggregate system). Each component of     |
| a single system will reside in a different table. Components of the same system will share an ID across tables.         |
| **The idea of an aggregate system does not make sense for multiply-lensed images.**                                     |
|                                                                                                                         |
|                                                                                                                         |
| 2) In addition to ID, each object will contain a ParentID linking it to its sibling components and                      |
| (if applicable) the aggregate system.                                                                                   |
|                                                                                                                         |
| We may also want to keep track of the halo ID from the simulation so that users can reconstruct the merger              |
| history if they want.                                                                                                   |
|                                                                                                                         |
+-------------------+------------+----------------+-----------------------------+-----------------+------------+----------+
| RA                | degrees    | Observed       | ICRS.  Reckoned from the    |                 | PhoSim     |          |
|                   | (decimal)  |                | flux-weighted centroid of   |                 | required   |          |
|                   |            |                | the galaxy or galaxy        |                 |            |          |
|                   |            |                | component.                  |                 |            |          |
+-------------------+------------+----------------+-----------------------------+                 |            |          |
| Dec               | degrees    | Observed       | ICRS.  Reckoned from the    |                 |            |          |
|                   | (decimal)  |                | flux-weighted centroid of   |                 |            |          |
|                   |            |                | the galaxy or galaxy        |                 |            |          |
|                   |            |                | component.                  |                 |            |          |
+-------------------+------------+----------------+-----------------------------+-----------------+------------+----------+
| **Comment:** This could be (i.e. 'technically is') bandpass-dependent.                                                  |
+-------------------+------------+----------------+-----------------------------+-----------------+------------+----------+
| Redshift          | float      | Observed       | Observed heliocentric       |                 | PhoSim     |          |
|                   |            |                | redshift due to both the    |                 | optional   |          |
|                   |            |                | Hubble flow and any         |                 |            |          |
|                   |            |                | peculiar motion of the      |                 |            |          |
|                   |            |                | galaxy.                     |                 |            |          |
+-------------------+------------+----------------+-----------------------------+-----------------+------------+----------+
| Sersic index      | float      | Observed       | Observed best fit Sersic    |                 | PhoSim     |          |
|                   |            |                | index of the galaxy's       |                 | recommended|          |
|                   |            |                | on-sky profile.             |                 |            |          |
+-------------------+------------+----------------+-----------------------------+-----------------+------------+----------+
| **Comment:** Every component of the galaxy will be fit to a Sersic profile.  The aggregate galaxy will also be          |
| represented by the best-fit Sersic index for the whole system.  It has been pointed out that the Sersic index of the    |
| entire system will be a poor fit. We may want to consider different profiles (e.g. mixtures of Gaussians or Moffatt     |
| profiles).                                                                                                              |
|                                                                                                                         |
| Adrian Pope has volunteered to research different profiles and how easily they can be transformed into observable       |
| quantities.                                                                                                             |
+-------------------+------------+----------------+-----------------------------+-----------------+------------+----------+
| Semi-major axis   | milli-     | Observed       | The observed semi-major     |                 | PhoSim     |          |
|                   | arcseconds |                | axis of the galaxy.         |                 | recommended|          |
|                   |            |                |                             |                 |            |          |
+-------------------+------------+----------------+-----------------------------+                 |            |          |
| Semi-minor axis   | milli-     | Observed       | The observed semi-minor     |                 |            |          |
|                   | arcseconds |                | axis of the galaxy.         |                 |            |          |
+-------------------+------------+----------------+-----------------------------+-----------------+------------+----------+
| **Comment:** PhoSim works in arcseconds rather than milli-arcseconds.  This may be a more natural choice for units.     |
|                                                                                                                         |
| We need to define where these axes are defined (i.e. at a certain isophote?).                                           |
|                                                                                                                         |
| Elisa Chisari suggests we store several sets of axes at several isophotes so that we can interpolate a realistic        |
| luminosity profile.                                                                                                     |
|                                                                                                                         |
| May be bandpass dependent.                                                                                              |
+-------------------+------------+----------------+-----------------------------+-----------------+------------+----------+
| Position Angle    | degrees    | Observed       | Rotation of the semi-major  |                 | PhoSim     |          |
|                   | (decimal)  |                | axis eastward of North.     |                 | recommended|          |
+-------------------+------------+----------------+-----------------------------+-----------------+------------+----------+
| **Comment:** This would also require multiple values at multiple isophotes.                                             |
|                                                                                                                         |
+-------------------+------------+----------------+-----------------------------+-----------------+------------+----------+
| Av                | magnitudes | Observed       | Extinction due to dust in   |                 | PhoSim     |          |
|                   |            |                | the galaxy/component.       |                 | optional   |          |
+-------------------+------------+----------------+-----------------------------+-----------------+------------+----------+
| Rv                | magnitudes | Observed       | Reddening due to dust in    |                 | PhoSim     |          |
|                   |            |                | the galaxy/component.       |                 | optional   |          |
+-------------------+------------+----------------+-----------------------------+-----------------+------------+----------+
| Extinction model  | str        | Observed       | Model of extinction inside  |                 | PhoSim     |          |
|                   |            |                | the galaxy (or galaxy       |                 | optional   |          |
|                   |            |                | component).  Examples: CCM, |                 |            |          |
|                   |            |                | O'Donnell,etc.              |                 |            |          |
+-------------------+------------+----------------+-----------------------------+-----------------+------------+----------+
| SED               | str        | Observed       | Some way that catalog       | PZ1.1           | PhoSim     |          |
|                   |            |                | generation code can         |                 | recommended|          |
|                   |            |                | associate the galaxy/       |                 |            |          |
|                   |            |                | component with an SED.      |                 |            |          |
+-------------------+------------+----------------+-----------------------------+-----------------+------------+----------+
| **Comment:** We may end up needing to support SED basis functions, in which case we would need to specify               |
| the library of basis functions and a list of weights used to recreate the SED.                                          |
|                                                                                                                         |
| We can also provide support for multiple SED and Normalization columns as a way to specify that an SED is a             |
| linear combination of basis functions.                                                                                  |
|                                                                                                                         |
+-------------------+------------+----------------+-----------------------------+-----------------+------------+----------+
| Normalization     | magnitudes | Observed       | Some way to normalize the   |                 | PhoSim     |          |
|                   |            |                | SED.                        |                 | required   |          |
+-------------------+------------+----------------+-----------------------------+-----------------+------------+----------+
| **Comment:** The current scheme in CatSim is to store the rest-frame AB magnitude of the SED in a delta-function        |
| bandpass at 500nm.  This is the system that PhoSim uses. Unfortunately, it fails in the case where the SED has          |
| zero flux at 500nm.                                                                                                     |
+-------------------+------------+----------------+-----------------------------+-----------------+------------+----------+
| u_ab              | AB         | Observed       | Above-the-atmosphere AB     |                 |            |          |
|                   | magnitudes |                | magnitude in LSST filters.  |                 |            |          |
+-------------------+            |                | Extincted by internal dust. |                 |            |          |
| g_ab              |            |                | Unextincted by the Milky    |                 |            |          |
|                   |            |                | Way.  Includes mean AGN     |                 |            |          |
+-------------------+            |                | flux.                       |                 |            |          |
| r_ab              |            |                |                             |                 |            |          |
|                   |            |                |                             |                 |            |          |
+-------------------+            |                |                             |                 |            |          |
| i_ab              |            |                |                             |                 |            |          |
|                   |            |                |                             |                 |            |          |
+-------------------+            |                |                             |                 |            |          |
| z_ab              |            |                |                             |                 |            |          |
|                   |            |                |                             |                 |            |          |
+-------------------+            |                |                             |                 |            |          |
| y_ab              |            |                |                             |                 |            |          |
|                   |            |                |                             |                 |            |          |
+-------------------+------------+----------------+-----------------------------+-----------------+------------+----------+
| Point_source_SED  | str        | Observed       | Some means of identifying   |                 |            |          |
|                   |            |                | the SED of a point source   |                 |            |          |
|                   |            |                | (e.g an AGN) associated     |                 |            |          |
|                   |            |                | galaxy the galaxy/component |                 |            |          |
+-------------------+------------+----------------+-----------------------------+-----------------+------------+----------+
| **Comment:** The same caveats apply here as applied to the SED column for the whole galaxy/component.                   |
+-------------------+------------+----------------+-----------------------------+-----------------+------------+----------+
| Point_source_norm | magnitudes | Observed       | Some way to normalize the   |                 |            |          |
|                   |            |                | point source SED.           |                 |            |          |
|                   |            |                |                             |                 |            |          |
+-------------------+------------+----------------+-----------------------------+-----------------+------------+----------+
| **Comment:** The same caveats apply here as applied to the normalization of the entire galaxy's SED.                    |
+-------------------+------------+----------------+-----------------------------+-----------------+------------+----------+
| Inclination Angle | degrees    | Truth          | Inclination of the galaxy   |                 |            |          |
|                   | (decimal)  |                | (or galaxy component)       |                 |            |          |
|                   |            |                | relative to the line of     |                 |            |          |
|                   |            |                | sight.                      |                 |            |          |
+-------------------+------------+----------------+-----------------------------+-----------------+------------+----------+
| Cosmological      | float      | Truth          | Heliocentric redshift due   |                 |            |          |
| Redshift          |            |                | only to the Hubble flow.    |                 |            |          |
+-------------------+------------+----------------+-----------------------------+-----------------+------------+----------+
| **Comment:** This is truth information that allows users to disentangle redshift due to proper motion from              |
| redshift due to the Hubble flow. We must be careful with our naming convention to make it obvious how this              |
| differs from the total redshift column.                                                                                 |
+-------------------+------------+----------------+-----------------------------+-----------------+------------+----------+
| Mass_gas          | Solar      | Truth          | The mass of the gas in the  | WL2.3.2         |            |          |
|                   | masses     |                | galaxy/galaxy component.    |                 |            |          |
+-------------------+------------+----------------+-----------------------------+-----------------+            |          |
| Mass_stellar      | Solar      | Truth          | The mass of stars in the    | PZ: 1.1.2, DC2, |            |          |
|                   | masses     |                | galaxy/component.           | DC3; WL2.3.2    |            |          |
+-------------------+------------+----------------+-----------------------------+-----------------+            |          |
| Mass_halo         | Solar      | Truth          | The mass of the dark matter |                 |            |          |
|                   | masses     |                | halo of the galaxy/component|                 |            |          |
+-------------------+------------+----------------+-----------------------------+-----------------+------------+----------+
| **Comment:** It has been pointed out that not all simulations might be able to deliver these masses, in which           |
| case they may not belong in the minimal schema.                                                                         |
+-------------------+------------+----------------+-----------------------------+-----------------+------------+----------+
| Bulge_to_total    | float      | Truth          | Ratio of the bolometric     |                 |            |          |
|                   |            |                | flux from the galaxy's bulge|                 |            |          |
|                   |            |                | to the total bolometric flux|                 |            |          |
|                   |            |                | of the galaxy.              |                 |            |          |
+-------------------+------------+----------------+-----------------------------+                 |            |          |
| Disk_to_total     | float      | Truth          | Ratio of the bolometric flux|                 |            |          |
|                   |            |                | from the galaxy's disk to   |                 |            |          |
|                   |            |                | the total bolometric flux of|                 |            |          |
|                   |            |                | the galaxy.                 |                 |            |          |
+-------------------+------------+----------------+-----------------------------+-----------------+------------+----------+
| **Comment:** Bulge_to_total and Disk_to_total will not sum to unity in the presence of an AGN.                          |
|                                                                                                                         |
| What do we mean by 'bolometric'? Just in the range of LSST bandpasses?  In a single LSST bandpass?  Restframe or        |
| observed?                                                                                                               |
+-------------------+------------+----------------+-----------------------------+-----------------+------------+----------+
| Barycentric_RA    | degrees    | Truth          | ICRS.  Defined according to | CL1.1           |            |          |
|                   | (decimal)  |                | the system's center of mass.|                 |            |          |
+-------------------+------------+----------------+-----------------------------+                 +------------+----------+
| Barycentric_Dec   | degrees    | Truth          | ICRS.  Defined according to |                 |            |          |
|                   | (decimal)  |                | the system's center of mass.|                 |            |          |
+-------------------+------------+----------------+-----------------------------+-----------------+------------+----------+

Other quantities we might want to consider supporting:

- Halo mass profile parameters
- Distance from center of dark matter halo
- Other characterizations of a galaxy's environment
- Some way to associate clusters of galaxies with each other
- Shear parameters (as defined/interpreted by PhoSim)

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

+-------------------+------------+----------------+-----------------------------+------------------------------------+
| Quantity          | Units      | Truth/Observed | Definition                  | Comment                            |
+===================+============+================+=============================+====================================+
| ID                | int        | Observed       | A unique identifier for     | We must determine how to handle    |
|                   |            |                | every galaxy in the catalog.| unique IDs in the case of compound |
|                   |            |                |                             | systems (both multi-component      |
|                   |            |                |                             | galaxies and multiply-lensed       |
|                   |            |                |                             | images).  The two most             |
|                   |            |                |                             | straightforward options are:       |
|                   |            |                |                             |                                    |
|                   |            |                |                             | 1) Deliver multiple tables/files,  |
|                   |            |                |                             | one file for each component (and   |
|                   |            |                |                             | one for the aggregate system).     |
|                   |            |                |                             | Each component of a single system  |
|                   |            |                |                             | will reside in a different table.  |
|                   |            |                |                             | Components of the same system will |
|                   |            |                |                             | share an ID across tables.         |
|                   |            |                |                             | **The idea of an aggregate system  |
|                   |            |                |                             | does not make sense for multiply-  |
|                   |            |                |                             | lensed images.**                   |
|                   |            |                |                             |                                    |
|                   |            |                |                             | 2) In addition to ID, each object  |
|                   |            |                |                             | will contain a ParentID linking it |
|                   |            |                |                             | to its sibling components and (if  |
|                   |            |                |                             | applicable) the aggregate system.  |
+-------------------+------------+----------------+-----------------------------+------------------------------------+
| RA                | degrees    | Observed       | ICRS.  Reckoned from the    |                                    |
|                   |            |                | flux-weighted centroid of   |                                    |
|                   |            |                | the galaxy or galaxy        |                                    |
|                   |            |                | component.                  |                                    |
+-------------------+------------+----------------+-----------------------------+------------------------------------+
| Dec               | degrees    | Observed       | ICRS.  Reckoned from the    |                                    |
|                   |            |                | flux-weighted centroid of   |                                    |
|                   |            |                | the galaxy or galaxy        |                                    |
|                   |            |                | component.                  |                                    |
+-------------------+------------+----------------+-----------------------------+------------------------------------+
| Redshift          | float      | Observed       | Observed heliocentric       |                                    |
|                   |            |                | redshift due to both the    |                                    |
|                   |            |                | Hubble flow and any         |                                    |
|                   |            |                | peculiar motion of the      |                                    |
|                   |            |                | galaxy.                     |                                    |
+-------------------+------------+----------------+-----------------------------+------------------------------------+
| Sersic index      | float      | Observed       | Observed best fit Sersic    | Every component of the galaxy will |
|                   |            |                | index of the galaxy's       | be fit to a Sersic profile.  The   |
|                   |            |                | on-sky profile.             | aggregate galaxye will also be     |
|                   |            |                |                             | represetned by the best-fit Sersic |
|                   |            |                |                             | index for the whoel system.  It    |
|                   |            |                |                             | has been pointed out that the      |
|                   |            |                |                             | Sersic index of the entire system  |
|                   |            |                |                             | will be a poor fit.  It may be     |
|                   |            |                |                             | worth exploring the use of         |
|                   |            |                |                             | different profiles (mixtures of    |
|                   |            |                |                             | Gaussians, Moffatt profiles, etc.) |
|                   |            |                |                             | if they are not too burdensome for |
|                   |            |                |                             | simulators to deliver.             |
+-------------------+------------+----------------+-----------------------------+------------------------------------+
| Semi-major axis   | milli-     | Observed       | The observed semi-major     | PhoSim works in arcseconds rather  |
|                   | arcseconds |                | axis of the galaxy.         | than milli-arcseconds.  This may   |
|                   |            |                |                             | be a more natural choice for       |
|                   |            |                |                             | units.                             |
+-------------------+------------+----------------+-----------------------------+                                    |
| Semi-minor axis   | milli-     | Observed       | The observed semi-minor     |                                    |
|                   | arcseconds |                | axis of the galaxy.         |                                    |
|                   |            |                |                             |                                    |
+-------------------+------------+----------------+-----------------------------+------------------------------------+
| Position Angle    | degrees    | Observed       | Rotation of the semi-major  |                                    |
|                   |            |                | axis eastward of North.     |                                    |
+-------------------+------------+----------------+-----------------------------+------------------------------------+
| Av                | magnitudes | Observed       | Extinction due to dust in   |                                    |
|                   |            |                | the galaxy/galaxy component.|                                    |
+-------------------+------------+----------------+-----------------------------+------------------------------------+
| Rv                | magnitudes | Observed       | Reddenting due to dust in   |                                    |
|                   |            |                | the galaxy/galaxy component.|                                    |
+-------------------+------------+----------------+-----------------------------+------------------------------------+
| Extinction model  | str        | Observed       | Model of extinction inside  |                                    |
|                   |            |                | the galaxy (or galaxy       |                                    |
|                   |            |                | component).  Examples: CCM, |                                    |
|                   |            |                | O'Donnell,etc.              |                                    |
+-------------------+------------+----------------+-----------------------------+------------------------------------+
| SED               | str        | Observed       | Some way that catalog       | We may end up needing to support   |
|                   |            |                | generation code can         | SED basis functions, in which case |
|                   |            |                | associate the galaxy/galaxy | we would need to specify the       |
|                   |            |                | component with an SED.      | library of basis functions and     |
|                   |            |                |                             | a list of weights used to recreate |
|                   |            |                |                             | the SED.                           |
+-------------------+------------+----------------+-----------------------------+------------------------------------+
| Normalization     | magnitudes | Observed       | Some way to normalize the   | The current scheme in CatSim is to |
|                   |            |                | SED.                        | store the rest-frame AB magnitude  |
|                   |            |                |                             | of the SED in a delta-function     |
|                   |            |                |                             | bandpass at 500nm.  This is the    |
|                   |            |                |                             | system that PhoSim uses.           |
|                   |            |                |                             | Unfortunately, it fails in the     |
|                   |            |                |                             | case where the SED has zero flux   |
|                   |            |                |                             | at 500nm.                          |
+-------------------+------------+----------------+-----------------------------+------------------------------------+
| u_ab              | AB         | Observed       | Above-the-atmosphere AB     | Extincted by internal dust.        |
|                   | magnitudes |                | magnitude in LSST filters.  | Unextincted by the Milky Way.      |
+-------------------+            |                |                             | Includes mean AGN flux.            |
| g_ab              |            |                |                             |                                    |
|                   |            |                |                             |                                    |
+-------------------+            |                |                             |                                    |
| r_ab              |            |                |                             |                                    |
|                   |            |                |                             |                                    |
+-------------------+            |                |                             |                                    |
| i_ab              |            |                |                             |                                    |
|                   |            |                |                             |                                    |
+-------------------+            |                |                             |                                    |
| z_ab              |            |                |                             |                                    |
|                   |            |                |                             |                                    |
+-------------------+            |                |                             |                                    |
| y_ab              |            |                |                             |                                    |
|                   |            |                |                             |                                    |
+-------------------+------------+----------------+-----------------------------+------------------------------------+
| Point_source_SED  | str        | Observed       | Some means of identifying   | The same caveats apply here as     |
|                   |            |                | the SED of a point source   | applied to the SED column for the  |
|                   |            |                | (e.g an AGN) associated     | whole galaxy/component.            |
|                   |            |                | galaxy the galaxy/galaxy    |                                    |
|                   |            |                | component.                  |                                    |
|                   |            |                |                             |                                    |
|                   |            |                |                             |                                    |
+-------------------+------------+----------------+-----------------------------+------------------------------------+
| Point_source_norm | magnitudes | Observed       | Some way to normalize the   | The same caveats apply here as     |
|                   |            |                | point source SED.           | applied to the normalization of    |
|                   |            |                |                             | the entire galaxy's SED.           |
+-------------------+------------+----------------+-----------------------------+------------------------------------+
| Inclination Angle | degrees    | Truth          | Inclination of the galaxy   |                                    |
|                   |            |                | (or galaxy component)       |                                    |
|                   |            |                | relative to the line of     |                                    |
|                   |            |                | sight.                      |                                    |
+-------------------+------------+----------------+-----------------------------+------------------------------------+
| Luminosity        | Mpc        | Truth          |                             | This is truth information that     |
| Distance          |            |                |                             | allows users to disentangle        |
|                   |            |                |                             | redshift due to proper motion from |
|                   |            |                |                             | redshift due to the Hubble flow    |
|                   |            |                |                             | (assuming they know the true       |
|                   |            |                |                             | cosmology).                        |
+-------------------+------------+----------------+-----------------------------+------------------------------------+
| Mass_gas          | Solar      | Truth          | The mass of the gas in the  | It has been pointed out that not   |
|                   | masses     |                | galaxy/galaxy component.    | all simulations might be able to   |
+-------------------+------------+----------------+-----------------------------+ deliver these masses, in which     |
| Mass_stellar      | Solar      | Truth          | The mass of stars in the    | case they may not belong in the    |
|                   | masses     |                | galaxy/galaxy component.    | minimal schema.                    |
+-------------------+------------+----------------+-----------------------------+                                    |
| Mass_halo         | Solar      | Truth          | The mass of the dark matter |                                    |
|                   |            |                | halo of the galaxy/galaxy   |                                    |
|                   | masses     |                | component.                  |                                    |
|                   |            |                |                             |                                    |
|                   |            |                |                             |                                    |
+-------------------+------------+----------------+-----------------------------+------------------------------------+
| Bulge_to_total    | float      | Truth          | Ratio of the bolometric     | Bulge_to_total and Disk_to_total   |
|                   |            |                | flux from the galaxy's bulge| will not sum to unity in the       |
|                   |            |                | to the total bolometric flux| presence of an AGN.                |
|                   |            |                | of the galaxy.              |                                    |
+-------------------+------------+----------------+-----------------------------+                                    |
| Disk_to_total     | float      | Truth          | Ratio of the bolometric flux|                                    |
|                   |            |                | from the galaxy's disk to   |                                    |
|                   |            |                | the total bolometric flux of|                                    |
|                   |            |                | the galaxy.                 |                                    |
+-------------------+------------+----------------+-----------------------------+------------------------------------+
| Barycentric_RA    | degrees    | Truth          | ICRS.  Defined according to |                                    |
|                   |            |                | the system's center of mass.|                                    |
+-------------------+------------+----------------+-----------------------------+------------------------------------+
| Barycentric_Dec   | degrees    | Truth          | ICRS.  Defined according to |                                    |
|                   |            |                | the system's center of mass.|                                    |
+-------------------+------------+----------------+-----------------------------+------------------------------------+

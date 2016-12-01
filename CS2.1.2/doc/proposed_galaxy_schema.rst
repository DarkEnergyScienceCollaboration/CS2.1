This schema is meant to provide definitions for quantities which the Cosmological Simulations (CS) working group
will present to the broader collaboration.  Individual cosmological simulations may be generated with their
own native schemas.  In that case, the CS working group will provide software tools to translate that native
schema into the publicly-facing schema presented blow.  That being said, not every catalog will contain data necessary
to calculate every quantity in this schema (e.g. not every simuation may treat internal dust extinction within
each galaxy), however, when they do, the publicly facing schema will adhere to the definitions below.  Put another
way: a catalog may not characterize the shapes of galaxies, but if it does, the CS working group will translate those shape
characterizations into the definitions provided below.  The schema is agnostic to the question of how the data is
delivered (it can be a database,a text file, a FITS file, or something else unthought of).  The schema merely speaks to
the contents of the files being delivered.  This is so that DESC science working groups can write their software tools
confident in what inputs they will be receiving.  Quantities are marked as either 'Observed' (in which case they are
quantities that we expect science working groups to be able to use directly at the catalog level) or 'Truth' (in which
case they represent physical truth which may be unobservable, but which we are delivering so that working groups can
validate the results of their analysis tools).

Some simulations model galaxies as multiple components (bulge, disk, AGN).  In those cases, each component of each
galaxy will be represented by an individual row in the schema.  The rows will contain an identifying integer which
is unique to each galaxy (not unique to each component), which will allow users to associate components that come
from the same galaxy with each other.

The following metadata will be expected for all cosmological simulations.

- The cosmology used to generate the simulation.
- Definitions (including units) for any columns included beyond the minimal schema.
- Detailed explanation of the dust model internal to galaxies (if any) used.  This should include details of both implementation and parametrization.
- A library (or a pointer to a library) of SEDs associated with each galaxy (if applicable).
- An indication of the specific version of the LSST bandpass throughputs used to calculate magnitudes.

The minimal schema for cosmological simulations will be:

- Row identifier -- an identifying integer that is unique to each component of a galaxy.

- Galaxy identifier -- an identifying integer that is unique to each galaxy and associates components of
the same galaxy with each other

Other quantities we might want to consider supporting:

- Halo mass profile parameters
- Distance from center of dark matter halo
- Other characterizations of a galaxy's environment
- Some way to associate clusters of galaxies with each other
- Shear parameters (as defined/interpreted by PhoSim)
- Inclination Angle
- Barycentric RA, Dec
- Mass due to stars, gas, and dark matter

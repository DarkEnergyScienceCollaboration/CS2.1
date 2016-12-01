This schema is meant to provide definitions for quantities which the Cosmological Simulations (CS) working group
will present to the broader collaboration.  Individual simulations will be provided to the CS working group
in the "Internal Schema".  The CS working group will provide software tools to translate the "Internal Schema"
into the publicly-facing "External Schema".  That being said, not every catalog will contain data necessary
to calculate every quantity in this schema (e.g. not every simuation may treat internal dust extinction within
each galaxy), however, when they do, the publicly facing schema will adhere to the definitions below.  Put another
way: a catalog may not characterize the shapes of galaxies, but if it does, the CS working group will translate those shape
characterizations into the definitions provided below.  The schema is agnostic to the question of how the data is
delivered (it can be a database,a text file, a FITS file, or something else unthought of).  The schema merely speaks to
the contents of the files being delivered.  This is so that DESC science working groups can write their software tools
confident in what inputs they will be receiving.

Some simulations model galaxies as multiple components (bulge, disk, AGN).  In those cases, each component of each
galaxy will be represented by an individual row in the schema.  The rows will contain an identifying integer which
is unique to each galaxy (not unique to each component), which will allow users to associate components that come
from the same galaxy with each other.

Metadata
--------

The following metadata will be expected for all cosmological simulations.

- The cosmology used to generate the simulation.
- Definitions (including units) for any columns included beyond the minimal schema.
- Detailed explanation of the dust model internal to galaxies (if any) used.  This should include details of both implementation and parametrization.
- A library (or a pointer to a library) of SEDs associated with each galaxy (if applicable).
- An indication of the specific version of the LSST bandpass throughputs used to calculate magnitudes.

Internal Schema
---------------

- Row identifier -- an identifying integer that is unique to each component of a galaxy.

- Galaxy identifier -- an identifying integer that is unique to each galaxy and associates components of
  the same galaxy with each other

- Halo identifier -- an identifying integer unique to the Dark Matter halo containing the galaxy.

- Right ascension -- decimal degrees -- in the International Celestial Reference System.
  Measured for the barycenter of the galaxy/component.

- Declination -- decimal degrees -- in the International Celestial Reference System.
  Measures for the barycenter of the galaxy/component.

- Redshift -- unitless -- Due to both the Hubble flow and the galaxy/component's
  peculiar motion.

- Size -- model TBD

- True Shape -- model TBD

- Observed Shape -- model TBD

- Flux -- either the flux of the galaxy/component in the nominal LSST bands or the
  model SED plus a normalization.

External Schema
---------------

- Row identifier -- an identifying integer that is unique to each component of a galaxy.

- Galaxy identifier -- an identifying integer that is unique to each galaxy and associates components of
  the same galaxy with each other

- Halo identifier -- an identifying integer unique to the Dark Matter halo containing the galaxy.

- Right ascension -- decimal degrees -- in the International Celestial Reference System.
  Measured for the barycenter of the galaxy/component.

- Declination -- decimal degrees -- in the International Celestial Reference System.
  Measures for the barycenter of the galaxy/component.

- Redshift -- unitless -- Due to both the Hubble flow and the galaxy/component's
  peculiar motion.

- SED -- a pointer to the SED file in the provided library (see metadata above)
  associated with the galaxy/component (can neglect internal extinction, which
  is parametrized below).

- Flux normalization -- unitless -- the multiplicative factor by which to multiply
  the SED to get the observed magnitudes of the galaxy/component (applied before
  internal dust extinction).

- Profile Type -- specification of the shape model used for the galaxy/component
  (e.g. Sersic, Mixture of Gaussians, etc.).

- Profile Parameters -- parameters needed to specify the galaxy's shape, given the profile.

- Semi-Major Axis -- arcseconds -- half light radius of the galaxy/component semi-major axis.

- Semi-Minor Axis -- arcseconds -- half light radius ofthe galaxy/component's semi-minor axis.

- Internal Extinction Model -- specification of the dust law (CCM, O'Donnell, etc.) used to
  model extinction due to dust internal to the galaxy/component (set to 'None' if extinction
  is accounted for in the galaxy/component's model SED).

- Internal Extinction Parameters -- parameters (Av, Rv, etc.) needed to apply the extinction
  model to the galaxy/component's SED.

- Shear 1 -- unitless -- first weak lensing shear parameter.

- Shear 2 -- unitless -- second weak lensing shear parameter.

- Convergence -- unitless -- weaklensing convergence parameter.

Summary Table
-------------

The CS working group will also construct a summary table which treats galaxies as a whole,
aggregating their components.  The schema for this table will be:

- Galaxy identifier -- a unique integer.  The same as listed above for individual galaxy compoents.

- Right Ascension -- decimal degrees -- in the International Celestial Reference System.  Measured
  at the flux-weighted centroid of the total galaxy.

- Declination -- decimal degrees -- in the International Celestial Reference System.  Measured
  at the flux-weighted centroid of the total galaxy.

- Magnitudes -- observed magnitudes of the total galaxy in nominal LSST bands (ignore Milky Way dust;
  apply internal dust)

- Ellipticity -- the eccentricity of the galaxy's profile on the sky (use semi-major and
  semi-minor axes from above).  *Should we apply weak lensing shear?*

- Size -- model TBD

Halo Table
----------

Finally, there will be an optional table containing information about the Dark Matter
halos containing each galaxy.  Its schema will be:

- Halo identifier -- a unique integer allowing users to associate galaxies to their halos.

- Right Ascension -- decimal degrees -- in the International Celestial Reference System.
  Measured from the barycenter of the halo.

- Declination -- decimal degrees -- in the International Celestial Reference System.
  Measured from the barycenter of the halo.

- Redshift -- unitless -- due to the Hubble flow

- Mass -- in 10^10 solar masses.

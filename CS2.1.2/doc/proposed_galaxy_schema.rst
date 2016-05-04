=================  ==========  ==========================================================
Quantity           Units       Comment
=================  ==========  ==========================================================
ID                 int         A unique identifier for every galaxy in the catalog.
                               This identifier will be shared by all of the components
                               (bulge,disk,agn etc.) of a given galaxy even if those
                               components are stored in different tables.

RA                 degrees     ICRS.  Reckoned from the flux-weighted centroid of the
                               galaxy or galaxy component.

Dec                degrees     ICRS.  Reckoned from the flux-weighted centroid of the
                               galaxy or galaxy component.

Redshift           float       This will be the observed heliocentric redshift
                               due to both the Hubble flow and any peculiar
                               motion of the galaxy.

Luminosity Dist.   Mpc         This is truth information that allows uses to
                               disentangle redshift due to proper motion from
                               redshift due to the Hubble flow (assuming they
                               know the true cosmology).

Sersic index       float       Every component of the galaxy will be fit to a
                               Sersic profile.  The aggregate galaxy will also
                               be represented by the best-fit Sersic index for
                               the whole System.  *It has been pointed out that
                               the Sersic index of the entire system is
                               unphysical.  It may be worth exploring the use
                               of different profiles (mixture of Gaussians,
                               Moffatt profiles etc.) if they are not too
                               burdensome for simulators to deliver.*

Semi-major axis    milli-      The observed semi-major axis of the
                   arcseconds  galaxy. *PhoSim works in arcseconds
                               rather than milli-arcseconds.  This
                               may be a more natural choice for
                               units.*

Semi-minor axis    milli-      The observed semi-minor axis of the
                   arcseconds  galaxy.  *PhoSim works in arcseconds
                               rather than milli-arcseconds.  This
                               may be a more natural choise for
                               units.*

Position Angle     degrees     Rotation of the semi-major axis
                               eastward of North.

Inclination Angle  degrees     Inclination of the galaxy
                               (or galaxy component) relative to the line of
                               sight.

Av                 magnitudes  Extinction due to dust in the galaxy (or
                               galaxy component).

Rv                 magnitudes  Reddenting due to dust in the galaxy (or
                               galaxy component).

Extinction model   str         Model of extinction inside the galaxy (or
                               galaxy component).  Examples: CCM/O'Donnell
                               etc.

SED                str         Some way that catalog generation code can
                               associate the galaxy/galaxy component with
                               an SED.  *We may end up needing to support
                               SED basis functions in which case we would
                               need to specify the library of basis
                               functions and a list of weights used to
                               recreate the SED.*

Normalization      magnitudes  Some way to normalize the SED.  The current
                               scheme in CatSim is to store the rest-frame
                               AB mangitude of the SED in a delta-function
                               bandpass at 500nm.  This is the system that
                               PhoSim uses.  Unfortunately it fails in the
                               case where the SED has zero flux at 500nm.

Mass_gas           Solar       The mass of the gas in the galaxy, galaxy
                   masses      component.

Mass_stellar       Solar       The mass of stars in the galaxy, galaxy
                   masses      component.

Mass_halo          Solar       The mass of the dark matter halo of the
                   masses      galaxy, galaxy component.  *It has been
                               pointed out that not all simulations might
                               be able to deliver these masses in which
                               case they may not belong in the minimal
                               schema.*

u_ab               AB          Extincted by internal dust.  Unextincted by
                   magnitudes  Milky Way.  Includes mean AGN flux.

g_ab               AB          Extincted by internal dust.  Unextincted by
                   magnitudes  Milky Way.  Includes mean AGN flux.

r_ab               AB          Extincted by internal dust.  Unextincted by
                   magnitudes  Milky Way.  Includes mean AGN flux.

i_ab               AB          Extincted by internal dust.  Unextincted by
                   magnitudes  Milky Way.  Includes mean AGN flux.

z_ab               AB          Extincted by internal dust.  Unextincted by
                   magnitudes  Milky Way.  Includes mean AGN flux.

y_ab               AB          Extincted by internal dust.  Unextincted by
                   magnitudes  Milky Way.  Includes mean AGN flux.

Bulge_to_total     float       Ratio of the bolometric flux from the
                               galaxy's bulge to the total bolometric flux
                               of the galaxy.

Disk_to_total      float       Ratio of the bolometric flux from the
                               galaxy's disk to the total bolometric flux
                               of the galaxy.  Note: Bulge_to_total and
                               Disk_to_total will not sum to unity in the
                               presence of an AGN.

Point_source_SED   str         Some means of identifying the SED of a
                               point source (e.g. an AGN) associated with
                               the galaxy/galaxy component.  The same
                               caveats apply here as applied to the SED
                               column for the whole galaxy/component.

Point_source_norm  magnitudes  Some way to normalize the point source SED.  The
                               same caveats apply here as applied to the
                               normalization of the entire galaxy's SED

Barycentric_RA     degrees     ICRS.  Defined according to the system's center
                               of mass.

Barycentric_Dec    degrees     ICRS.  Defined according to the system's center
                               of mass.
=================  ==========  ==========================================================

#  Define the schema required for input catalogs

Summary -- There currently exists a schema for all components needed by CatSim for generating simulated
observed catalogs as well as inputs to both PhoSim and GalSim. This schema should be reviewed to make sure it
is both compact (i.e. to maximize the orthogonality between different parameters) and sufficient for all
potential simulated catalogs.


## Key Tasks
* Key Task CS2.1.1 ( 12/16 ): Gather the schema currently in use within the project for input
catalogs.
* Key Task CS2.1.2 ( 12/16 ): With knowledge from [CS1.2](github.com/DarkEnergyScienceCollaboration/CS1.2)
distill the current schema into the most compact but
covering schema.
* Key Task CS2.1.3 ( 12/16 ): Document the schema including units and datatypes.

### Suggested organization
Repositories are available per deliverable.  Each key task has a subdirectory.
We have a `source` directory in each key task area for any supporting
code that goes with an effort.  There will also be a `doc` directory to hold documents in markdown,
latex, or binary formats.  The idea is to version everything and give us a good way to diff things.

Each deliverable is slightly different, so these repositories should grow to support the different need.

Please feel free to use github issues on each repository to organize work.

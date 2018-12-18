# cellular-structure-identification
Identifying the type of the multicellular structure based on the connectivity graph of the cells

### Format of the output data

The experiment data is saved in a json file under the same name as the CompuCell3D project for easier identification. The data follows the format:

```python
[{
  "time"  : <MonteCarlo-timestep1>,
  "cells" : {
    "<cell-id1>": {
      "type": <type-cell-id1>,
      "pos" : [<x>, <y>, <z>],
      "neighbors": {
        "<neighbor-id1>": <common-contact-surface1>,
        "<neighbor-id2>": <common-contact-surface2>,
        ...
      }
    },
    "<cell-id2>": {
      "type": <type-cell-id2>,
      "pos" : [<x>, <y>, <z>],
      "neighbors": {
        "<neighbor-id1>": <common-contact-surface1>,
        "<neighbor-id2>": <common-contact-surface2>,
        ...
      }
    },
    ...
  }
},
{
  "time"  : <MonteCarlo-timestep2>,
  "cells" : { ... }
},
...
]
```

The data is a list of dictionaries, one for each saved Monte Carlo step. The dictionary containes two entries, a number - the experiment time, and a dictionary containing the type, position and the neigbors for each cell.

# cellular-structure-identification
Identifying the type of the multicellular structure based on the connectivity graph of the cells

### Format of the output data

The experimental data is saved in a json and following the format:

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

#### Python code to be placed in step
```python
import json

...

# Save simulation data
if mcs % RESOL == 0:
    cells = {}

    # Extract the connectivity graph between cells
    for cell in self.cellList:
        cells[cell.id] = {
            "type": cell.type,
            "pos": [cell.xCOM, cell.yCOM, cell.zCOM],
            "neighbors": {n.id:s for n, s in self.getCellNeighborDataList(cell) if n}
        }

    GLOBAL.append({"time": mcs, "cells": cells})

    # Save partial results in case it crashes later
    try:
        f, _ = self.openFileInSimulationOutputDirectory("results.json", "w")
        json.dump(f, GLOBAL)
        f.close()
    except:
        print("Could not write the results file")
```

Notes on how to use json and python to code a minimal rules engine for 3D chess.

  ```
  {
    "coords": {
      "board_to_vts_offset": [10, 10, 10]
    },

    "rays": {
      "rook": [[1,0,0], [-1,0,0], [0,1,0], [0,-1,0], [0,0,1], [0,0,-1]],
      "bishop": [[1,1,0], [1,-1,0], ...],
      "duke": [[1,1,1], [1,1,-1], ...]
    },

    "planes": {
      "rook": {
        "XY": { "rays": ["+X","+Y","-X","-Y"], "quadrants": ... },
        "XZ": ...
      },
      "bishop": { ... },
      "duke": { ... }
    },

    "tile_classes": {
      "brook": ["rook", "bishop"],
      "feynman": ["bishop", "duke"],
      "hotspot": ["rook", "duke"],
      "q_tile": ["rook","bishop","duke"]
    },

    "colors": {
      "bishop_color": "parity(x+y+z)",
      "duke_color": "parity(x,y,z mod 2 pattern)"
    }
  }
```

Local script:
  ```
  import json

  with open("data/spec.json") as f:
      SPEC = json.load(f)
  ...
```

Structured results:
  ```
  {
    "attacks": True,
    "planes": ["duke_slant_3"],
    "blocker_effect": "blocks_at_shell_1",
    "quark": False
  }
  ```

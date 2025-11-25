# Quads Module

This module defines all canonical plane cycles, quadrant construction rules, 
ray–plane membership, and duke quad-type classification.  
It is the authoritative basis for quads.json and quads.py.

-------------------------------------------------------------------------------
## 1. Canonical Plane Rule

Each plane is defined solely by its canonical cyclic list of rays.
The following constraints apply:

- Ray adjacency exists **only** within the listed cycle.
- Quadrants are defined **only** by adjacent ray pairs (ray[i], ray[i+1]).
- No rotation, reversal, or permutation of any cycle is permitted.
- All quad and movement logic must reference these exact cycles.
- Planes are text-distinct; cube symmetry does not equate planes.

For each plane:
- Quad1 is formed by (ray1, ray2).
- wrapQuad is formed by (ray-last, ray1).

Ray membership:
- Each rook ray occurs in exactly 2 planes.
- Each bishop ray occurs in exactly 2 planes.
- Each duke ray occurs in exactly 3 planes.

-------------------------------------------------------------------------------
## 2. The Plane Quad Table

### 2.1 Rook Planes (orthogonal)
Horizontal:  left_fore > right_fore > left_back  > right_back >
Left:        up        > right_fore > down       > right_back >
Right:       up        > left_fore  > down       > left_back  >

### 2.2 Bishop Planes (skew)
Upward:     LFU > RFU > right > RBD > LBD > left >
Downward:   LFD > RFD > right > RBU > LBU > left >
Leftward:   LBU > LFU > fore  > RFD > RBD > back >
Rightward:  RBU > RFU > fore  > LFD > LBD > back >

### 2.3 Duke Planes (slant)
Major:      fore_down > fore_up   > back_up    > back_down >
Minor:      left_up   > right_up  > right_down > left_down >
Upleft:     left_up   > fore_up   > right_down > back_down >
Downleft:   left_down > fore_down > right_up   > back_up   >
Upright:    right_up  > fore_up   > left_down  > back_down >
Downright:  right_down> fore_down > left_up    > back_up   >

-------------------------------------------------------------------------------
## 3. Ray Index (Ray → Planes)

Each ray belongs only to the planes listed below.

(Exactly identical to the JSON "rayIndex" table; kept authoritative here.)

- left_fore:  Horizontal, Right
- right_fore: Horizontal, Left
- left_back:  Horizontal, Right
- right_back: Horizontal, Left

- up:   Left, Right
- down: Left, Right

- LFU: Upward, Leftward
- RFU: Upward, Rightward
- LFD: Downward, Rightward
- RFD: Downward, Leftward

- LBU: Downward, Leftward
- LBD: Upward, Rightward
- RBU: Upward, Downward
- RBD: Downward, Upward

- fore:  Leftward, Rightward
- right: Upward, Downward
- back:  Leftward, Rightward
- left:  Upward, Downward

- fore_down: Major, Downleft, Downright
- fore_up:   Major, Upleft, Upright
- back_up:   Major, Downleft, Downright
- back_down: Major, Upleft, Upright

- left_up:    Minor, Upleft, Downright
- right_up:   Minor, Upright, Downleft
- right_down: Minor, Upleft, Downright
- left_down:  Minor, Downleft, Upright

-------------------------------------------------------------------------------
## 4. Duke Quad Types

Duke quadrants come in two flavors: **edge** and **face**.

### 4.1 Delta Classification Rule
Given adjacent vertex-ray vectors (dz1,dx1,dy1) and (dz2,dx2,dy2):

Let:
    Δ = (dz2−dz1, dx2−dx1, dy2−dy1)

Classification:
- If Δ has **two zeros**: quad is **face**
- If Δ has **one zero**: quad is **edge**

No other case occurs.

This rule is the authoritative method for determining quad flavor.

### 4.2 Alternation Pattern
In every duke plane, the quad sequence alternates edge/face cyclically.

Patterns:

- Major:     edge, face, edge, face
- Minor:     face, edge, face, edge
- Upleft:    edge, face, edge, face
- Downleft:  edge, face, edge, face
- Upright:   edge, face, edge, face
- Downright: edge, face, edge, face

Because each cycle is closed, alternation wraps naturally.

-------------------------------------------------------------------------------
## 5. Summary

This module defines:

- all 13 canonical planes
- all canonical ray cycles
- the construction of quadrants via adjacent ray pairs
- ray → plane membership (rayIndex)
- the duke quad-type delta rule
- the duke plane alternation patterns

These specifications together fully determine quads.json and quads.py.

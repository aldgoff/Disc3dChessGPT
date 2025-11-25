# Plane Quad Module

  Canonical Plane Rule
   - Each plane is uniquely defined by its canonical cyclic ray list.
   - Ray adjacency exists only within this cycle.
   - Quadants (quads) are defined only by adjacent pairs in this cycle.
   - No rotation or reversal of the cycle is permitted.
   - Any alternative ordering, rotation, reversal, or ray-pair mapping is invalid.
   - All plane, quad, and movement logic MUST reference the canonical Plane Quad Table.

## 1. The Plane Quad Table
  Plane, Ray Set (1st to last)

    Rook Planes (Orthogonal)
      Horizontal  left_fore > right_fore > left_back  > right_back >
      Left        up        > right_fore > down       > right_back >
      Right       up        > left_fore  > down       > left_back  >
      Each rook ray must occur in two and only two planes

    Bishop Planes (Skew)
      Upward      LFU   > RFU   > right > RBD   > LBD   > left  >
      Downward    LFD   > RFD   > right > RBU   > LBU   > left  >
      Leftward    LBU   > LFU   > fore  > RFD   > RBD   > back  >
      Rightward   RBU   > RFU   > fore  > LFD   > LBD   > back  >
      Each bishop ray must occur in two and only two planes

    Duke Planes (Slant)
      Each duke-plane is defined ONLY by the following ray set
        Major       fore_down  > fore_up   > back_up    > back_down >
        Minor       left_up    > right_up  > right_down > left_down >
        Upleft      left_up    > fore_up   > right_down > back_down >
        Downleft    left_down  > fore_down > right_up   > back_up   >
        Upright     right_up   > fore_up   > left_down  > back_down >
        Downright   right_down > fore_down > left_up    > back_up   >
        Each duke ray must occur in three and only three planes
      Duke-plane adjacency is defined only by the listed cycles.
      No coordinate pattern or geometric relation may add or modify adjacency.

  Constraints:

    No other grouping or adjacency pattern is valid.
    No ray may belong to more than the listed planes.

    Planes are distinct by text only.
    No symmetry or rotation of the cube may identify two plane-cycles.
    Only the listed cycles define plane identity.

    These cycles are the canonical order; none other exists.

  Summary: 
   - For all 13 planes, the first quad is always the quadrant formed by the first two rays listed,
   - the wrapQuad is the last one listed.

## 2. The Plane Groups
    Vertical planes (rook)
      Left
      Right
    Forward planes (bishop)
      Upward
      Downward
    Outward planes (bishop)
      Leftward
      Rightward
    Verticalcross planes (duke)
      Major
      Minor
    Leftcross planes (duke)
      Upleft
      Downleft
    Rightcross planes (duke)
      Upright
      Downright

## 3. Duke Quad Types
  - Duke quads come in two flavors, edge and face, which alternate.
  - Quad flavor is computed from ray deltas.

  ### 3.1 Formula for Quad Type:
    Given adjacent vertex rays with components (dz1,dx1,dy1) and (dz2,dx2,dy2):
      Let Δ = (dz2-dz1, dx2-dx1, dy2-dy1).
      Count zeros in Δ:
      2 zeros → face-quad
      1 zero  → edge-quad
    No other case occurs.

  ### 3.2 Alternating Quad Type Summary:
    Plane    firstQuad            wrapQuad
    Major:     edge - face - edge - face
    Minor:     face - edge - face - edge
    Upleft:    edge - face - edge - face
    Downleft:  edge - face - edge - face
    Upright:   edge - face - edge - face
    Downright: edge - face - edge - face
    
  - Because the quad sequence is cyclic, each slant plane alternates edge and face quadrants.
  - In all slant planes except the Minor plane, quad1 is an edge quad and quad2 is a face quad.
  - In the Minor plane, quad1 is a face quad and quad2 is an edge quad.

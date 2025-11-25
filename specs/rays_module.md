# Rays Module
  Rays are unit-offset directions in VTS space
  Each ray is a triple (dz,dx,dy) with components in {−1,0,1} excluding (0,0,0)
  These ray lists define names and coordinates only.
  They do not specify ordering, adjacency, or plane membership.
  All plane structure is defined only in the planeQuad module.

  Rook rays (6 face-adjacent)
    up          ( 1, 0, 0)
    down        (−1, 0, 0)
    left_fore   ( 0, 1, 0)
    left_back   ( 0,−1, 0)
    right_fore  ( 0, 0, 1)
    right_back  ( 0, 0,−1)

  Bishop rays (12 edge-adjacent)
    fore   ( 0,  1,  1)
    right  ( 0, -1,  1)
    back   ( 0, -1, -1)
    left   ( 0,  1, -1)
    LFU    ( 1,  1,  0)
    LFD    (-1,  1,  0)
    LBU    ( 1, -1,  0)
    LBD    (-1, -1,  0)
    RFU    ( 1,  0,  1)
    RFD    (-1,  0,  1)
    RBU    ( 1,  0, -1)
    RBD    (-1,  0, -1)

  Duke rays (8 vertex-adjacent)
    fore_up     ( 1,  1,  1)
    fore_down   (-1,  1,  1)
    right_up    ( 1, -1,  1)
    right_down  (-1, -1,  1)
    back_up     ( 1, -1, -1)
    back_down   (-1, -1, -1)
    left_up     ( 1,  1, -1)
    left_down   (-1,  1, -1)

  Scope
    Defines the 26 rays and their rook, bishop, and duke classifications
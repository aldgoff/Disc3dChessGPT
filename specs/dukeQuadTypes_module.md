# Duke Quad types
  Duke quads come in two flavors, edge and face, which alternate.
  Quad flavor is computed from ray deltas.
  Given adjacent vertex rays with components (dz1,dx1,dy1) and (dz2,dx2,dy2):
    Let Δ = (dz2-dz1, dx2-dx1, dy2-dy1).
    Count zeros in Δ:
      2 zeros → face-quad
      1 zero  → edge-quad
  No other case occurs.

  Duke alternating quad type summary:
    Plane    firstQuad            wrapQuad
    Major:     edge - face - edge - face
    Minor:     face - edge - face - edge
    Upleft:    edge - face - edge - face
    Downleft:  edge - face - edge - face
    Upright:   edge - face - edge - face
    Downright: edge - face - edge - face
    
    Because the quad sequence is cyclic, each slant plane alternates edge and face quadrants.
      In all slant planes except the Minor plane, quad1 is an edge quad and quad2 is a face quad.
      In the Minor plane, quad1 is a face quad and quad2 is an edge quad.

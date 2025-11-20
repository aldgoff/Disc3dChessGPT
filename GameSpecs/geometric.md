# Geometry Specification

**Version:** 0.2
**Status:** In-work
**Purpose:** Definitions of 2D and 3D rays, planes, quadrants, perimeters, advancement squares & rectangles.

## Sections

1. Rays (2D + 3D)
2. Plane Names
3. Quadrants
4. Plane Specifications.
5. Advancement Squares
6. Advancement Rectangles

---

# 1. Rays
  Rays define all primitive geometric directions used by Q3DC. 
  These are expressed in **absolute VTS coordinates** (aligned with White POV). 
  Black POV directions are derived later via 180° rotation around the z-axis.

  Each ray is a vector consisting of:

  * **2D:** (dx, dy)
  * **3D:** (dx, dy, dz)
  with each component ∈ {−1, 0, +1}, excluding the zero vector.

  Rays are used to specify the legal moves of the base pieces.

  ## 1.1 2D Rays (Planar)
    These rays describe all 8 adjacency directions in a square lattice.
    2D rays define directions along ranks (y) and files (x).

    ### 1.1.1 2D Rook Rays (orthogonal: side-adjacent squares)

    2D rook:
      forward:     0, +1
      backward:    0, -1
      right:      +1,  0
      left:       -1,  0

    ### 1.1.2 2D Bishop Rays (diagonal: corner-adjacent squares)

    2D bishop:
      right_forward:   +1, +1
      right_backward:  +1, -1
      left_backward:   -1, -1
      left_forward:    -1, +1

  ## 1.2 3D Rays (Spatial)

    These rays describe all 26 adjacency directions in a cubic lattice.
    3D rays define directions along orthogonal, skew & slant planes.
    Coords (x,y,z).

    ### 1.2.1 3D Rook Rays (orthogonal: face-adjacent cubes)

      Name      Coords (x,y,z)

      left_fore   +1,  0,  0
      left_back   -1,  0,  0
      right_fore   0, +1,  0
      right_back   0, -1,  0
      up           0,  0, +1
      down         0,  0, -1

    ### 1.2.2 3D Bishop Rays (edge-adjacent)

      Name           Coords (x,y,z)  Shorthand

      fore             +1, +1,  0
      right            -1, +1,  0
      back             -1, -1,  0
      left             +1, -1,  0

      left_fore_up:    +1,  0, +1    LFU
      left_fore_down:  +1,  0, -1    LFD
      left_back_up:    -1,  0, +1    LBU
      left_back_down:  -1,  0, -1    LBD

      right_fore_up:    0, +1, +1    RFU
      right_fore_down:  0, +1, -1    RFD
      right_back_up:    0, -1, +1    RBU
      right_back_down:  0, -1, -1    RBD

    ### 1.2.3 3D Duke Rays (vertex-adjacent)

      Name      Coords (x,y,z)

      fore_up:     +1, +1, +1
      fore_down:   +1, +1, -1
      right_up:    -1, +1, +1
      right_down:  -1, +1, -1
 
      back_up:     -1, -1, +1
      back_down:   -1, -1, -1
      left_up:     +1, -1, +1
      left_down:   +1, -1, -1

# 2. Plane Types
  Planes are categorized by the type of base piece which moves in that plane.
    - Three types of base pieces => three categories of planes.
    - Within each category, there are different orientations of planes, each orientation is given a globally unique name.
      - These are the 'plane types'.
  The bishop and duke planes have also been sub-grouped by pairs, as have the rook vertical planes.

  ## 2.1 Major piece planes planes
    Rook (Orthogonal)
      Horizontal
      Vertical
        Left
        Right
    Bishop (Skew) Each bishop plane has the same bishop color (white, black)
      Forward
        Upward
        Downward
      Outward
        Leftward
        Rightward
    Duke (Slant) Each duke plane has the same duke color (gold, silver, ruby, jade)
      Vertical Cross Planes (Line of intersection connects top and bottom faces)
        Major (Connects the players)
          Primary Major Plane (Largest major plane, starting lineup, pawn promotion, gold & silver tiles only)
        Minor (Separates the players)
      Left Cross Planes (Line of intersection connects left faces)
        Upleft (Leans toward opponent)
        Downleft (Leans toward self)
      Right Cross Planes (Line of intersection connects right faces)
        Upright (Leans toward opponent)
        Downright (Leans toward self)

  ## 2.2 Special duke planes
    Vertical planes (both major and minor) can be of two types:
      metal planes: gold/silver
      gem planes: ruby/jade
    The primary plane is the (1,1) - (8,8) major plane.
      It contains the starting lineup, the pawn promotion tiles, and is a metal plane. 

# 3. Quadrants (quad(s) for short)

  ## 3.1 Rays and quads
    When used to construct a plane, rays and quads group into correlated cyclically ordered lists.
    A quad is defined by an ordered **pair** of rays.
      The rays must be of the **same type** (rook/face/orthogonal, biship/edge/skew, duke/vertice/slant).
      They must be **adjacent** (this is how they become cyclic).
        Because the ray list is cyclic, each ray appears in exactly two adjacent quadrants: one with its predecessor and one with its successor in the cyclic order.
      The first ray must be **prior** to the second.
    Given a cyclic list of four rays (ray1, ray2, ray3, ray4) the cyclic order of the four quads is:
      quad1 (ray1,ray2)
      quad2 (ray2,ray3)
      quad3 (ray3,ray4)
      quad4 (ray4,ray1)
    Given a cyclic list of six rays (ray1, ray2, ray3, ray4, ray5, ray6) the cyclic order of the six quads is:
      quad1 (ray1,ray2)
      quad2 (ray2,ray3)
      quad3 (ray3,ray4)
      quad4 (ray4,ray5)
      quad5 (ray5,ray6)
      quad6 (ray6,ray1)
  
    ### 3.1.1 Circular Ambiguity
      A plane is defined by a cyclic ordered list of **adjacent** quads.
      A cyclic ordered list of quads is defined by a cyclic ordered list of **adjacent** rays.
      Traversal order of these cyclic lists, and the choice of starting ray/quad, are established by convention (below).
      The number of quadrants is plane dependent 
        4 for rook planes
        6 for bishop planes
        4 for duke planes
  
    ### 3.1.2 Resolving Circular Ambiguity
      There are two; traversal direction and starting point.
      **Traversal direction** is either clockwise (CW) or counterclockwise (CCW) from some canonical perspective.
        **Perspective** This requires establishing standard perspective:
          **Top**: view looking down through the top face of the board.
          **KR**: view looking through White's upper corner (where the king rook starts).
          **Neutral**: view looking into the board from the vertical edge between the players.
            Black on left, White on right.
          Each perspective presents a subset of planes **face-on**.
        **Traversal direction** (both ray & quad) is clockwise (CW) or counterclockwise (CCW), specified for each plane.
      **Starting Point**
        If a quad has two rays where both x and y increase, then it has a quad that advances toward the opponent.
        If not, it will have a quad where z increases and either x or y (but not both)
        The quad that most points toward the opponent.
          Or the quad that most points upward (toward top of board)

        For outward bishop planes (leftward and rightward), quad1 is the quadrant whose ray pair has the greatest positive-z (upward) contribution.  
          If multiple quadrants are equally upward, choose among them the one whose rays have the greatest forward (positive-y) projection when viewed in the horizontal plane.  
          The traversal direction (CW or CCW) is then chosen so that rotation from quad1 proceeds toward the opponent in this horizontal projection.  
          This yields a consistent forward-facing arc of adjacent quadrants immediately following quad1.
        For slant (duke) planes:
          Quad1 is the quadrant whose ray-pair has the strongest combined forward and upward projection in the slant’s defining axis components.
          This selects the edge-quadrant in every slant plane.

        Traversal direction is then either (this is actually bishop only, isn't it.)
          **towards opponent** for quadrants which approach the top of the board.
          **downward** for quadrants which approach the opponent.
        The first pair of rays listed in the cyclic list define the first quadrant and the traversal order.
        The second pair of rays define the 2nd quadrant, etc.

  ## 3.2 Black's POV
    - Since a player can be either White or Black, their mental map of the board (planes, rays, quadrants, etc.), should NOT have to change.
    - Only White’s specification is canonical; Black’s is derivative.
    - Black’s ray/quad ordering is not separately defined; it is obtained from White’s by applying the standard 180° rotation about the z-axis.
    - For many planes, Black's first quad will differ from White's, for others it will be the same.
    - For many planes, Black's traversal order will be the same as White's, for others it will be different.

  ## 3.3 Quadrant Count Summary:
    - 12 rook quadrants
    - 24 bishop quadrants
    - 24 duke quadrants

  ## 3.4 Quadrant Reference (a bit redundant, but each has a purpose):
    - Rook quadrants:   1 through 4 for each plane (3), 1 through 12 for orthogonal planes, 1 through 12 for all planes.
    - Bishop quadrants: 1 through 6 for each plane (4), 1 through 24 for skew planes,      13 through 36 for all planes.
    - Duke quadrants:   1 through 4 for each plane (6), 1 through 24 for slant planes,     37 through 60 for all planes.

  ## 3.5 Meta Narrative by Base Piece
    - Striking a better balance between geometry and human intuition.

  ## 3.6 Plane, Ray, Quadrant Spec table
    Plane      Perspective  Rotate  Ray Set (1st to last)                   Quad Numbers -> Plane  Local  Global  Quad Nicknames
    - Horizontal   KR       CW           left_fore > right_fore > right_back > left_back  >  1-4    1-4    1-4    Forward.Right.Backward.Left
    - Left         Neutral  CW           up        > right_fore > down       > right_back >  1-4    5-8    5-8    Q5.Q6.Q7.Q8 
    - Right        Neutral  CCW          up        > left_fore  > down       > left_back  >  1-4    9-12   9-12   Q9.Q10.Q11.Q12
      - (double check: each ray used twice)
    - Upward       Top      CW           LFU   > RFU   > right > RBD   > LBD   > left  >     1-6    1-6   13-18   UpPredator.Q14.Q15.DN.Q17.Q18
    - Downward     Top      CW           LFD   > RFD   > right > RBU   > LBU   > left  >     1-6    7-12  19-24   DnPredator.Q20.Q21.UP.Q23.Q24
    - Leftward     Top      CW           LBU   > LFU   > fore  > RFD   > RBD   > back  >     1-6   13-18  25-30   Q25.LUpSling.LDnSling.Q27.Q28.Q29
    - Rightward    Top      CCW          RBU   > RFU   > fore  > LFD   > LBD   > back  >     1-6   19-24  31-36   Q31.RUpSling.RDnSling.Q34.Q35.Q36
      - (double check: each ray used twice: √LFU √RFU √RBD √LBD √RBU √LBU √LFD √RFD )
    - Major        Neutral  CW  (up)     fore_down  > for_up    > back_up    > back_down >   1-4    1-4   37-40   Fore.Up.Aft.Down
    - Minor        KR       CW  (right)  left_up    > right_up  > right_down > left_down >   1-4    5-8   41-44   Top.Starboard.Bottom.Port
    - Upleft       Top      CW  (down)   left_up    > fore_up   > right_down > back_down >   1-4    9-12  45-48   Q45.Q46.Q57.Q48
    - Downleft     Top      CW  (up)     left_down  > fore_down > right_up   > back_up   >   1-4   13-16  49-52   Q49.Q50.Q51.Q52
    - Upright      Top      CCW (down)   right_up   > fore_up   > left_down  > back_down >   1-4   17-20  53-56   Q53.Q54.Q55.Q56
    - Downright    Top      CCW (up)     right_down > fore_down > left_up    > back_up   >   1-4   21-24  57-60   Q57.Q58.Q59.Q60
      - (double check: each ray used thrice)

    Summary: For all 13 planes, quad1 is always the quadrant formed by the first two rays listed in that row of the table.
    Note: duke quads come in two flavors, edge quads and face quads, which alternate.
      Plane    firstQuad            lastQuad
      Major:     edge - face - edge - face
      Minor:     face - edge - face - edge
      Upleft:    edge - face - edge - face
      Downleft:  edge - face - edge - face
      Upright:   edge - face - edge - face
      Downright: edge - face - edge - face
      In all planes except the minor, the first quard is an edge quad, the last one a face quad.
    Note: some quads get nicknames, 4 rook quads, 6 bishop quads, 8 duke quads; the rest are referrenced by their global numbers (Qnn).

# 4. Plane Specification

*(To be developed in terms of rays or quadrants.)*

---

# 5. Advancement Squares

*(To be developed.)*

---

# 6. Advancement Rectangles

*(To be developed.)*


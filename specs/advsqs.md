# Advancement Squares Spec
  - In 2D, a piece advances by stepping to the next **tile** along a **line**, in one of 2 directions. 
  - In 3D, a piece advances by stepping to the next **perimeter** along a **quadrant**, in one of 4 or 6 directions. 
  - In 3D, **lines are replaced by planes**, and the linear directions along a line are replaced by **quadrants**. 
  
  - The advancement square generalizes the notions of forward direction and distance.
    - In 2D, 'perimeters' are frontiers of 1 tile.
    - In 3D, 'perimeters' are frontiers of 2k+1 tiles (an 'L' shape).

  - Advancement squares are how blocking is defined in 3D chess.

## 1. Definition
  An advancement square is the ordered set of successive perimeters (0-k)

  - defined within **one quadrant** of **one plane**
  - grows outward using **perimeters**, not ray steps
  - encodes both **direction** (quadrant) and **distance** (perimeter index)

  Let S be a source tile, Q a valid quadrant, and k ≥ 0 (k ∈ ℕ)

    The NxN‑advancement square, written A(S,Q,N), is the union of all tiles enclosed by the nested perimeters:
      P(0) = {S}
      P(1)
      P(2)
      …
      P(k=(N-1))
    A(S,Q,N) is defined even if part of it falls off board.

  Each perimeter P(i) is computed from the ray‑pair defining quadrant Q using the perimeter algorithm.

    The resulting region is always a (k+1)×(k+1) square:
      k = 0 → 1×1 square
      k = 1 → 2×2 square
      k = 2 → 3×3 square
      …
      The shape is square in VTS space even when clipped by on-board boundaries.

  Perimeter P(k) is the **active frontier** of the advancement square.

    For (i < k) P(i) is included in A(S,Q,N), but only P(k) is the active frontier; earlier perimeters are interior layers.
    Advancement is to any tile on the perimeter only, but blocking can occur an any tile in the advancement square.

## 2. Structural Invariants
  ### 2.1 Forward Geometry
    The ordered ray pair (r1,r2) of quadrant Q defines the square’s orientation.
    No rotation, reversal, or POV‑adjustment is permitted.

  ### 2.2 Nested Squares
    P(0), P(1), …, P(k) form perfectly nested layers. Each P(i) has 2i+1 tiles.

  ### 2.3 Shape
    Only two edges of the (k+1)×(k+1) square appear in P(i). 
    The other two sides are interior.

  ### 2.4 On‑Board / Off‑Board
    Advancement squares may be fully on‑board, fully off‑board, or mixed, and tile formatting follows coords spec.

  ### 2.5 Termination
    The advancement square terminates at the last perimeter with any tiles on board.

## 3. Data Structure (a json object)
    Canonical:
      Perimeter list:
        P(0)…P(k)
      Quad - Quadrant numbers [Qn, BpQn, PQn, nickname (none)]

    Derivative:
      Source tile - P(0)
      Plane
      Direction:
        Ray pair:
          Name pair
          Coord pair
      Distance:
        k
      Size:
        as NxN (k+1)*(k+1)
        product, area = N x N.
      Real-Virtual:
        On board count
        Off board count

## 3. Construction Algorithm - A(S, Q, k)
    Inputs:
      Tile S (board <LL>X,Y or VTS (z,x,y))
      Quadrant Q (global Q‑number, base piece Qn, plane Qn, nickname, or explicit adjacent ray‑pair)
      Distance k ≥ 0 (optional)
        If k is absent, compute until a perimeter is fully off-board.

    Outputs:
      A - the advSq defined by the input parameters

    Steps:
      1. Identify plane and quadrant.
      2. Compute successive perimeters P(0)…P(k).
          Format tiles (<LL>X,Y if on‑board, VTS if off‑board).
          Throw an error if any perimeter tile is outside the VTS coords.
      4. Assemble the advSq object with all the derived values.

  The full set of nested perimeters defines the entire advancement square.

    Source tile, quadrant, distance, size, and on/off board stats are all derivative.

## 4. Relation to Piece Advancement
    In a quadrant move, a piece advances into the advancement square.
    The move is legal iff the advancement square is empty.
    Except for capture, a move is blocked by any occupied tile in the advancement square.

## 5. Functions
  ### 5.1 Parameter Defs
    S - source tile (must be on board)
    Q - a Quad object
      Contains all the ways of specifying a quadrant 
        (global, base-piece, plane, nickname, or adjacently ordered ray pair)
    k - integral distance, the 'kth' perimeter
    A - an AdvSq json object.

  ### 5.2 Function Defs
    AdvSq(S,Q)
      Computes perimeters until all tiles off board.
      returns an AdvSq json object.

    AdvSq(S,Q, k)
      Computes k perimeters regardless of on/off board tile status.
      returns an AdvSq json object.

    frontier(A,k)
      Returns ordered tile list for perimeter P(k).
        Format: <LL>X,Y for on-board; (z,x,y) for off-board.
        Null if A was too small to have a kth perimeter.

    on_off_board_tiles(A, k)
      Returns: integer pair
        1. on-board tiles
        2. off-board tiles

    advsq_size(A)
      Returns: N = k+1, the side length of the advancement square.

    quad_name(A)
      Returns: the canonical global quadrant number of the advancement square.

    color_tiles(A)
      rook:   mixed
      bishop: constant bishop color
      duke:   constant duke color

    tile_type_counts(A, k)
      triplet of (endTiles, apexTiles, betweenTiles)
      By perimeter if k present, for the whole advancement square if not.

  ### 5.3 Error Handling
    If syntax, tile, quadrant, ray-pair, distance, or advancement square invalid:
     [ ERROR:<reason> ]
    One line per failed item, no extra text.

## 6. Examples

  ### 6.1 Construct
    All on Board:
      AdvSq("KR2,2", Q1, 4)
      print perimeter list
      print plane, quad, NxN, and on/off board tile stats
        
    Some on Board:
      AdvSq("KR2,2", Q2, 4)
      print perimeter list
      print plane, quad, NxN, and on/off board tile stats
        
    None on Board:
      AdvSq("KR1,1", Q3, 4)
      print perimeter list
      print plane, quad, NxN, and on/off board tile stats
        
    Without Limit:
      AdvSq("KR1,1", Q4)
      print perimeter list
      print plane, quad, NxN, and on/off board tile stats

  ### 6.2 Details
    Last perimeter:
      print frontier(A, A.advsq_size(A)-1)

    Given a rook advancment square Ar
      print color_tiles(Ab)

    Given a bishop advancment square Ab
      print color_tiles(Ab)

    Given a duke advancment square Ad
      print color_tiles(Ab)

  Scope:
  - Definition and purpose.
  - Define an AdvSq class.
  - Clean object interface to construct advancement squares.
  - Explicit construction instructions, options, and error handling.
  - Functions to access derived values.
  - Examples

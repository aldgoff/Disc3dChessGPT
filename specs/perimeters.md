# Perimeters Spec

  Perimeters:
  - How direction and distance are defined in 3D chess.

## 1. Definition
    An advancement perimeter is the growing frontier of an expanding square defined by a quadrant’s ray-pair.
    Unlike the full perimeter of a square (which traces all four sides), an advancement perimeter traces only 
    the two active sides that extend outward along the quadrant’s two rays.
    It is a 'frontier' rather than a 'boundary.'
    The frontier always expands only inside its quadrant and never forms a loop.

    This design prevents expansion into other quadrants and avoids repeated coverage of pre-existing boundary tiles.

## 2. Distance
    The implicit 1×1 advancement square (the source tile) has perimeter 0 and consists only of the origin tile.
    Perimeter 1 P(1) is the first true frontier and consists of 3 tiles; this corresponds to the 2×2 advancement square.
    A k×k advancement square is represented by the ordered list of perimeters P0, P1, …, P(k).
    A perimeter P(k) contains 2k + 1 tiles.
    
    The value of k is the measure of the distance, the 3D analog of how far down a 2D line.

## 3. Representation
    A perimeter is represented as a series of tiles, expressed in the appropriate coordinate system.
      Off-board tiles SHALL be written in VTS triple format using parentheses and commas: (z,x,y). 
      On-board tiles SHALL remain in board format <LL>X,Y.

    Perimeters which cross the board boundary will use both formats.
      The <LL>X,Y notation guarantees unambiguous grouping of Board triplets.
      Parentheses guarantee unambiguous grouping of VTS triplets.

## 4. Formatting Contract
    Tile Formatting Pipeline (MUST-FOLLOW):

    Given a computed VTS tile (z,x,y):

    Step 1. Convert VTS → Board coordinates
      Z = z − (Az − 1)
      X = x − (Ax − 1)
      Y = y − (Ay − 1)

    Step 2. Board-membership test
      A tile is on-board iff:
        1 ≤ Z ≤ 8
        1 ≤ X ≤ 8
        1 ≤ Y ≤ 8
      (If any component fails, the tile is off-board.)

    Step 3. Choose output format
      If on-board, output board format:
        <LL>X,Y where <LL> is the Level Label for Z
      If off-board, output VTS triple format:
        (z,x,y)

    Mandatory rule:
      Steps 1–2 must be performed before choosing a format.
      On-board tiles MUST appear in <LL>X,Y form.
      A tile is on-board if and only if its Board-coordinates satisfy 1–8 after VTS→Board conversion.
      Failure to do so is specification non-compliance.

## 5 Computing Perimeters

  ### 5.1 Input Parameters
    The perimeter algorithm requires three parameters and returns an ordered list of tiles:
    • The source (origin) tile - S
    • A pair of rays           - (r1,r2) in adjacency order.
    • The perimeter number     - k ≥ 1

  ### 5.2 Tile Labels
    Define special tile labels:
      First end tile: E1 = S + k·r1
      Apex tile A = S + k·r1 + k·r2
      Second end tile: E2 = S + k·r2
      All the rest are "between" tiles
    Symbolically, [ E1, Bi++, A, Bj++, E2], puts end tiles first and last, apex in the middle.

  ### 5.3 Tile Sequence
    The k-th perimeter P(k) is constructed as a sequence of 2k + 1 tiles in this order:
      1. First end tile:
          E1 = S + k·r1
      2. Forward segment along +r2 (between tiles):
          Bn++ = E1 + n·r2, for n = 1 to k−1
      3. Apex tile:
          A = S + k·r1 + k·r2
      4. Return segment along −r1 (between tiles):
          Bn++ = A − n·r1, for n = 1 to k−1
      5. Second end tile:
          E2 = S + k·r2

  ### 5.4 Enforce Wrap of Ray Pairs
    (rWrap, r1) is NOT the same as (r1, rWrap).
    Perimeter tiles MUST always be listed in the canonical order:
      E1 (S + k·r1), then stepping by +r2 to Apex, then stepping by −r1 to E2.
      This ordering is mandatory and MUST NOT be reversed, mirrored, or reordered based on board membership or symmetry.

  ### 5.5 Invariant
    The resulting list 
      begins at the first frontier corner (E1)
      ascends up one edge to the (apex)
      returns down the other edge ending at the second frontier corner (E2) 
    Producing the required odd-length frontier inside the quadrant.

## 6. Examples

  ### 6.1 Example 1 - Small Perimeter All Tiles on Board
    Source tile S = KR2,2
    ray1 = left_fore
    ray2 = right_fore
    k = 3

    Produces a P3:
      [ KR5,2, KR5,3, KR5,4, KR5,5, KR4,5, KR3,5, KR2,5 ]
      [ E1,    B2,    B3,    Apex,  B5,    B6,    E2 ]
      Exactly 7 tiles,
        end tiles first and last,
        apex in the center,
        potentially two 'between' tile sequences
      symmetric.

    Interpretation:
      A growing advancement square
        in the forward quadrant (Q1, nickname Forward)
        of a horizontal (rook) plane (first orthogonal plane)
        slice: top most level of the board
      approaching the opponent
      now out to perimeter 3
      implying a 4x4 advancement square

  ### 6.2 Example 2 - Larger Perimeter with Tiles both On and Off Board
    Source tile S = K2,2
    ray1 = right_fore
    ray2 = left_back
    k = 4

    Produces a P4:
      [ K2,6  K1,6, (15,9,16), (15,8,16), (15,7,16), (15,7,5), (15,7,14), (15,7,13), (15,7,12) ]
      [ E1,   B2,   B3,        B4,        Apex,      B6,       B7,        B8,        E2 ]
      Exactly 9 tiles.

    Interpretation:
      A growing advancement square
        in the right quadrant (Q2, nickname Forward)
        of a horizontal (rook) plane (first orthogonal plane)
        slice: king level of the board
      advancing to the right between the players.
      now out to perimeter 4
      implying a 5x5 advancement square largly off the board.

## 7. Sanity Check.
    Creating all perimeters for fixed k in quad order runs all the way around the source tile.

  Scope:
  - The measure of distance in 3D chess
  - Computation formula
  - Input parameters
  - 2k+1 series of tiles in appropriate coordinate systems
  - Invariant order of tiles and coordinate representation make interpretation trivial
  - Can extend off the board

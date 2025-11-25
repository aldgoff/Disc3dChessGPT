# Plane Quad Module
  Canonical Plane Rule
    Each plane is uniquely defined by its canonical cyclic ray list.
    Ray adjacency exists only within this cycle.
    Quadants (quads) are defined only by adjacent pairs in this cycle.
    No rotation or reversal of the cycle is permitted.
    Any alternative ordering, rotation, reversal, or ray-pair mapping is invalid.
    All plane, quad, and movement logic MUST reference the canonical Plane Quad Table.

  ## The Plane Quad Table
    Plane       Ray Set (1st to last)

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

    No other grouping or adjacency pattern is valid
    No ray may belong to more than the listed planes

    Planes are distinct by text only.
    No symmetry or rotation of the cube may identify two plane-cycles.
    Only the listed cycles define plane identity.

    These cycles are the canonical order; none other exists

    Summary: For all 13 planes, the first quad is always the quadrant formed by the first two rays listed, the wrapQuad is the last one listed.

  ## The Plane Groups
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

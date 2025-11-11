# Tactical Analysis

## Grid and Point of View (POV)

Grid and Point of View (POV)

To perform accurate Tactical Analysis, all interactions must be referenced within a consistent 3D grid system and Point of View (POV).
This ensures that each movement, attack, or tactical relation is geometrically grounded.


1. Grid System

Each board coordinate is expressed as a triplet:

(level, x, y)


level — one of the eight stacked boards, named after the home piece that begins on that level (from the top downward):

KR, KN, KB, K, Q, QB, QN, QR


KR is the uppermost board, QR the lowest.

x and y — integers from 1 to 8, describing tile displacement downward along the left and right edges, respectively.
This replaces the standard “file/rank” convention used in 2D chess.

Each pair (x, y) represents:

x: number of tiles down along the left edge of that level, from the top-left corner.

y: number of tiles down along the right edge, from the same top-left reference.

These two values fully specify a position along both edges of the board, forming the oblique geometry that defines each level.


2. Point of View (POV)

The Point of View determines orientation of the grid and thus how coordinates are interpreted.

POV is declared at the start of any position record as:

(POV-White)
(POV-Black)
(POV-Neutral)


(POV-White) — the observer stands at the vertical edge nearest White’s home side.
Level KR is uppermost; counting proceeds downward through to QR.
Each coordinate (x, y) measures tile descent along the left and right boundaries from White’s orientation.

(POV-Black) — the observer stands at the opposite vertical edge.
Levels and coordinates are mirrored, so each opposing pair of indices sums to 9:
(POV-White) K@K4,4 corresponds to (POV-Black) K@K5,5.

(POV-Neutral) — used for mid-plane or diagrammatic analysis, with no directional bias.


3. Position Representation

Positions are represented as concise typographic strings that encode:

The POV declaration, and

Two board states (White and Black), each as a list of pieces with coordinates.

Example:

(POV-White) [White: K@K4,4; R@QR2,2] [Black: K@KB4,7]


Breakdown:

K@K4,4 — King on Level K, tile (4,4).

R@QR2,2 — Rook on Level QR, tile (2,2).

K@KB4,7 — opposing King on Level KB, tile (4,7).

Semicolons separate pieces within each side’s bracket.


4. Tile Colors

Each tile in 3D chess carries two simultaneous color designations:

Type	Domain	Colors
Bishop Color	traditional	White / Black
Duke Color	elemental	Gold / Silver / Ruby / Jade

From White’s POV:

Tile	Bishop	Duke
KR1,1	White	Gold
KR2,2	White	Silver
KR1,2	Black	Ruby
KR2,1	Black	Jade

From Black’s POV, the same tiles are perceived as:

Tile	Bishop	Duke
KR8,8	White	Gold
KR7,7	White	Silver
KR8,7	Black	Ruby
KR7,8	Black	Jade

Color identity remains invariant across perspectives even though coordinate indices invert.


5. Position Validation (Regex)

A regular expression ensures that every position string is syntactically valid:

^\(POV-(White|Black|Neutral)\)\s*
\[(White|Black|Gray):\s*(?:[KQRBDSNP]@[A-Z]{1,2}\d,\d(?:;\s*)?)*\]
(?:\s*\[Target:\s*@?[A-Z]{1,2}\d,\d\])?$


Definition summary:

POV-(White|Black|Neutral) — validates declared point of view.

[KQRBDSNP] — permits all standard and 3D pieces (K, Q, R, B, D, S, N, P).

[A-Z]{1,2} — matches level abbreviations (e.g., KR, KB, QR).

\d,\d — enforces numeric coordinate pair (x,y) each from 1–8.

White and Black lists enclosed in separate brackets.

Any mismatch, omission, or malformed entry (e.g. missing @, extra ;, unknown level) fails validation.


6. Regression test suite commands.

run regression           # auto-verbosity summary + fails expanded
show test L12_T051       # detailed view of one
show range L12_T200-215  # expand multiple
set verbosity quiet      # summary only
set verbosity verbose    # full expansion for all
rerun failed             # retest only failed

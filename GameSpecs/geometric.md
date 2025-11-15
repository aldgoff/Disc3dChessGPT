# Geometry Specification
**Version:** 0.1  
**Status:** 🚧 Inwork  
**Purpose:** Dfinitions of rays, planes, quadrants, advancement squares, and rectangles.

## Sections
1. Rays
2. Planes
3. Quadrants
4. Advancement Squares
5. Advancement Rectangles

## 1. Rays

### 2D Rays (Planar)

- The 2D board is a regular array of regular things, a square of squares.
- Each square has 8 adjacent neighbors:
  - 4 connected by sides (rook).
  - 4 connected by corners (bishop).
- Rays are composed of 1 to 2 unit vectors, specifed as doublets.
  - A rook ray has one zero unit vector.
  - A bishop ray has no zero unit vectors.
  - A unit vector is +1, or -1.

- Encodes all unit directions on a 3×3 grid centered on (0, 0).
- Each ray = (dx, dy) from the set {−1, 0, +1} excluding (0, 0).
- These are POV names: White's forward is Black's backward, etc.

Rook Rays — through sides (orthogonal)
|  #  |  dx |  dy | Name       |
| :-: | :-: | :-: | :--------- |
|  1  |  0  |  +1 | forwards   |
|  2  |  +1 |  0  | rightward  |
|  3  |  0  |  −1 | backwards  |
|  4  |  −1 |  0  | leftward   |

Bishop Rays — through corners (diagonal)
|  #  |  dx |  dy | Name           |
| :-: | :-: | :-: | :------------- |
|  5  |  +1 |  +1 | right_forward  |
|  6  |  +1 |  −1 | right_backward |
|  7  |  −1 |  −1 | left_backward  |
|  8  |  −1 |  +1 | left_forward   |

### 3D Rays (Spatial)

- The 3D board is a regular array of regular things, a cube of cubes.
- Each cube has 26 adjacent neighbors:
  -  6 connect be faces (rook).
  - 12 connect be edges (bishop).
  -  8 connect be vertices (duke).
- Rays are composed of 1 to 3 unit vectors, specifed as triplets:
  - A rook ray has two zero unit vectors
  - A bishop ray has one zero unit vector.
  - A duke ray has no zero unit vectors.
  - A unit vector is +1, or -1.

- Encodes all unit directions on a 3×3×3 cube centered on (0, 0, 0).
- Each ray = (dx, dy, dz) from the set {−1, 0, +1} excluding (0, 0, 0).
- These are POV names: White's left_out is Black's left_back, etc.

Name component definition table
| Component | Definition | Count |
| :-------- | :--------- | :---- |
| x         | +x or -x   |    2  |
| y         | +y or -y   |    2  |
| away      | +x or +y   |    6  |
| back      | -x or -y   |    6  |
| up        | +z         |    9  |
| down      | -z         |    9  |
| forward   | +x and +y  |    3  |
| backward  | -x and -y  |    3  |
| left      | +x and -y  |    7  |
| right     | -x and +y  |    7  |

Rook Rays — through faces (orthogonal planes)
|  #  |  dx |  dy |  dz | Name   |
| :-: | :-: | :-: | :-: | :----- |
|  1  |  +1 |  0  |  0  | x_away |
|  2  |  −1 |  0  |  0  | x_back |
|  3  |  0  |  +1 |  0  | y_away |
|  4  |  0  |  −1 |  0  | y_back |
|  5  |  0  |  0  |  +1 | up     |
|  6  |  0  |  0  |  −1 | down   |

Bishop Rays — through edges (skew planes)
|  #  |  dx |  dy |  dz | Name            |
| :-: | :-: | :-: | :-: | :-------------- |
|  7  |  +1 |  +1 |  0  | forward         |
|  8  |  +1 |  −1 |  0  | left            |
|  9  |  −1 |  +1 |  0  | right           |
|  10 |  −1 |  −1 |  0  | backward        |
|  11 |  +1 |  0  |  +1 | left_away_up    |
|  12 |  +1 |  0  |  −1 | left_away_down  |
|  13 |  −1 |  0  |  +1 | left_back_up    |
|  14 |  −1 |  0  |  −1 | left_back_down  |
|  15 |  0  |  +1 |  +1 | right_away_up   |
|  16 |  0  |  +1 |  −1 | right_away_down |
|  17 |  0  |  −1 |  +1 | right_back_up   |
|  18 |  0  |  −1 |  −1 | right_back_down |

Duke Rays — through vertices (slant planes)
|  #  |  dx |  dy |  dz | Name          |
| :-: | :-: | :-: | :-: | :------------ |
|  19 |  +1 |  +1 |  +1 | up_forward    |
|  20 |  +1 |  +1 |  −1 | down_forward  |
|  21 |  +1 |  −1 |  +1 | up_left       |
|  22 |  +1 |  −1 |  −1 | down_left     |
|  23 |  −1 |  +1 |  +1 | up_right      |
|  24 |  −1 |  +1 |  −1 | down_right    |
|  25 |  −1 |  −1 |  +1 | up_backward   |
|  26 |  −1 |  −1 |  −1 | down_backward |

Component tally (just a double check):
- 54 = 10 + 28 + 16

---

## 2. Planes ?!?


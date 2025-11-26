# Perimeters Spec

Perimeters:
- How direction and distance are defined in 3D chess.

## 1. Definition
  An advancement square is the ordered set of successive perimeters (0-k)

    An advancement square:
      is defined within **one quadrant** of **one plane**
      grows outward using **perimeters**, not ray steps
      encodes both **direction** (quadrant) and **distance** (perimeter index)


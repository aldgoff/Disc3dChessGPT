# Color Spec

## 1. Bishop color
    parity(z+x+y)
      0 → white
      1 → black

## 2. Duke Color (4-color 2×2×2 unit cell)
    Define:
      uz = z % 2
      ux = x % 2
      uy = y % 2

    The four duke colors are assigned exactly as follows:
      If uz = 0:
        (ux,uy) = (0,0) → Silver
                  (0,1) → Jade
                  (1,0) → Ruby
                  (1,1) → Gold
      If uz = 1:
        (ux,uy) = (0,0) → Gold
                  (0,1) → Ruby
                  (1,0) → Jade
                  (1,1) → Silver

## 3. Board Tiles
    The VTS color pattern repeats every 2 units along each axis.
    parse LLX,Y → (Z,X,Y)
    map to (z,x,y)
    apply bishop & duke colors

## 3. Equivalence Classes
    bishop color      - 1/2 of board - (bishop)
    duke color        - 1/4 of board - (duke)
    bishop-duke color - 1/8 of board - (stack)

Scope:
  - Defines bishop and duke colors and equivalence class assignment for VTS and Board tiles.

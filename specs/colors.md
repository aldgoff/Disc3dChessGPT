# Color Spec

## 1. Bishop Color
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

## 3. Combined Tile Color  
   The canonical board-tile color is the ordered pair:
       (bishop_color, duke_color)

## 4. Board Tiles
    The VTS color pattern repeats every 2 units along each axis.
    parse LLX,Y → (Z,X,Y)
    map to (z,x,y)
    apply bishop & duke colors

## 5. Equivalence Classes
    bishop color      - 1/2 of board - (bishop)
    duke color        - 1/4 of board - (duke)
    bishop-duke color - 1/8 of board - (stack)

## 6. Tile Color API
    All tile color functions accept either:
        • a board coordinate string, e.g. "A3C"
        • or a VTS tuple (z, x, y)

    The function MUST perform normalization by calling:
        coords.board_to_vts() if a board string is provided
        (no normalization is needed for VTS tuples)

    After normalization, color computations ALWAYS use VTS.

## 7. Functions
    bishop_color(tile)
        Input: tile (string or (z,x,y))
        Output: "white" or "black"

    duke_color(tile)
        Input: tile (string or (z,x,y))
        Output: "Gold", "Silver", "Ruby", or "Jade"

    tile_colors(tile)
        Input: tile (string or (z,x,y))
        Output: dict:
            {
                "bishop": bishop_color(...),
                "duke": duke_color(...),
                "vts":   (z,x,y)
            }

    tile_color_string(tile)
        Input: tile (string or (z,x,y))
        Output: "<bishop>-<duke>" string (for JSON)

Scope:
  - Defines bishop and duke colors and equivalence class assignment for VTS and Board tiles.

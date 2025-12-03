# Moves (L10) — Skeleton Spec

## 1. Purpose
  Define how a **piece + sweep quad-set** is interpreted as a **move type**.
  This layer classifies geometry; it does *not* test legality.

## 2. Inputs
  **piece** (from L9 pieces layer)
  **source tile, target tile** (L1)
  **sweep finds**: list of quadrants/quad-signatures (L8)

## 3. Matrix
  | Quads | Test                 | rook  |  bishop   | duke   |  queen  |    knight  |  stack   |  pawn  |  king |
  | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
      0   |  
      1   |
      2   |
      3   |
      4   |
      5   |
      6   | 6 duke quads                  linear
        1 rook, 4 bishop, 1 duke

## 3. Outputs
  * **move_type** (placeholder categories)
    * `quadrant_advance`
    * `linear_advance`
    * `quadrant_capture`
    * `linear_capture`
    * `overlap_move`
    * `stack_move`
    * `knight_jump`
    * `invalid`

## 4. General Structure
  1. Identify **eligible movement classes** from piece specification.
  2. Interpret sweep signature accordingly.
  3. Apply piece-specific overrides (pawn, king, stack, knight).
  4. Classify as one of the move types.

## 5. Geometry Classes (from sweep)
  * **Single-quad match** → quadrant candidate.
  * **Multi-quad match** → overlap candidate.
  * **Dual-plane intersection** → linear candidate.

  (Details to be added once L8–L7 interactions are finalized.)

## 6. Piece Overrides (Skeleton)
  ### 6.1 Pawn
    * Advance uses orthogonal quadrants only.
    * Captures use bishop capture geometry.
    * End-tile and Brook interpretations deferred.

  ### 6.2 King
    * Linear-only; range capped at 1.
    * No quadrant advance.

  ### 6.3 Knight
    * Ignores geometry; uses discrete offsets.

  ### 6.4 Stack
    * Decomposable piece; move classification must account for decay.
    * Overlap tiles fully accessible.

  ### 6.5 Base Pieces (rook, bishop, duke)
    * Pure planar or linear depending on signature.
    * Overlap interpretations piece-dependent.

  ### 6.6 Queen
    * Union of base pieces; uses overlap signature when present.

## 7. Classification Rules (Skeleton)
  1. **If piece is knight** → `knight_jump`.
  2. **If sweep reports multi-quad overlap**

    * If piece supports overlaps → `overlap_move`.
  3. **If sweep reports quadrant geometry**

    * If piece supports that plane → `quadrant_advance`.
  4. **If sweep reports linear geometry**

    * If piece supports linear → `linear_advance`.
  5. Else → `invalid`.

## 8. Deferred Sections
  * Advancement rectangle integration.
  * Pawn end-geometry.
  * Brook/Qtile/Feynman mapping.
  * Capture legality.
  * Blocking and path constraints.
  * Turn logic and global rules.

## 9. Notes

This file is intentionally skeletal and will be expanded incrementally per piece, per geometry class.

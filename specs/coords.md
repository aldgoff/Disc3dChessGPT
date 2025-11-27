# Coordinate System Spec

## 1. VTS coordinates
    Form: (z,x,y) with z,x,y ∈ 0–29

## 2. Board coordinates
    Form: LLX,Y
    LL ∈ {QR,QN,QB, Q,K, KB,KN,KR}
    X,Y ∈ 1–8
    Z is given by LL using the level table:
    QR→1, QN→2, QB→3, Q→4, K→5, KB→6, KN→7, KR→8
    A Board tile is valid when Z,X,Y ∈ 1–8 (assumes 8x8x8 board)

  ### 2.1 Anchor
    Board (1,1,1) = VTS (Az,Ax,Ay)
    For the 8x8x8 board
      Az = 11
      Ax = 11
      Ay = 11

## 3. Conversions
    Board → VTS (White POV)
      z = (Az - 1) + Z
      x = (Ax - 1) + X
      y = (Ay - 1) + Y

    VTS → Board (White POV)
      Z = z − (Az - 1)
      X = x − (Ax - 1)
      Y = y − (Ay - 1)

    Mapping validity
      Results must fall in the defined Board and VTS ranges

## 4. Formats
    LLX,Y identifies Board-space
    (z,x,y) identifies VTS-space
    Formats are disjoint

## 5. Membership
    On-board iff Z,X,Y ∈ 1–8
    Format does not decide membership

## 6. Parsing
    In LLX,Y, LL is the level prefix; X,Y are decimal integers
    LL determines Z by table lookup
    Parsed Board coordinate is (Z,X,Y)

Scope:
  - Defines VTS and Board coordinates, Board/VTS formats, Board parsing, anchor, affine mapping, and on-board membership.

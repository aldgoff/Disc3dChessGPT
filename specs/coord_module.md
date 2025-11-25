# Coordinate System Module
  VTS coordinates
    Form: (z,x,y) with z,x,y ∈ 0–29

  Board coordinates
    Form: LLX,Y
    LL ∈ {QR,QN,QB,Q,K,KB,KN,KR}
    X,Y ∈ 1–8
    Z is given by LL using the level table:
    QR→1, QN→2, QB→3, Q→4, K→5, KB→6, KN→7, KR→8
    A Board tile is valid when Z,X,Y ∈ 1–8

  Anchor
    Board (1,1,1) = VTS (11,11,11)

  Board → VTS (White POV)
    z = 10 + Z
    x = 10 + X
    y = 10 + Y

  VTS → Board (White POV)
    Z = z − 10
    X = x − 10
    Y = y − 10

  Mapping validity
    Results must fall in the defined Board and VTS ranges

  Formats
    LLX,Y identifies Board-space
    (z,x,y) identifies VTS-space
    Formats are disjoint

  Membership
    On-board iff Z,X,Y ∈ 1–8
    Format does not decide membership

  Parsing
    In LLX,Y, LL is the level prefix; X,Y are decimal integers
    LL determines Z by table lookup
    Parsed Board coordinate is (Z,X,Y)

  Scope
    Defines VTS and Board coordinates, Board/VTS formats, Board parsing, anchor, affine mapping, and on-board membership.

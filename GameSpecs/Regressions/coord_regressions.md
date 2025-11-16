# SUITE: coordinates

## Series: vts-basics  (fold)

	VT-B1: {
	category: "coordinates/vts-basics",
	query: "Is VTS defined as a 30x30x30 integer lattice?",
	expect: "yes",
	mode: "S"
	}

	VT-B2: {
	category: "coordinates/vts-basics",
	query: "What is the valid range for VTS x?",
	expect: "0-29",
	mode: "CR"
	}

	VT-B3: {
	category: "coordinates/vts-basics",
	query: "Is (30,0,0) a valid VTS coordinate?",
	expect: "no",
	mode: "S"
	}

	VT-B4: {
	category: "coordinates/vts-basics",
	query: "Is z-axis the third component of VTS coordinates?",
	expect: "yes",
	mode: "S"
	}

---

## Series: bishop-color  (fold)

  BC-1: {
    category: "coordinates/bishop-color",
    query: "What is bishop color of VTS (0,0,0)?",
    expect: "white",
    mode: "S"
  }

  BC-2: {
    category: "coordinates/bishop-color",
    query: "What is bishop color of VTS (1,0,0)?",
    expect: "black",
    mode: "CR"
  }

  BC-3: {
    category: "coordinates/bishop-color",
    query: "Compute bishop color at (2,3,4).",
    expect: "white",
    mode: "C"
  }

---

## Series: duke-color  (fold)

  DC-1: {
    category: "coordinates/duke-color",
    query: "What is duke color of VTS (0,0,0)?",
    expect: "Silver",
    mode: "CR"
  }

  DC-2: {
    category: "coordinates/duke-color",
    query: "What is duke color of VTS (1,1,0)?",
    expect: "Gold",
    mode: "C"
  }

  DC-3: {
    category: "coordinates/duke-color",
    query: "What is duke color at (2,2,2)?  (same parity tile as 0,0,0)",
    expect: "Silver",
    mode: "S"
  }

  DC-4: {
    category: "coordinates/duke-color",
    query: "Is z-parity used to determine 2x2x2 cell pattern?",
    expect: "yes",
    mode: "S"
  }

---

## Series: vts-unit-cell  (fold)

  UC-1: {
    category: "coordinates/vts-unit-cell",
    query: "Does VTS color pattern repeat every 2 units in each axis?",
    expect: "yes",
    mode: "CR"
  }

  UC-2: {
    category: "coordinates/vts-unit-cell",
    query: "Do (3,4,5) and (1,2,3) share the same bishop and duke colors?",
    expect: "yes",
    mode: "C"
  }

---

## Series: board-basics  (fold)

  BB-1: {
    category: "coordinates/board-basics",
    query: "What is the dimension of the standard board?",
    expect: "8x8x8",
    mode: "S"
  }

  BB-2: {
    category: "coordinates/board-basics",
    query: "What are the valid board X values?",
    expect: "1-8",
    mode: "CR"
  }

  BB-3: {
    category: "coordinates/board-basics",
    query: "Do players sit on opposite vertical edges?",
    expect: "yes",
    mode: "S"
  }

---

## Series: z-labels  (fold)

  ZL-1: {
    category: "coordinates/z-labels",
    query: "What VTS z corresponds to board level K?",
    expect: "15",
    mode: "CR"
  }

  ZL-2: {
    category: "coordinates/z-labels",
    query: "What is the Z-label for VTS z=11?",
    expect: "QR",
    mode: "S"
  }

  ZL-3: {
    category: "coordinates/z-labels",
    query: "Are Z-labels uppercase?",
    expect: "yes",
    mode: "S"
  }

---

## Series: anchor-mapping  (fold)

  AM-1: {
    category: "coordinates/anchor-mapping",
    query: "What is the standard board anchor (Ax,Ay,Az)?",
    expect: "11,11,11",
    mode: "CR"
  }

  AM-2: {
    category: "coordinates/anchor-mapping",
    query: "What is VTS location of board tile QR1,1?",
    expect: "11,11,11",
    mode: "C"
  }

  AM-3: {
    category: "coordinates/anchor-mapping",
    query: "What are VTS extents of the standard 8x8x8 board in x?",
    expect: "11-18",
    mode: "CR"
  }

---

## Series: board-to-vts  (fold)

  BV-1: {
    category: "coordinates/board-to-vts",
    query: "Convert board (K,2,2) to VTS coordinates.",
    expect: "12,12,15",
    mode: "C"
  }

  BV-2: {
    category: "coordinates/board-to-vts",
    query: "Convert QR1,8 to VTS.",
    expect: "11,18,11",
    mode: "C"
  }

  BV-3: {
    category: "coordinates/board-to-vts",
    query: "Does increasing board Z always increase VTS z?",
    expect: "yes",
    mode: "CR"
  }

---

## Series: vts-to-board-white  (fold)

  VW-1: {
    category: "coordinates/vts-to-board-white",
    query: "Convert VTS (11,11,11) to board (White POV).",
    expect: "QR1,1",
    mode: "C"
  }

  VW-2: {
    category: "coordinates/vts-to-board-white",
    query: "Convert VTS (18,18,18) to board (White POV).",
    expect: "KR8,8",
    mode: "CR"
  }

  VW-3: {
    category: "coordinates/vts-to-board-white",
    query: "If a VTS tile gives board coordinates outside 1-8 range, is it off-board?",
    expect: "yes",
    mode: "S"
  }

---

## Series: vts-to-board-black  (fold)

  VB-1: {
    category: "coordinates/vts-to-board-black",
    query: "Convert VTS (18,11,11) to board (Black POV).",
    expect: "KR1,8",
    mode: "C"
  }

  VB-2: {
    category: "coordinates/vts-to-board-black",
    query: "Does Black see board X mirrored from White?",
    expect: "yes",
    mode: "CR"
  }

  VB-3: {
    category: "coordinates/vts-to-board-black",
    query: "Convert VTS (11,18,18) for Black.",
    expect: "QR8,1",
    mode: "C"
  }

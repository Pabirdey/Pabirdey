.table-container {
    max-height: 60vh;
    overflow: auto;          /* Enables vertical + horizontal scroll */
}

#tblBinDetails {
    min-width: 900px;        /* Force horizontal scroll */
    border-collapse: separate;
    border-spacing: 0;
}

/* ===== Sticky Header ===== */
#tblBinDetails thead th {
    position: sticky;
    top: 0;
    background: #ffffff;     /* Prevent overlap issue */
    z-index: 5;
}

/* ===== Freeze First Column ===== */
#tblBinDetails th:first-child,
#tblBinDetails td:first-child {
    position: sticky;
    left: 0;
    background: #ffffff;
    z-index: 4;
}

/* ===== Fix Top-Left Corner Layer ===== */
#tblBinDetails thead th:first-child {
    z-index: 6;
}
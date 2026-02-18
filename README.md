/* ===== FLEXBOX FOR TABLES ===== */

.Consumption {
    display: flex;
    gap: 10px;
    align-items: flex-start;
    flex-wrap: wrap;
    margin-top: 20px;
}

/* LEFT TABLE */
#materialTable {
    flex: 2;
    margin-left: 5px;   /* 👈 Left margin added */
    min-width: 60%;
    background: white;
}

/* RIGHT TABLE (SMALL WIDTH) */
#types {
    flex: 0 0 250px;   /* 👈 Fixed small width */
    max-width: 250px;
    background: white;
}
.scrollable-table {
    max-height: 318px;
    overflow-x: auto;
    overflow-y: auto;
    position: relative;
}

/* Freeze Cast No column horizontally */
#Mudgun_Details th:first-child,
#Mudgun_Details td:first-child {
    position: sticky;
    left: 0;
    background: #ffffff;
    z-index: 3;
    min-width: 120px;
}

/* Keep header above body */
#Mudgun_Details thead th:first-child {
    background: #f8f9fa;
    z-index: 5;
}

.table td {
    line-height: 1.1 !important;
}
/* ===== Responsive Font & Table Scaling ===== */
@media screen and (max-width: 1366px) {

    .Main-Heading {
        font-size: 4vh;
    }

    .section-title,
    .section_Exception-title,
    .section-Drill-title,
    legend {
        font-size: 14px !important;
    }

    th,
    td {
        font-size: 11px !important;
        padding: 2px !important;
    }

    .table-input,
    input,
    select,
    textarea {
        font-size: 11px !important;
        padding: 2px 4px !important;
        height: 26px;
    }

    .Long_Heading,
    .Long_Heading_Medium,
    .Heading_Small,
    .Heading_Tiny {
        font-size: 11px !important;
    }

    .btnSaveCastHouse,
    .btn,
    button {
        font-size: 11px !important;
        padding: 3px 8px !important;
    }

    label,
    span,
    option {
        font-size: 12px !important;
    }

    .scrollable-table {
        overflow-x: auto;
    }

    table {
        white-space: nowrap;
    }
}

/* Extra compact mode for small monitors */
@media screen and (max-width: 1024px) {

    th,
    td {
        font-size: 9px !important;
        padding: 1px !important;
    }

    .table-input,
    input,
    select {
        font-size: 9px !important;
        height: 22px;
    }

    .btnSaveCastHouse,
    .btn {
        font-size: 9px !important;
    }

    .Main-Heading {
        font-size: 3vh;
    }
}

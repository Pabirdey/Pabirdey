<style>
/* ===== Global ===== */
body {
    background-image: linear-gradient(90deg, #FFE259, #FFA751);
    font-family: Arial, sans-serif;
}

/* ===== Headings ===== */
.Main-Heading {
    font-family: Allan, cursive;
    font-weight: bold;
    font-size: 6vh;
    text-align: center;
    padding: 20px;
    color: rgb(57,57,57);
    text-shadow: rgba(13, 0, 77, 0.08) 0px 2px 4px,
                 rgba(13, 0, 77, 0.08) 0px 3px 6px,
                 rgba(13, 0, 77, 0.08) 0px 8px 16px;
    border-radius: 10px;
    margin: 20px 0;
}

/* ===== Sections ===== */
.form-section {
    background: #ffffff;
    padding: 20px;
    border-radius: 20px;
    box-shadow: 0 10px 20px rgba(0,0,0,0.1);
    margin-bottom: 25px;
    overflow: visible;
    border: 1px solid #ccc;
    font-family: Courier New, Courier, monospace;
}

.section-title,
.section_Exception-title,
.section-Drill-title {
    background: #EEB86D;
    color: black;
    padding: 5px 10px;
    font-weight: bold;
    border-radius: 10px;
    margin-bottom: 10px;
    font-family: Courier New, Courier, monospace;
}

.section-title { font-size: 18px; }
.section_Exception-title { font-size: 15px; width: 15vh; }
.section-Drill-title { font-size: 20px; border-radius: 4px; }

/* ===== Forms ===== */
.form-control-lg {
    font-size: 1.5rem;
    font-family: Courier New, Courier, monospace;
    color: black;
}

.form-group {
    border-radius: 25px;
    border: 4px solid #73AD21;
    padding: 10px;
    margin: 10px;
    width: 500px;
}

/* ===== Tables ===== */
th {
    font-family: Courier New, Courier, monospace;
    font-size: 14px;
    font-weight: bold;
    border: 1px solid;
    color: white;
}

.table th,
.table td {
    text-align: center;
    vertical-align: middle;
}

.scrollable-table {
    overflow-y: auto;
}

.table thead th {
    position: sticky;
    top: 0;
    z-index: 2;
    border: 1px solid;
}

/* ===== Column Widths ===== */
.Long_Heading { min-width: 130px; }
.Long_Heading_Medium { min-width: 100px; }
.Heading_Tiny { width: 20px; white-space: nowrap; }
.Heading_Small { width: 10px; white-space: nowrap; }

/* ===== Inputs ===== */
.table-input {
    font-size: 1rem;
    padding: 2px 4px;
    border: 2px solid;
}

.highlight {
    background-color: #ffe08a !important;
}

/* ===== Buttons ===== */
.btnSaveCastHouse {
    background: linear-gradient(to bottom right, #EF4765, #FF9A5A);
    border: 0;
    border-radius: 10px;
    color: #FFFFFF;
    cursor: pointer;
    font-family: Courier New, Courier, monospace;
    font-size: 15px;
    font-weight: bold;
    line-height: 2.5;
    padding: 0 1rem;
    width: 12vh;
    margin-left: 30px;
    margin-top: 100px;
    transition: box-shadow .2s ease-in-out;
}

.btnSaveCastHouse:hover,
.btnSaveCastHouse:focus {
    box-shadow: 0 0 .25rem rgba(0,0,0,.5),
                -.125rem -.125rem 1rem rgba(239,71,101,.5),
                .125rem .125rem 1rem rgba(255,154,90,.5);
}

.btnHMLogistics {
    margin: 10px;
    padding: 15px 30px;
    font-weight: bold;
    color: white;
    border-radius: 10px;
    border: 0;
    background-image: linear-gradient(45deg, #FF512F 0%, #F09819 51%, #FF512F 100%);
    background-size: 200% auto;
    cursor: pointer;
    transition: 0.5s;
    box-shadow: 0px 0px 14px -7px #f09819;
}

.btnHMLogistics:hover {
    background-position: right center;
}

.btnHMLogistics:active {
    transform: scale(0.95);
}

/* ===== Dropdown Fix ===== */
select {
    appearance: auto !important;
    -webkit-appearance: auto !important;
    -moz-appearance: auto !important;
}

/* ===== SweetAlert ===== */
.my-swal-popup { font-family: Arial, sans-serif; }
.my-swal-title { font-family: Georgia, serif; font-size: 22px; }
.my-swal-text { font-family: Verdana, sans-serif; font-size: 18px; }

/* ===== Mudgun Clay Dropdown ===== */
.mgClayWrapper {
    position: relative;
    display: flex;
    align-items: center;
}

.mgClayWrapper .mgClayInput {
    width: 100%;
}

.mgClayWrapper button {
    margin-left: 5px;
}

.mgClayList {
    display: none;
    position: absolute;
    background: white;
    border: 1px solid #ccc;
    z-index: 1000;
    top: 30px;
    left: 0;
    width: 150px;
    max-height: 150px;
    overflow-y: auto;
}

.mgClayList div {
    padding: 5px;
    cursor: pointer;
}

.mgClayList div:hover {
    background: #eee;
}

/* ===== Misc ===== */
#backgrcol_Tap_hole {
    color: white;
    font-weight: bold;
    padding: 8px;
}
</style>

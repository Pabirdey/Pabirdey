<!DOCTYPE html>
<html>
<head>
    <title>Furnace Material Report</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            padding: 20px;
        }

        .top-section {
            display: flex;
            gap: 50px;
            margin-bottom: 20px;
        }

        label {
            font-weight: bold;
            display: block;
            margin-bottom: 5px;
        }

        select, input[type="date"] {
            padding: 6px;
            width: 180px;
        }

        table {
            border-collapse: collapse;
            width: 100%;
            margin-top: 20px;
        }

        th {
            background-color: #2f3e4d;
            color: white;
            padding: 10px;
            text-align: left;
        }

        td {
            border: 1px solid #ccc;
            padding: 10px;
        }

        .types-section {
            margin-top: 15px;
        }
    </style>
</head>
<body>

    <h2>Furnace Material Report</h2>

    <!-- Top Section -->
    <div class="top-section">
        <div>
            <label>Date</label>
            <input type="date" id="reportDate">
        </div>

        <div>
            <label>Furnace</label>
            <select id="furnaceSelect">
                <option value="A">A</option>
                <option value="B">B</option>
                <option value="C" selected>C</option>
            </select>
        </div>

        <div>
            <label>Types</label>
            <select id="typeSelect" onchange="loadData()">
                <option value="">-- Select Type --</option>
                <option value="IPC">IPC</option>
                <option value="RPC">RPC</option>
                <option value="CURRAGH">CURRAGH</option>
            </select>
        </div>
    </div>

    <!-- Table -->
    <table>
        <thead>
            <tr>
                <th>Material</th>
                <th>Value (Tons)</th>
                <th>Value (Kgs)</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>Coal</td>
                <td id="coalTons">0</td>
                <td id="coalKgs">0</td>
            </tr>
            <tr>
                <td>Nut Coke</td>
                <td id="nutTons">0</td>
                <td id="nutKgs">0</td>
            </tr>
            <tr>
                <td>Noa Ore / LRP</td>
                <td id="oreTons">0</td>
                <td id="oreKgs">0</td>
            </tr>
            <tr>
                <td>Sinter</td>
                <td id="sinterTons">0</td>
                <td id="sinterKgs">0</td>
            </tr>
            <tr>
                <td>Quartz</td>
                <td id="quartzTons">0</td>
                <td id="quartzKgs">0</td>
            </tr>
        </tbody>
    </table>

<script>
    // Sample Data (You can replace with API data)
    const materialData = {
        IPC: {
            coal: 327.49,
            nut: 120.87,
            ore: 0,
            sinter: 1590.73,
            quartz: 51.74
        },
        RPC: {
            coal: 210.10,
            nut: 95.50,
            ore: 50.00,
            sinter: 1300.25,
            quartz: 40.12
        },
        CURRAGH: {
            coal: 400.00,
            nut: 150.00,
            ore: 20.00,
            sinter: 1700.00,
            quartz: 60.00
        }
    };

    function loadData() {
        const selectedType = document.getElementById("typeSelect").value;

        if (!materialData[selectedType]) {
            clearTable();
            return;
        }

        const data = materialData[selectedType];

        updateRow("coal", data.coal);
        updateRow("nut", data.nut);
        updateRow("ore", data.ore);
        updateRow("sinter", data.sinter);
        updateRow("quartz", data.quartz);
    }

    function updateRow(material, tons) {
        document.getElementById(material + "Tons").innerText = tons.toFixed(2);
        document.getElementById(material + "Kgs").innerText = (tons * 1000).toFixed(2);
    }

    function clearTable() {
        const ids = ["coal", "nut", "ore", "sinter", "quartz"];
        ids.forEach(id => {
            document.getElementById(id + "Tons").innerText = "0";
            document.getElementById(id + "Kgs").innerText = "0";
        });
    }
</script>

</body>
</html>
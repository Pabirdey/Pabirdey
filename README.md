@model ProcessTrends.Models.RawMaterialQuantity
@{
    Layout = null;
}
<!DOCTYPE html>
<html>
<head>
    <title>Raw Material Quantity</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <style>
        .form-label {
            font-weight: 600;
            font-family: Georgia;
        }

        .section-divider {
            border: 3px solid #8e2626;
            width: 100%;
            margin: 20px auto;        
        }

        .material-row .form-label {
            padding-top: 0.375rem;
        }

        .material-row .col-md-2 {
            display: flex;
            align-items: center;
        }

        .material-row .form-control {
            width: 150px;
        }

        .material-row label {
            min-width: 140px;
            margin-right: 10px;
        }
        h6{
            font-family:Georgia, 'Times New Roman', Times, serif;
            font-weight:bold;
            color:#8e2626;
        }
        
    </style>
</head>
<body>
    <div class="container-fluid mt-4">
        <h4 class="mb-4" style="font-family:'Comic Sans MS';text-align:center;font-weight:bold;color:#4CAF50;font-size:xx-large;">Raw Material Quantity</h4>
        <hr class="section-divider">
        <form method="post" action="/Blast_FurnaceController/RawMaterialEntry" id="rawMaterialForm">>
            <div class="container-fluid" style="margin-left:280px;">
                <div class="d-flex flex-nowrap gap-2 align-items-end">
                    <div style="width:8%;">
                        <label class="form-label" style="margin-left:40px;">Pile No</label>
                        <input type="text" name="PileNo" class="form-control" value="@Model?.PileNo">
                    </div>
                    <div style="width:8%;">
                        <label class="form-label" style="margin-left:40px;">Source</label>
                        <select name="Source" class="form-control" onchange="document.getElementById('rawMaterialForm').submit();">
                            <option value="">Select Source</option>
                            <option value="RMBB_KNR" @(Model !=null && Model.Source == "RMBB_KNR" ? "selected" : "")>RMBB_KNR</option>
                            <option value="RMBB" @(Model != null && Model.Source == "RMBB" ? "selected" : "")>RMBB</option>
                            <option value="RMBBN" @(Model != null && Model.Source == "RMBBN" ? "selected" : "")>RMBBN</option>
                        </select>

                    </div>
                    <div style="width:8%">
                        <label class="form-label" style="margin-left:40px;">Shift</label>
                        <select class="form-select">
                            <option value="A">A</option>
                            <option value="B">B</option>
                            <option value="C">C</option>iro
                        </select>
                    </div>
                    <div style="width:12%;">
                        <label class="form-label fw-bold" style="margin-left:40px;">Start Date</label>
                        <input type="datetime-local" class="form-control" value="@Model.StartDate">
                    </div>
                    <div style="width:12%;">
                        <label class="form-label" style="margin-left:40px;">End Date</label>
                        <input type="datetime-local" class="form-control" value="@Model.EndDate">
                    </div>
                    <div style="width:12%;">
                        <label class="form-label" style="margin-left:40px;">Cons.St.Date</label>
                        <input type="datetime-local" class="form-control" value="@Model.ConsStartDate">
                    </div>
                </div>
            </div>
            <hr class="section-divider">
            <!-- First row of materials -->
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Noa Fines</label>
                    <input class="form-control" type="text" value="@Model.NoaFines">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Joda Fines</label>
                    <input class="form-control" type="text" value="@Model.JodaFines">
                </div>
                <div class="col-md-2">
                    <label class="form-label">KB Fines</label>
                    <input class="form-control" type="text" value="@Model.KBFines">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Yard Fines</label>
                    <input class="form-control" type="text" value="@Model.YardFines">
                </div>
                <div class="col-md-2">
                    <label class="form-label">BHJ</label>
                    <input class="form-control" type="text" value="@Model.BHJ">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Namisa</label>
                    <input class="form-control" type="text" value="@Model.Namisa">
                </div>
            </div>           
        </form>
    </div>
    <hr class="section-divider">
</body>
</html>



 public ActionResult RawMaterialEntry()
        {
            return View(new RawMaterialQuantity());
        }

        [HttpPost]
        public ActionResult RawMaterialEntry(RawMaterialQuantity input)
        {
            RawMaterialQuantity model = new RawMaterialQuantity();
            model.PileNo = input.PileNo;
            model.Source = input.Source;
            

            using (OracleConnection conn = new OracleConnection(mycon))
            {
                conn.Open();

                string query = "SELECT * FROM imtg.T_PILE_RAWMAT_QUANTITY_NEW WHERE PILE_NO = :pileNo AND SOURCE = :source";

                using (OracleCommand cmd = new OracleCommand(query, conn))
                {
                    cmd.Parameters.Add(new OracleParameter("pileNo", input.PileNo));
                    cmd.Parameters.Add(new OracleParameter("source", input.Source));

                    using (OracleDataReader reader = cmd.ExecuteReader())
                    {
                        if (reader.Read())
                        {
                            model.NoaFines = reader["NOA_FINES"] != DBNull.Value ? Convert.ToDecimal(reader["NOA_FINES"]) : 0;
                           
                        }
                    }
                }
            }

            return View(model);
        }
    

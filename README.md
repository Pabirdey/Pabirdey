public class RawMaterialModel
{
    public string PileNo { get; set; }
    public string Source { get; set; }

    public string NoaFines { get; set; }
    public string JodaFines { get; set; }
    public string KBFines { get; set; }
    public string YardFines { get; set; }
    public string BHJ { get; set; }
    public string Namisa { get; set; }

    public string FortescueBF { get; set; }
    public string NoaCrushed { get; set; }
    public string JodaCrushed { get; set; }
    public string KBCrushed { get; set; }
    public string Pilbhara { get; set; }
    public string Kumba { get; set; }

    public string CoastalFines { get; set; }
    public string DeobharKatamatiFines { get; set; }
    public string KirandulSOLump { get; set; }
    public string KirandulFines { get; set; }
    public string FSFVenezuelan { get; set; }
    public string SNFeedValue { get; set; }

    public string OtherImpOre { get; set; }
    public string ImpOreFines { get; set; }
    public string Bacheli { get; set; }
    public string Jaroli { get; set; }
    public string KayPeeEntp { get; set; }
    public string Daitari { get; set; }

    public string DomesticIOF { get; set; }
    public string IronOreFines { get; set; }
}

using System.Web.Mvc;
using YourApp.Models;
using Oracle.ManagedDataAccess.Client;
using System.Data;

public class RawMaterialController : Controller
{
    public ActionResult Index()
    {
        return View(new RawMaterialModel());
    }

    [HttpPost]
    public ActionResult Index(RawMaterialModel input)
    {
        RawMaterialModel model = new RawMaterialModel();
        model.PileNo = input.PileNo;
        model.Source = input.Source;

        string connectionString = "User Id=your_user;Password=your_password;Data Source=your_datasource";

        using (OracleConnection conn = new OracleConnection(connectionString))
        {
            conn.Open();

            string query = "SELECT * FROM RAW_MATERIAL_TABLE WHERE PILE_NO = :pileNo AND SOURCE = :source";

            using (OracleCommand cmd = new OracleCommand(query, conn))
            {
                cmd.Parameters.Add(new OracleParameter("pileNo", input.PileNo));
                cmd.Parameters.Add(new OracleParameter("source", input.Source));

                using (OracleDataReader reader = cmd.ExecuteReader())
                {
                    if (reader.Read())
                    {
                        model.NoaFines = reader["NOA_FINES"]?.ToString();
                        model.JodaFines = reader["JODA_FINES"]?.ToString();
                        model.KBFines = reader["KB_FINES"]?.ToString();
                        model.YardFines = reader["YARD_FINES"]?.ToString();
                        model.BHJ = reader["BHJ"]?.ToString();
                        model.Namisa = reader["NAMISA"]?.ToString();

                        model.FortescueBF = reader["FORTESCUE_BF"]?.ToString();
                        model.NoaCrushed = reader["NOA_CRUSHED"]?.ToString();
                        model.JodaCrushed = reader["JODA_CRUSHED"]?.ToString();
                        model.KBCrushed = reader["KB_CRUSHED"]?.ToString();
                        model.Pilbhara = reader["PILBHARA"]?.ToString();
                        model.Kumba = reader["KUMBA"]?.ToString();

                        model.CoastalFines = reader["COASTAL_FINES"]?.ToString();
                        model.DeobharKatamatiFines = reader["DEOBHAR_KATAMATI_FINES"]?.ToString();
                        model.KirandulSOLump = reader["KIRANDUL_SO_LUMP"]?.ToString();
                        model.KirandulFines = reader["KIRANDUL_FINES"]?.ToString();
                        model.FSFVenezuelan = reader["FSF_VENEZUELAN"]?.ToString();
                        model.SNFeedValue = reader["SN_FEED_VALUE"]?.ToString();

                        model.OtherImpOre = reader["OTHER_IMP_ORE"]?.ToString();
                        model.ImpOreFines = reader["IMP_ORE_FINES"]?.ToString();
                        model.Bacheli = reader["BACHELI"]?.ToString();
                        model.Jaroli = reader["JAROLI"]?.ToString();
                        model.KayPeeEntp = reader["KAY_PEE_ENTP"]?.ToString();
                        model.Daitari = reader["DAITARI"]?.ToString();

                        model.DomesticIOF = reader["DOMESTIC_IOF"]?.ToString();
                        model.IronOreFines = reader["IRON_ORE_FINES"]?.ToString();
                    }
                }
            }
        }

        return View(model);
    }
}


@model YourApp.Models.RawMaterialModel

<form method="post" action="/RawMaterial/Index">
    <div class="row mb-3">
        <div class="col-md-2">
            <label>Pile No</label>
            <input name="PileNo" class="form-control" value="@Model.PileNo" />
        </div>
        <div class="col-md-2">
            <label>Source</label>
            <select name="Source" class="form-control">
                <option selected>@Model.Source</option>
                <option>RMBB_KNR</option>
                <option>RMBB_JSG</option>
                <option>RMBB_BSP</option>
            </select>
        </div>
        <div class="col-md-2">
            <label>&nbsp;</label>
            <button type="submit" class="btn btn-primary form-control">Fetch</button>
        </div>
    </div>

    <div class="row mb-2">
        <div class="col-md-2"><label>Noa Fines</label><input name="NoaFines" class="form-control" value="@Model.NoaFines" /></div>
        <div class="col-md-2"><label>Joda Fines</label><input name="JodaFines" class="form-control" value="@Model.JodaFines" /></div>
        <div class="col-md-2"><label>KB Fines</label><input name="KBFines" class="form-control" value="@Model.KBFines" /></div>
        <div class="col-md-2"><label>Yard Fines</label><input name="YardFines" class="form-control" value="@Model.YardFines" /></div>
        <div class="col-md-2"><label>BHJ</label><input name="BHJ" class="form-control" value="@Model.BHJ" /></div>
        <div class="col-md-2"><label>Namisa</label><input name="Namisa" class="form-control" value="@Model.Namisa" /></div>
    </div>

    <!-- Repeat this .row for every group of 6 fields shown in the image -->
</form>
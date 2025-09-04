using iMonitor_Web.CustomSecurity;
using iMonitor_Web.Models;
using Oracle.ManagedDataAccess.Client;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.Mvc;

namespace iMonitor_Web.Controllers
{
    [CustomAuthorization(Role = "Operator")]
    public class RmbbPileController : Controller
    {

        // GET: Pile
        public ActionResult RmbbPile()
        {
            return View(new RmbbPile());
        }

        public List<SelectListItem>GetBlendNumbers()
        {
            List<SelectListItem> blendList = new List<SelectListItem>();
            using (OracleConnection conn = new OracleConnection(iMonitorWebUtils.msConRWString))
            {
                conn.Open();
                string blendsql = string.Empty;
                blendsql = "Select distinct(BLEND_NO) BLEND_NO From T_PSW_DAILY Where SOURCE='RMBB_KNR' And BLEND_NO>0 Order by BLEND_NO";
                using (OracleCommand cmd = new OracleCommand(blendsql, conn))
                using (OracleDataReader reader = cmd.ExecuteReader())
                {
                    while(reader.Read())
                    {
                        blendList.Add(new SelectListItem
                        {
                            Value = reader["BLEND_NO"].ToString(),
                            Text = reader["BLEND_NO"].ToString()
                        });
                    }
                }
                
            }
            return blendList;
        }
        [HttpPost]
        public ActionResult RmbbPile(RmbbPile input, string SaveRawMaterial)
        {
            RmbbPile model = new RmbbPile();
            ViewBag.PSW_BL1 = GetBlendNumbers();
            ViewBag.PSW_BL2 = GetBlendNumbers();
            string message = "";
            bool recordFound = false;
            if (!string.IsNullOrEmpty(SaveRawMaterial))
            {

                using (OracleConnection conn = new OracleConnection(iMonitorWebUtils.msConRWString))
                {
                    conn.Open();

                    decimal? LD_Sludge_Cons = null, Mill_Scale_Cons = null, Flue_Dust_Cons = null, Esp_Dust_Cons = null,
                     Kiln_Dust_Cons = null, Gcp_Sludge_Cons = null, Lime_Fines_Cons = null, Wrp_MET_Cons = null,
                     LD_Slag_Fines_Cons = null, Mill_Sludge_Cons = null;

                    string blendQuery = @"SELECT SUM(LD_Sludge),SUM(Mill_Scale),SUM(Flue_Dust),SUM(Esp_Dust),SUM(Kiln_Dust),SUM(Gcp_Sludge),SUM(Lime_Fines),SUM(Wrp_MET),SUM(LD_Slag_Fines),SUM(MILL_SLUDGE) 
                    FROM (
                        SELECT 
                            :vPSW1*AVG(LD_Sludge) / 100 AS LD_Sludge,
                            :vPSW1*AVG(Mill_Scale) / 100 AS Mill_Scale,
                            :vPSW1*AVG(Flue_Dust) / 100 AS Flue_Dust,
                            :vPSW1*AVG(Esp_Dust) / 100 AS Esp_Dust,
                            :vPSW1*AVG(Kiln_Dust) / 100 AS Kiln_Dust,
                            :vPSW1*AVG(Gcp_Sludge) / 100 AS Gcp_Sludge,
                            :vPSW1*AVG(Lime_Fines) / 100 AS Lime_Fines,
                            :vPSW1*AVG(WRP_MET) / 100 AS Wrp_MET,
                            :vPSW1*AVG(LD_Slag_Fines) / 100 AS LD_Slag_Fines,
                            :vPSW1*AVG(MILL_SLUDGE) / 100 AS MILL_SLUDGE
                        FROM T_PSW_DAILY WHERE TRIM(SOURCE) = 'RMBB_KNR' AND TIMESTAMP >= TRUNC(:prepEndDate) - 200 AND BLEND_NO=:BL1
                            Union
						SELECT
                            :vPSW2*Avg(LD_Sludge)/100 LD_Sludge,
                            :vPSW2*Avg(Mill_Scale)/100 Mill_Scale,
                            :vPSW2*Avg(Flue_Dust)/100 Flue_Dust,
                            :vPSW2*Avg(Esp_Dust)/100 Esp_Dust,
                            :vPSW2*Avg(Kiln_Dust)/100 Kiln_Dust,
                            :vPSW2*Avg(Gcp_Sludge)/100 Gcp_Sludge,
                            :vPSW2*Avg(Lime_Fines)/100 Lime_Fines,
                            :vPSW2*Avg(Wrp_MET)/100 Wrp_MET,
                            :vPSW2*Avg(LD_Slag_Fines)/100 LD_Slag_Fines ,
                            :vPSW2*Avg(MILL_SLUDGE)/100 MILL_SLUDGE 
						    From T_PSW_DAILY where trim(SOURCE)='RMBB_KNR' AND TIMESTAMP>=trunc(:prepEndDate)-200 and BLEND_NO=:BL2)";

                    using (OracleCommand blendCmd = new OracleCommand(blendQuery, conn))
                    {
                        blendCmd.BindByName = true;
                        blendCmd.Parameters.Add(":vPSW1", OracleDbType.Decimal).Value = input.PSW_CONS1 ?? 0;
                        blendCmd.Parameters.Add(":vPSW2", OracleDbType.Decimal).Value = input.PSW_CONS2 ?? 0;
                        blendCmd.Parameters.Add(":prepEndDate", OracleDbType.Date).Value = input.EndDate;
                        //blendCmd.Parameters.Add(":BL1", OracleDbType.Int32).Value = input.PSW_BL1 ?? 0;
                        //blendCmd.Parameters.Add(":BL2", OracleDbType.Int32).Value = input.PSW_BL2 ?? 0;
                        blendCmd.Parameters.Add(":BL1", OracleDbType.Int32).Value =15;
                        blendCmd.Parameters.Add(":BL2", OracleDbType.Int32).Value =0;
                        using (OracleDataReader reader = blendCmd.ExecuteReader())
                        {
                            if (reader.Read())
                            {
                               input.LD_SLUDGE=LD_Sludge_Cons = reader.IsDBNull(0) ? (decimal?)null : reader.GetDecimal(0);
                               input.MILL_SCALE=Mill_Scale_Cons = reader.IsDBNull(1) ? (decimal?)null : reader.GetDecimal(1);
                               input.FLUE_DUST=Flue_Dust_Cons = reader.IsDBNull(2) ? (decimal?)null : reader.GetDecimal(2);
                               input.ESP_DUST=Esp_Dust_Cons = reader.IsDBNull(3) ? (decimal?)null : reader.GetDecimal(3);
                               input.KILN_DUST=Kiln_Dust_Cons = reader.IsDBNull(4) ? (decimal?)null : reader.GetDecimal(4);
                               input.GCP_SLUDGE=Gcp_Sludge_Cons = reader.IsDBNull(5) ? (decimal?)null : reader.GetDecimal(5);
                               input.LIME_FINES=Lime_Fines_Cons = reader.IsDBNull(6) ? (decimal?)null : reader.GetDecimal(6);
                               input.WRP=Wrp_MET_Cons = reader.IsDBNull(7) ? (decimal?)null : reader.GetDecimal(7);
                               input.LD_SLAG_FINES= LD_Slag_Fines_Cons = reader.IsDBNull(8) ? (decimal?)null : reader.GetDecimal(8);
                               input.MILL_SLUDGE=Mill_Sludge_Cons = reader.IsDBNull(9) ? (decimal?)null : reader.GetDecimal(9);
                               input.LD_SLUDGE_PRM=input.LD_SLUDGE;
                               input.FLUE_DUST_PRM = input.FLUE_DUST;
                               input.ESP_DUST_PRM = input.ESP_DUST;
                               input.MILL_SLUDGE_PRM = input.MILL_SLUDGE;
                               input.MILL_SCALE_PRM = input.MILL_SCALE;                              

                            }
                        }
                    }


                    string checkSql = "SELECT COUNT(*) FROM Test.T_PILE_RAWMAT_QUANTITY_NEW WHERE PILE_NO ='" + input.PileNo + "' AND SOURCE ='" + input.Source + "'";
                    using (OracleCommand checkCmd = new OracleCommand(checkSql, conn))
                    {
                        int count = Convert.ToInt32(checkCmd.ExecuteScalar());
                        if (count > 0)
                        {

                            string updateSql = @"UPDATE Test.T_PILE_RAWMAT_QUANTITY_NEW SET                                         
                                        PREP_START_DATE=:PREP_START_DATE,
                                        PREP_END_DATE=:PREP_END_DATE,
                                        CONS_ST_DATE=:CONS_ST_DATE,
                                        NOA_FINES=:NOA_FINES,
                                        JODA_FINES=:JODA_FINES,
                                        KB_FINES=:KB_FINES,
 					                    YARD_FINES=:YARD_FINES,
                                        BHJ=:BHJ,
                                        IO_NAMISA=:IO_NAMISA,
                                        IRON_ORE_NOA_CRUSHED=:IRON_ORE_NOA_CRUSHED ,
                                        IRON_ORE_JODA_CRUSHED=:IRON_ORE_JODA_CRUSHED,
                                        IRON_ORE_KB_CRUSHED=:IRON_ORE_KB_CRUSHED,
                                        IO_PILBHARA=:IO_PILBHARA,
                                        IO_KUMBA=:IO_KUMBA,
                                        IO_COASTAL_FINES=:IO_COASTAL_FINES,
                                        KATAMATI_FINES=:KATAMATI_FINES,
                                        IO_KIRANDUL_SIZE_ORE=:IO_KIRANDUL_SIZE_ORE,
                                        IO_KIRANDUL_FINES=:IO_KIRANDUL_FINES,
                                        IO_FSF_VENEZUELAN=:IO_FSF_VENEZUELAN,
                                        IO_SN_FEED_VALE=:IO_SN_FEED_VALE ,
                                        IO_OTHER_IMP_ORE=:IO_OTHER_IMP_ORE ,
                                        IMP_ORE_FINES=:IMP_ORE_FINES,
                                        DO_BACHELI=:DO_BACHELI ,
                                        DO_JAROLI_FINES=:DO_JAROLI_FINES,
                                        DO_KAY_PEE_ENTERPRISE=:DO_KAY_PEE_ENTERPRISE ,
                                        DO_AHLUWALIA_FINES=:DO_AHLUWALIA_FINES,
                                        DO_DIATARI_FINES=:DO_DIATARI_FINES  ,
                                        DOMESTIC_ORE_FINES=:DOMESTIC_ORE_FINES ,
                                        IO_FINES=:IO_FINES  ,
                                        LS_HI_SILICA=:LS_HI_SILICA,
                                        LS_RPD=:LS_RPD,
                                        LS_SP_GRADE=:LS_SP_GRADE,
                                        LD_SLAG_OS=:LD_SLAG_OS,
                                        SOAP_STONE=:SOAP_STONE,
                                        LS_GOTTAN=:LS_GOTTAN,
                                        LS_IMPORTED=:LS_IMPORTED,
                                        LS_HIMACHAL=:LS_HIMACHAL,
                                        BHUTAN_DOLO=:BHUTAN_DOLO ,
                                        GOMARDIH_DOLO=:GOMARDIH_DOLO,
                                        LS_PHILLIPINES=:LS_PHILLIPINES,
                                        PYROXENITE_LOCAL=:PYROXENITE_LOCAL,
                                        PYROXENITE_IMPORTED=:PYROXENITE_IMPORTED,
                                        MIXED_FLUX=:MIXED_FLUX,
                                        LD_SLUDGE=:LD_SLUDGE,
                                        MILL_SCALE=:MILL_SCALE,
                                        KILN_DUST=:KILN_DUST,
                                        SOLID_WASTE=:SOLID_WASTE,
                                        MILL_SLUDGE=:MILL_SLUDGE,
                                        FLUE_DUST=:FLUE_DUST,
                                        ESP_DUST=:ESP_DUST ,
                                        PSW_CONS1=:PSW_CONS1,
                                        PSW_CONS2=:PSW_CONS2,
                                        PSW_BL2=:PSW_BL2,
                                        GCP_SLUDGE=:GCP_SLUDGE,
                                        LD_SLUDGE_PRM=:LD_SLUDGE_PRM,
                                        LIME_FINES=:LIME_FINES,
                                        LD_SLAG_FINES=:LD_SLAG_FINES,
                                        PSW_BL1=:PSW_BL1,
                                        WRP=:WRP,
                                        DOLO_FINES=:DOLO_FINES,
                                        FLUE_DUST_PRM=:FLUE_DUST_PRM,
                                        MILL_SLUDGE_PRM=:MILL_SLUDGE_PRM,
                                        ESP_DUST_PRM=:ESP_DUST_PRM,
                                        REVERT_MAT=:REVERT_MAT,
                                        LD_SLUDGE_MIX_PRM=:LD_SLUDGE_MIX_PRM,
                                        SOLID_MIX=:SOLID_MIX,
                                        MILL_SCALE_PRM=:MILL_SCALE_PRM,
                                        KILN_DUST_PRM=:KILN_DUST_PRM,
                                        COKE_BREEZE=:COKE_BREEZE,
                                        RPC=:RPC,
                                        JHAMA=:JHAMA,
                                        G_SINTER_FINES=:G_SINTER_FINES,
                                        G_PELLET_FINES=:G_PELLET_FINES,
                                        G_ORE_FINES=:G_ORE_FINES,                                         
  				  	                    BM_END_CONE=:BM_END_CONE,
                                        ANTHRACITE=:ANTHRACITE,
                                        BM_PREVIOUS=:BM_PREVIOUS,
                                        MIXED_MATERIAL=:MIXED_MATERIAL,
                                        TOTAL_PILE=:TOTAL_PILE ,
					                    NO_OF_LAYERS=:NO_OF_LAYERS,
                                        BM_SIO2_PLANT=:BM_SIO2_PLANT,
                                        BM_CAO_PLANT=:BM_CAO_PLANT,
                                        BM_PHOS_PLANT=:BM_PHOS_PLANT,
                                        BM_AL2O3_PLANT=:BM_AL2O3_PLANT,                                                                                
                                        BM_MGO_PLANT=:BM_MGO_PLANT,
                                        BM_C_PLANT=:BM_C_PLANT,
                                        BM_OIL_PLANT=:BM_OIL_PLANT,
                                        BM_FEO_PLANT=:BM_FEO_PLANT,
                                        BM_SIO2_PLANT_LOI=:BM_SIO2_PLANT_LOI,
                                        BM_CAO_PLANT_LOI=:BM_CAO_PLANT_LOI,
                                        BM_PHOS_PLANT_LOI=:BM_PHOS_PLANT_LOI,
                                        BM_AL2O3_PLANT_LOI=:BM_AL2O3_PLANT_LOI,
                                        BM_MGO_PLANT_LOI=:BM_MGO_PLANT_LOI,
                                        BM_C_PLANT_LOI=:BM_C_PLANT_LOI,
                                        BM_OIL_PLANT_LOI=:BM_OIL_PLANT_LOI,
                                        BM_FEO_PLANT_LOI=:BM_FEO_PLANT_LOI                                                                                                                                                          
                                    WHERE PILE_NO ='" + input.PileNo + "' AND SOURCE ='" + input.Source + "'";
                            using (OracleCommand updateCmd = new OracleCommand(updateSql, conn))
                            {
                                updateCmd.Parameters.Add(":PREP_START_DATE", OracleDbType.Date).Value = input.StartDate ?? (object)DBNull.Value; 
                                updateCmd.Parameters.Add(":PREP_END_DATE", OracleDbType.Date).Value = input.EndDate ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":CONS_ST_DATE", OracleDbType.Date).Value = input.ConsStartDate ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":NOA_FINES", OracleDbType.Decimal).Value = input.NOA_FINES ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":JODA_FINES", OracleDbType.Decimal).Value = input.JODA_FINES ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":KB_FINES", OracleDbType.Decimal).Value = input.KB_FINES ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":YARD_FINES", OracleDbType.Decimal).Value = input.YARD_FINES ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":BHJ", OracleDbType.Decimal).Value = input.TXT_BHJ ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":IO_NAMISA", OracleDbType.Decimal).Value = input.IO_NAMISA ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":IRON_ORE_NOA_CRUSHED", OracleDbType.Decimal).Value = input.IRON_ORE_NOA_CRUSHED ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":IRON_ORE_JODA_CRUSHED", OracleDbType.Decimal).Value = input.IRON_ORE_JODA_CRUSHED ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":IRON_ORE_KB_CRUSHED", OracleDbType.Decimal).Value = input.IRON_ORE_KB_CRUSHED ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":IO_PILBHARA", OracleDbType.Decimal).Value = input.IO_PILBHARA ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":IO_KUMBA", OracleDbType.Decimal).Value = input.IO_KUMBA ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":IO_COASTAL_FINES", OracleDbType.Decimal).Value = input.IO_COASTAL_FINES ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":KATAMATI_FINES", OracleDbType.Decimal).Value = input.KATAMATI_FINES ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":IO_KIRANDUL_SIZE_ORE", OracleDbType.Decimal).Value = input.IO_KIRANDUL_SIZE_ORE ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":IO_KIRANDUL_FINES", OracleDbType.Decimal).Value = input.IO_KIRANDUL_FINES ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":IO_FSF_VENEZUELAN", OracleDbType.Decimal).Value = input.IO_FSF_VENEZUELAN ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":IO_SN_FEED_VALE", OracleDbType.Decimal).Value = input.IO_SN_FEED_VALE ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":IO_OTHER_IMP_ORE", OracleDbType.Decimal).Value = input.IO_OTHER_IMP_ORE ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":IMP_ORE_FINES", OracleDbType.Decimal).Value = input.TXT_IMP_ORE_FINES ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":DO_BACHELI", OracleDbType.Decimal).Value = input.DO_BACHELI ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":DO_JAROLI_FINES", OracleDbType.Decimal).Value = input.DO_JAROLI_FINES ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":DO_KAY_PEE_ENTERPRISE", OracleDbType.Decimal).Value = input.DO_KAY_PEE_ENTERPRISE ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":DO_AHLUWALIA_FINES", OracleDbType.Decimal).Value = input.DO_AHLUWALIA_FINES ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":DO_DIATARI_FINES", OracleDbType.Decimal).Value = input.DO_DIATARI_FINES ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":DOMESTIC_ORE_FINES", OracleDbType.Decimal).Value = input.TXT_DOMESTIC_ORE_FINES ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":IO_FINES", OracleDbType.Decimal).Value = input.IO_FINES ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":LS_HI_SILICA", OracleDbType.Decimal).Value = input.LS_HI_SILICA ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":LS_RPD", OracleDbType.Decimal).Value = input.LS_RPD ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":LS_SP_GRADE", OracleDbType.Decimal).Value = input.LS_SP_GRADE ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":LD_SLAG_OS", OracleDbType.Decimal).Value = input.LD_SLAG_OS ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":SOAP_STONE", OracleDbType.Decimal).Value = input.SOAP_STONE ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":LS_GOTTAN", OracleDbType.Decimal).Value = input.LS_GOTTAN ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":LS_IMPORTED", OracleDbType.Decimal).Value = input.LIME_STONE_IMP ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":LS_HIMACHAL", OracleDbType.Decimal).Value = input.LS_HIMACHAL ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":BHUTAN_DOLO", OracleDbType.Decimal).Value = input.BHUTAN_DOLO ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":GOMARDIH_DOLO", OracleDbType.Decimal).Value = input.GOMARDIH_DOLO ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":LS_PHILLIPINES", OracleDbType.Decimal).Value = input.LS_PHILLIPINES ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":PYROXENITE_LOCAL", OracleDbType.Decimal).Value = input.PYROXENITE_LOCAL ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":PYROXENITE_IMPORTED", OracleDbType.Decimal).Value = input.PYROXENITE_IMPORTED ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":MIXED_FLUX", OracleDbType.Decimal).Value = input.MIXED_FLUX ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":LD_SLUDGE", OracleDbType.Decimal).Value = input.LD_SLUDGE ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":MILL_SCALE", OracleDbType.Decimal).Value = input.MILL_SCALE ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":KILN_DUST", OracleDbType.Decimal).Value = input.KILN_DUST ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":SOLID_WASTE", OracleDbType.Decimal).Value = input.SOLID_WASTE ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":MILL_SLUDGE", OracleDbType.Decimal).Value = input.MILL_SLUDGE ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":FLUE_DUST", OracleDbType.Decimal).Value = input.FLUE_DUST ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":ESP_DUST", OracleDbType.Decimal).Value = input.ESP_DUST ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":PSW_CONS1", OracleDbType.Decimal).Value = input.PSW_CONS1 ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":PSW_CONS2", OracleDbType.Decimal).Value = input.PSW_CONS2 ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":PSW_BL2", OracleDbType.Decimal).Value = input.PSW_BL2 ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":GCP_SLUDGE", OracleDbType.Decimal).Value = input.GCP_SLUDGE ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":LD_SLUDGE_PRM", OracleDbType.Decimal).Value = input.LD_SLUDGE_PRM ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":LIME_FINES", OracleDbType.Decimal).Value = input.LIME_FINES ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":LD_SLAG_FINES", OracleDbType.Decimal).Value = input.LD_SLAG_FINES ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":PSW_BL1", OracleDbType.Decimal).Value = input.PSW_BL1 ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":WRP", OracleDbType.Decimal).Value = input.WRP ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":DOLO_FINES", OracleDbType.Decimal).Value = input.DOLO_FINES ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":FLUE_DUST_PRM", OracleDbType.Decimal).Value = input.FLUE_DUST_PRM ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":MILL_SLUDGE_PRM", OracleDbType.Decimal).Value = input.MILL_SLUDGE_PRM ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":ESP_DUST_PRM", OracleDbType.Decimal).Value = input.ESP_DUST_PRM ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":REVERT_MAT", OracleDbType.Decimal).Value = input.REVERT_MAT ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":LD_SLUDGE_MIX_PRM", OracleDbType.Decimal).Value = input.LD_SLUDGE_MIX_PRM ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":SOLID_MIX", OracleDbType.Decimal).Value = input.SOLID_MIX ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":MILL_SCALE_PRM", OracleDbType.Decimal).Value = input.MILL_SCALE_PRM ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":KILN_DUST_PRM", OracleDbType.Decimal).Value = input.KILN_DUST_PRM ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":COKE_BREEZE", OracleDbType.Decimal).Value = input.COKE_BREEZE ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":RPC", OracleDbType.Decimal).Value = input.RPC ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":JHAMA", OracleDbType.Decimal).Value = input.JHAMA ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":G_SINTER_FINES", OracleDbType.Decimal).Value = input.G_SINTER_FINES ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":G_PELLET_FINES", OracleDbType.Decimal).Value = input.G_PELLET_FINES ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":G_ORE_FINES", OracleDbType.Decimal).Value = input.G_ORE_FINES ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":BM_END_CONE", OracleDbType.Decimal).Value = input.BM_END_CONE ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":ANTHRACITE", OracleDbType.Decimal).Value = input.ANTHRACITE ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":BM_PREVIOUS", OracleDbType.Decimal).Value = input.BM_PREVIOUS ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":MIXED_MATERIAL", OracleDbType.Decimal).Value = input.MIXED_MATERIAL ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":TOTAL_PILE", OracleDbType.Decimal).Value = input.TOTAL_PILE ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":NO_OF_LAYERS", OracleDbType.Decimal).Value = input.NO_OF_LAYERS ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":BM_SIO2_PLANT", OracleDbType.Decimal).Value = input.BM_SIO2_PLANT ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":BM_CAO_PLANT", OracleDbType.Decimal).Value = input.BM_CAO_PLANT ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":BM_PHOS_PLANT", OracleDbType.Decimal).Value = input.BM_PHOS_PLANT ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":BM_AL2O3_PLANT", OracleDbType.Decimal).Value = input.BM_AL2O3_PLANT ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":BM_MGO_PLANT", OracleDbType.Decimal).Value = input.BM_MGO_PLANT ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":BM_C_PLANT", OracleDbType.Decimal).Value = input.BM_C_PLANT ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":BM_OIL_PLANT", OracleDbType.Decimal).Value = input.BM_OIL_PLANT ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":BM_FEO_PLANT", OracleDbType.Decimal).Value = input.BM_FEO_PLANT ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":BM_SIO2_PLANT_LOI", OracleDbType.Decimal).Value = input.BM_SIO2_PLANT_LOI ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":BM_CAO_PLANT_LOI", OracleDbType.Decimal).Value = input.BM_CAO_PLANT_LOI ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":BM_PHOS_PLANT_LOI", OracleDbType.Decimal).Value = input.BM_PHOS_PLANT_LOI ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":BM_AL2O3_PLANT_LOI", OracleDbType.Decimal).Value = input.BM_AL2O3_PLANT_LOI ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":BM_MGO_PLANT_LOI", OracleDbType.Decimal).Value = input.BM_MGO_PLANT_LOI ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":BM_C_PLANT_LOI", OracleDbType.Decimal).Value = input.BM_C_PLANT_LOI ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":BM_OIL_PLANT_LOI", OracleDbType.Decimal).Value = input.BM_OIL_PLANT_LOI ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":BM_FEO_PLANT_LOI", OracleDbType.Decimal).Value = input.BM_FEO_PLANT_LOI ?? (object)DBNull.Value;
                                updateCmd.ExecuteNonQuery();
                                message = "Record Updated Successfully!";
                            }
                        }
                        else
                        {

                            string insertSql = @"INSERT INTO Test.T_PILE_RAWMAT_QUANTITY_NEW
                            (PILE_NO,SOURCE,PREP_START_DATE,PREP_END_DATE,CONS_ST_DATE,NOA_FINES,
                            JODA_FINES,KB_FINES,YARD_FINES,BHJ,IO_NAMISA,IRON_ORE_NOA_CRUSHED,IRON_ORE_JODA_CRUSHED,
                            IRON_ORE_KB_CRUSHED,IO_PILBHARA,IO_KUMBA,IO_COASTAL_FINES,KATAMATI_FINES,IO_KIRANDUL_SIZE_ORE,IO_KIRANDUL_FINES,IO_FSF_VENEZUELAN,IO_SN_FEED_VALE,IO_OTHER_IMP_ORE,IMP_ORE_FINES,DO_BACHELI,DO_JAROLI_FINES,
                            DO_KAY_PEE_ENTERPRISE,DO_AHLUWALIA_FINES,DO_DIATARI_FINES,DOMESTIC_ORE_FINES,IO_FINES,LS_HI_SILICA,LS_RPD,LS_SP_GRADE,LD_SLAG_OS,SOAP_STONE,LS_GOTTAN,LS_IMPORTED,LS_HIMACHAL,
                            BHUTAN_DOLO,GOMARDIH_DOLO,LS_PHILLIPINES,PYROXENITE_LOCAL,PYROXENITE_IMPORTED,MIXED_FLUX,LD_SLUDGE,MILL_SCALE,KILN_DUST,SOLID_WASTE,MILL_SLUDGE,FLUE_DUST,ESP_DUST,PSW_CONS1,PSW_CONS2,
                            PSW_BL2,GCP_SLUDGE,LD_SLUDGE_PRM,LIME_FINES,LD_SLAG_FINES,PSW_BL1,WRP,DOLO_FINES,FLUE_DUST_PRM,MILL_SLUDGE_PRM,ESP_DUST_PRM,REVERT_MAT,LD_SLUDGE_MIX_PRM,SOLID_MIX,MILL_SCALE_PRM,
                            KILN_DUST_PRM,COKE_BREEZE,RPC,JHAMA,G_SINTER_FINES,G_PELLET_FINES,G_ORE_FINES,ANTHRACITE,BM_PREVIOUS,MIXED_MATERIAL,TOTAL_PILE,BM_SIO2_PLANT,BM_CAO_PLANT,BM_PHOS_PLANT,BM_AL2O3_PLANT,
                            BM_MGO_PLANT,BM_C_PLANT,BM_OIL_PLANT,BM_FEO_PLANT,BM_SIO2_PLANT_LOI,BM_CAO_PLANT_LOI,BM_PHOS_PLANT_LOI,BM_AL2O3_PLANT_LOI,BM_MGO_PLANT_LOI,BM_C_PLANT_LOI,BM_OIL_PLANT_LOI,BM_FEO_PLANT_LOI,NO_OF_LAYERS) 
                            values(:PILE_NO,:SOURCE,:PREP_START_DATE,:PREP_END_DATE,:CONS_ST_DATE,:NOA_FINES,
                            :JODA_FINES,:KB_FINES,:YARD_FINES,:BHJ,:IO_NAMISA,:IRON_ORE_NOA_CRUSHED,:IRON_ORE_JODA_CRUSHED,
                            :IRON_ORE_KB_CRUSHED,:IO_PILBHARA,:IO_KUMBA,:IO_COASTAL_FINES,:KATAMATI_FINES,:IO_KIRANDUL_SIZE_ORE,:IO_KIRANDUL_FINES,:IO_FSF_VENEZUELAN,:IO_SN_FEED_VALE,:IO_OTHER_IMP_ORE,:IMP_ORE_FINES,
                            :DO_BACHELI,:DO_JAROLI_FINES,:DO_KAY_PEE_ENTERPRISE,:DO_AHLUWALIA_FINES,:DO_DIATARI_FINES,:DOMESTIC_ORE_FINES,:IO_FINES,:LS_HI_SILICA,:LS_RPD,:LS_SP_GRADE,:LD_SLAG_OS,
                            :SOAP_STONE,:LS_GOTTAN,:LS_IMPORTED,:LS_HIMACHAL,:BHUTAN_DOLO,:GOMARDIH_DOLO,:LS_PHILLIPINES,:PYROXENITE_LOCAL,:PYROXENITE_IMPORTED,:MIXED_FLUX,:LD_SLUDGE,:MILL_SCALE,
                            :KILN_DUST,:SOLID_WASTE,:MILL_SLUDGE,:FLUE_DUST,:ESP_DUST,:PSW_CONS1,:PSW_CONS2,:PSW_BL2,:GCP_SLUDGE,:LD_SLUDGE_PRM,:LIME_FINES,:LD_SLAG_FINES,:PSW_BL1,:WRP,:DOLO_FINES,
                            :FLUE_DUST_PRM,:MILL_SLUDGE_PRM,:ESP_DUST_PRM,:REVERT_MAT,:LD_SLUDGE_MIX_PRM,:SOLID_MIX,:MILL_SCALE_PRM,:KILN_DUST_PRM,:COKE_BREEZE,:RPC,:JHAMA,:G_SINTER_FINES,
                            :G_PELLET_FINES,:G_ORE_FINES,:ANTHRACITE,:BM_PREVIOUS,:MIXED_MATERIAL,:TOTAL_PILE,:BM_SIO2_PLANT,:BM_CAO_PLANT,:BM_PHOS_PLANT,:BM_AL2O3_PLANT,:BM_MGO_PLANT,:BM_C_PLANT,
                            :BM_OIL_PLANT,:BM_FEO_PLANT,:BM_SIO2_PLANT_LOI,:BM_CAO_PLANT_LOI,:BM_PHOS_PLANT_LOI,:BM_AL2O3_PLANT_LOI,:BM_MGO_PLANT_LOI,:BM_C_PLANT_LOI,:BM_OIL_PLANT_LOI,:BM_FEO_PLANT_LOI,:NO_OF_LAYERS)";
                            using (OracleCommand insertCmd = new OracleCommand(insertSql, conn))
                            {
                                insertCmd.Parameters.Add("PILE_NO", OracleDbType.Varchar2).Value = input.PileNo ?? "";
                                insertCmd.Parameters.Add("SOURCE", OracleDbType.Varchar2).Value = input.Source ?? "";                                
                                insertCmd.Parameters.Add("PREP_START_DATE", OracleDbType.Date).Value = input.StartDate ?? (object)DBNull.Value; 
                                insertCmd.Parameters.Add("PREP_END_DATE", OracleDbType.Date).Value = input.EndDate ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("CONS_ST_DATE", OracleDbType.Date).Value = input.ConsStartDate ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("NOA_FINES", OracleDbType.Decimal).Value = input.NOA_FINES ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("JODA_FINES", OracleDbType.Decimal).Value = input.JODA_FINES ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("KB_FINES", OracleDbType.Decimal).Value = input.KB_FINES ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("YARD_FINES", OracleDbType.Decimal).Value = input.YARD_FINES ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("BHJ", OracleDbType.Decimal).Value = input.TXT_BHJ ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("IO_NAMISA", OracleDbType.Decimal).Value = input.IO_NAMISA ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("IRON_ORE_NOA_CRUSHED", OracleDbType.Decimal).Value = input.IRON_ORE_NOA_CRUSHED ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("IRON_ORE_JODA_CRUSHED", OracleDbType.Decimal).Value = input.IRON_ORE_JODA_CRUSHED ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("IRON_ORE_KB_CRUSHED", OracleDbType.Decimal).Value = input.IRON_ORE_KB_CRUSHED ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("IO_PILBHARA", OracleDbType.Decimal).Value = input.IO_PILBHARA ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("IO_KUMBA", OracleDbType.Decimal).Value = input.IO_KUMBA ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("IO_COASTAL_FINES", OracleDbType.Decimal).Value = input.IO_COASTAL_FINES ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("KATAMATI_FINES", OracleDbType.Decimal).Value = input.KATAMATI_FINES ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("IO_KIRANDUL_SIZE_ORE", OracleDbType.Decimal).Value = input.IO_KIRANDUL_SIZE_ORE ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("IO_KIRANDUL_FINES", OracleDbType.Decimal).Value = input.IO_KIRANDUL_FINES ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("IO_FSF_VENEZUELAN", OracleDbType.Decimal).Value = input.IO_FSF_VENEZUELAN ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("IO_SN_FEED_VALE", OracleDbType.Decimal).Value = input.IO_SN_FEED_VALE ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("IO_OTHER_IMP_ORE", OracleDbType.Decimal).Value = input.IO_OTHER_IMP_ORE ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("IMP_ORE_FINES", OracleDbType.Decimal).Value = input.TXT_IMP_ORE_FINES ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("DO_BACHELI", OracleDbType.Decimal).Value = input.DO_BACHELI ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("DO_JAROLI_FINES", OracleDbType.Decimal).Value = input.DO_JAROLI_FINES ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("DO_KAY_PEE_ENTERPRISE", OracleDbType.Decimal).Value = input.DO_KAY_PEE_ENTERPRISE ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("DO_AHLUWALIA_FINES", OracleDbType.Decimal).Value = input.DO_AHLUWALIA_FINES ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("DO_DIATARI_FINES", OracleDbType.Decimal).Value = input.DO_DIATARI_FINES ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("DOMESTIC_ORE_FINES", OracleDbType.Decimal).Value = input.TXT_DOMESTIC_ORE_FINES ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("IO_FINES", OracleDbType.Decimal).Value = input.IO_FINES ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("LS_HI_SILICA", OracleDbType.Decimal).Value = input.LS_HI_SILICA ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("LS_RPD", OracleDbType.Decimal).Value = input.LS_RPD ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("LS_SP_GRADE", OracleDbType.Decimal).Value = input.LS_SP_GRADE ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("LD_SLAG_OS", OracleDbType.Decimal).Value = input.LD_SLAG_OS ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("SOAP_STONE", OracleDbType.Decimal).Value = input.SOAP_STONE ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("LS_GOTTAN", OracleDbType.Decimal).Value = input.LS_GOTTAN ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("LS_IMPORTED", OracleDbType.Decimal).Value = input.LIME_STONE_IMP ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("LS_HIMACHAL", OracleDbType.Decimal).Value = input.LS_HIMACHAL ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("BHUTAN_DOLO", OracleDbType.Decimal).Value = input.BHUTAN_DOLO ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("GOMARDIH_DOLO", OracleDbType.Decimal).Value = input.GOMARDIH_DOLO ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("LS_PHILLIPINES", OracleDbType.Decimal).Value = input.LS_PHILLIPINES ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("PYROXENITE_LOCAL", OracleDbType.Decimal).Value = input.PYROXENITE_LOCAL ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("PYROXENITE_IMPORTED", OracleDbType.Decimal).Value = input.PYROXENITE_IMPORTED ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("MIXED_FLUX", OracleDbType.Decimal).Value = input.MIXED_FLUX ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("LD_SLUDGE", OracleDbType.Decimal).Value = input.LD_SLUDGE ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("MILL_SCALE", OracleDbType.Decimal).Value = input.MILL_SCALE ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("KILN_DUST", OracleDbType.Decimal).Value = input.KILN_DUST ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("SOLID_WASTE", OracleDbType.Decimal).Value = input.SOLID_WASTE ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("MILL_SLUDGE", OracleDbType.Decimal).Value = input.MILL_SLUDGE ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("FLUE_DUST", OracleDbType.Decimal).Value = input.FLUE_DUST ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("ESP_DUST", OracleDbType.Decimal).Value = input.ESP_DUST ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("PSW_CONS1", OracleDbType.Decimal).Value = input.PSW_CONS1 ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("PSW_CONS2", OracleDbType.Decimal).Value = input.PSW_CONS2 ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("PSW_BL2", OracleDbType.Decimal).Value = input.PSW_BL2 ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("GCP_SLUDGE", OracleDbType.Decimal).Value = input.GCP_SLUDGE ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("LD_SLUDGE_PRM", OracleDbType.Decimal).Value = input.LD_SLUDGE_PRM ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("LIME_FINES", OracleDbType.Decimal).Value = input.LIME_FINES ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("LD_SLAG_FINES", OracleDbType.Decimal).Value = input.LD_SLAG_FINES ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("PSW_BL1", OracleDbType.Decimal).Value = input.PSW_BL1 ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("WRP", OracleDbType.Decimal).Value = input.WRP ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("DOLO_FINES", OracleDbType.Decimal).Value = input.DOLO_FINES ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("FLUE_DUST_PRM", OracleDbType.Decimal).Value = input.FLUE_DUST_PRM ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("MILL_SLUDGE_PRM", OracleDbType.Decimal).Value = input.MILL_SLUDGE_PRM ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("ESP_DUST_PRM", OracleDbType.Decimal).Value = input.ESP_DUST_PRM ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("REVERT_MAT", OracleDbType.Decimal).Value = input.REVERT_MAT ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("LD_SLUDGE_MIX_PRM", OracleDbType.Decimal).Value = input.LD_SLUDGE_MIX_PRM ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("SOLID_MIX", OracleDbType.Decimal).Value = input.SOLID_MIX ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("MILL_SCALE_PRM", OracleDbType.Decimal).Value = input.MILL_SCALE_PRM ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("KILN_DUST_PRM", OracleDbType.Decimal).Value = input.KILN_DUST_PRM ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("COKE_BREEZE", OracleDbType.Decimal).Value = input.COKE_BREEZE ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("RPC", OracleDbType.Decimal).Value = input.RPC ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("JHAMA", OracleDbType.Decimal).Value = input.JHAMA ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("G_SINTER_FINES", OracleDbType.Decimal).Value = input.G_SINTER_FINES ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("G_PELLET_FINES", OracleDbType.Decimal).Value = input.G_PELLET_FINES ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("G_ORE_FINES", OracleDbType.Decimal).Value = input.G_ORE_FINES ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("ANTHRACITE", OracleDbType.Decimal).Value = input.ANTHRACITE ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("BM_PREVIOUS", OracleDbType.Decimal).Value = input.BM_PREVIOUS ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("MIXED_MATERIAL", OracleDbType.Decimal).Value = input.MIXED_MATERIAL ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("TOTAL_PILE", OracleDbType.Decimal).Value = input.TOTAL_PILE ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("BM_SIO2_PLANT", OracleDbType.Decimal).Value = input.BM_SIO2_PLANT ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("BM_CAO_PLANT", OracleDbType.Decimal).Value = input.BM_CAO_PLANT ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("BM_PHOS_PLANT", OracleDbType.Decimal).Value = input.BM_PHOS_PLANT ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("BM_AL2O3_PLANT", OracleDbType.Decimal).Value = input.BM_AL2O3_PLANT ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("BM_MGO_PLANT", OracleDbType.Decimal).Value = input.BM_MGO_PLANT ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("BM_C_PLANT", OracleDbType.Decimal).Value = input.BM_C_PLANT ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("BM_OIL_PLANT", OracleDbType.Decimal).Value = input.BM_OIL_PLANT ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("BM_FEO_PLANT", OracleDbType.Decimal).Value = input.BM_FEO_PLANT ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("BM_SIO2_PLANT_LOI", OracleDbType.Decimal).Value = input.BM_SIO2_PLANT_LOI ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("BM_CAO_PLANT_LOI", OracleDbType.Decimal).Value = input.BM_CAO_PLANT_LOI ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("BM_PHOS_PLANT_LOI", OracleDbType.Decimal).Value = input.BM_PHOS_PLANT_LOI ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("BM_AL2O3_PLANT_LOI", OracleDbType.Decimal).Value = input.BM_AL2O3_PLANT_LOI ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("BM_MGO_PLANT_LOI", OracleDbType.Decimal).Value = input.BM_MGO_PLANT_LOI ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("BM_C_PLANT_LOI", OracleDbType.Decimal).Value = input.BM_C_PLANT_LOI ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("BM_OIL_PLANT_LOI", OracleDbType.Decimal).Value = input.BM_OIL_PLANT_LOI ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("BM_FEO_PLANT_LOI", OracleDbType.Decimal).Value = input.BM_FEO_PLANT_LOI ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("NO_OF_LAYERS", OracleDbType.Decimal).Value = input.NO_OF_LAYERS ?? (object)DBNull.Value;                                
                                insertCmd.ExecuteNonQuery();
                                ViewBag.Message = "Data Inserted Successfully!";
                            }
                        }
                    }
                }

               
                model = input;
            }

            else if (!string.IsNullOrEmpty(input.PileNo) && !string.IsNullOrEmpty(input.Source))
            {                
                using (OracleConnection conn = new OracleConnection(iMonitorWebUtils.msConRWString))
                {
                    conn.Open();
                    string query = "SELECT * FROM Test.T_PILE_RAWMAT_QUANTITY_NEW  WHERE PILE_NO ='" + input.PileNo + "' AND SOURCE ='" + input.Source + "'";
                    using (OracleCommand cmd = new OracleCommand(query, conn))
                    {

                        using (OracleDataReader reader = cmd.ExecuteReader())
                        {
                            if (reader.Read())
                            {
                                recordFound = true;
                                model.PileNo = input.PileNo;
                                model.Source = input.Source;
                                model.StartDate = reader["PREP_START_DATE"] == DBNull.Value ? (DateTime?)null : Convert.ToDateTime(reader["PREP_START_DATE"]);
                                model.EndDate = reader["PREP_END_DATE"] == DBNull.Value ? (DateTime?)null : Convert.ToDateTime(reader["PREP_END_DATE"]);
                                model.ConsStartDate = reader["CONS_ST_DATE"] == DBNull.Value ? (DateTime?)null : Convert.ToDateTime(reader["CONS_ST_DATE"]);
                                model.NOA_FINES = reader["NOA_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["NOA_FINES"]);
                                model.JODA_FINES = reader["JODA_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["JODA_FINES"]);
                                model.KB_FINES = reader["KB_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["KB_FINES"]);
                                model.YARD_FINES = reader["YARD_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["YARD_FINES"]);
                                model.TXT_BHJ = reader["BHJ"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["BHJ"]);
                                model.IO_NAMISA = reader["IO_NAMISA"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["IO_NAMISA"]);
                                model.IO_FORTESCUE_BF = reader["IO_FORTESCUE_BF"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["IO_FORTESCUE_BF"]);
                                model.IRON_ORE_NOA_CRUSHED = reader["IRON_ORE_NOA_CRUSHED"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["IRON_ORE_NOA_CRUSHED"]);
                                model.IRON_ORE_JODA_CRUSHED = reader["IRON_ORE_JODA_CRUSHED"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["IRON_ORE_JODA_CRUSHED"]);
                                model.IRON_ORE_KB_CRUSHED = reader["IRON_ORE_KB_CRUSHED"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["IRON_ORE_KB_CRUSHED"]);
                                model.IO_PILBHARA = reader["IO_PILBHARA"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["IO_PILBHARA"]);
                                model.IO_KUMBA = reader["IO_KUMBA"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["IO_KUMBA"]);
                                model.IO_COASTAL_FINES = reader["IO_COASTAL_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["IO_COASTAL_FINES"]);
                                model.KATAMATI_FINES = reader["KATAMATI_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["KATAMATI_FINES"]);
                                model.IO_KIRANDUL_SIZE_ORE = reader["IO_KIRANDUL_SIZE_ORE"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["IO_KIRANDUL_SIZE_ORE"]);
                                model.IO_KIRANDUL_FINES = reader["IO_KIRANDUL_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["IO_KIRANDUL_FINES"]);
                                model.IO_FSF_VENEZUELAN = reader["IO_FSF_VENEZUELAN"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["IO_FSF_VENEZUELAN"]);
                                model.IO_SN_FEED_VALE = reader["IO_SN_FEED_VALE"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["IO_SN_FEED_VALE"]);
                                model.IO_OTHER_IMP_ORE = reader["IO_OTHER_IMP_ORE"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["IO_OTHER_IMP_ORE"]);
                                model.TXT_IMP_ORE_FINES = reader["IMP_ORE_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["IMP_ORE_FINES"]);
                                model.DO_BACHELI = reader["DO_BACHELI"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["DO_BACHELI"]);
                                model.DO_JAROLI_FINES = reader["DO_JAROLI_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["DO_JAROLI_FINES"]);
                                model.DO_KAY_PEE_ENTERPRISE = reader["DO_KAY_PEE_ENTERPRISE"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["DO_KAY_PEE_ENTERPRISE"]);
                                model.DO_AHLUWALIA_FINES = reader["DO_AHLUWALIA_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["DO_AHLUWALIA_FINES"]);
                                model.DO_DIATARI_FINES = reader["DO_DIATARI_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["DO_DIATARI_FINES"]);
                                model.TXT_DOMESTIC_ORE_FINES = reader["DOMESTIC_ORE_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["DOMESTIC_ORE_FINES"]);
                                model.IO_FINES = reader["IO_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["IO_FINES"]);
                                model.LS_HI_SILICA = reader["LS_HI_SILICA"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["LS_HI_SILICA"]);
                                model.LS_RPD = reader["LS_RPD"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["LS_RPD"]);
                                model.LS_SP_GRADE = reader["LS_SP_GRADE"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["LS_SP_GRADE"]);
                                model.LD_SLAG_OS = reader["LD_SLAG_OS"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["LD_SLAG_OS"]);
                                model.SOAP_STONE = reader["SOAP_STONE"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["SOAP_STONE"]);
                                model.LS_GOTTAN = reader["LS_GOTTAN"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["LS_GOTTAN"]);
                                model.LIME_STONE_IMP = reader["LS_IMPORTED"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["LS_IMPORTED"]);
                                model.LS_HIMACHAL = reader["LS_HIMACHAL"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["LS_HIMACHAL"]);
                                model.BHUTAN_DOLO = reader["BHUTAN_DOLO"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["BHUTAN_DOLO"]);
                                model.GOMARDIH_DOLO = reader["GOMARDIH_DOLO"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["GOMARDIH_DOLO"]);
                                model.LS_PHILLIPINES = reader["LS_PHILLIPINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["LS_PHILLIPINES"]);
                                model.PYROXENITE_LOCAL = reader["PYROXENITE_LOCAL"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["PYROXENITE_LOCAL"]);
                                model.PYROXENITE_IMPORTED = reader["PYROXENITE_IMPORTED"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["PYROXENITE_IMPORTED"]);
                                model.MIXED_FLUX = reader["MIXED_FLUX"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["MIXED_FLUX"]);
                                model.LD_SLUDGE = reader["LD_SLUDGE"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["LD_SLUDGE"]);
                                model.MILL_SCALE = reader["MILL_SCALE"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["MILL_SCALE"]);
                                model.KILN_DUST = reader["KILN_DUST"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["KILN_DUST"]);
                                model.SOLID_WASTE = reader["SOLID_WASTE"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["SOLID_WASTE"]);
                                model.MILL_SLUDGE = reader["MILL_SLUDGE"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["MILL_SLUDGE"]);
                                model.FLUE_DUST = reader["FLUE_DUST"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["FLUE_DUST"]);
                                model.ESP_DUST = reader["ESP_DUST"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["ESP_DUST"]);
                                model.PSW_CONS1 = reader["PSW_CONS1"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["PSW_CONS1"]);
                                model.PSW_CONS2 = reader["PSW_CONS2"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["PSW_CONS2"]);
                                //model.PSW_BL1 = reader["PSW_BL1"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["PSW_BL1"]);
                                //model.PSW_BL2 = reader["PSW_BL2"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["PSW_BL2"]);
                                model.GCP_SLUDGE = reader["GCP_SLUDGE"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["GCP_SLUDGE"]);
                                model.LD_SLUDGE_PRM = reader["LD_SLUDGE_PRM"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["LD_SLUDGE_PRM"]);
                                model.LIME_FINES = reader["LIME_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["LIME_FINES"]);
                                model.LD_SLAG_FINES = reader["LD_SLAG_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["LD_SLAG_FINES"]);
                                model.WRP = reader["WRP"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["WRP"]);
                                model.DOLO_FINES = reader["DOLO_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["DOLO_FINES"]);
                                model.FLUE_DUST_PRM = reader["FLUE_DUST_PRM"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["FLUE_DUST_PRM"]);
                                model.MILL_SLUDGE_PRM = reader["MILL_SLUDGE_PRM"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["MILL_SLUDGE_PRM"]);
                                model.ESP_DUST_PRM = reader["ESP_DUST_PRM"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["ESP_DUST_PRM"]);
                                model.REVERT_MAT = reader["REVERT_MAT"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["REVERT_MAT"]);
                                model.LD_SLUDGE_MIX_PRM = reader["LD_SLUDGE_MIX_PRM"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["LD_SLUDGE_MIX_PRM"]);
                                model.SOLID_MIX = reader["SOLID_MIX"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["SOLID_MIX"]);
                                model.MILL_SCALE_PRM = reader["MILL_SCALE_PRM"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["MILL_SCALE_PRM"]);
                                model.KILN_DUST_PRM = reader["KILN_DUST_PRM"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["KILN_DUST_PRM"]);
                                model.COKE_BREEZE = reader["COKE_BREEZE"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["COKE_BREEZE"]);
                                model.RPC = reader["RPC"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["RPC"]);
                                model.JHAMA = reader["JHAMA"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["JHAMA"]);
                                model.G_SINTER_FINES = reader["G_SINTER_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["G_SINTER_FINES"]);
                                model.G_PELLET_FINES = reader["G_PELLET_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["G_PELLET_FINES"]);
                                model.G_ORE_FINES = reader["G_ORE_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["G_ORE_FINES"]);
                                model.BM_END_CONE = reader["BM_END_CONE"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["BM_END_CONE"]);
                                model.ANTHRACITE = reader["ANTHRACITE"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["ANTHRACITE"]);
                                model.BM_PREVIOUS = reader["BM_PREVIOUS"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["BM_PREVIOUS"]);
                                model.MIXED_MATERIAL = reader["MIXED_MATERIAL"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["MIXED_MATERIAL"]);
                                model.BM_SIO2_PLANT = reader["BM_SIO2_PLANT"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["BM_SIO2_PLANT"]);
                                model.BM_CAO_PLANT = reader["BM_CAO_PLANT"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["BM_CAO_PLANT"]);
                                model.BM_PHOS_PLANT = reader["BM_PHOS_PLANT"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["BM_PHOS_PLANT"]);
                                model.BM_AL2O3_PLANT = reader["BM_AL2O3_PLANT"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["BM_AL2O3_PLANT"]);
                                model.TOTAL_PILE = reader["TOTAL_PILE"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["TOTAL_PILE"]);
                                model.NO_OF_LAYERS = reader["NO_OF_LAYERS"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["NO_OF_LAYERS"]);
                                model.BM_MGO_PLANT = reader["BM_MGO_PLANT"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["BM_MGO_PLANT"]);
                                model.BM_C_PLANT = reader["BM_C_PLANT"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["BM_C_PLANT"]);
                                model.BM_OIL_PLANT = reader["BM_OIL_PLANT"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["BM_OIL_PLANT"]);
                                model.BM_FEO_PLANT = reader["BM_FEO_PLANT"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["BM_FEO_PLANT"]);
                                model.BM_SIO2_PLANT_LOI = reader["BM_SIO2_PLANT_LOI"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["BM_SIO2_PLANT_LOI"]);
                                model.BM_CAO_PLANT_LOI = reader["BM_CAO_PLANT_LOI"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["BM_CAO_PLANT_LOI"]);
                                model.BM_PHOS_PLANT_LOI = reader["BM_PHOS_PLANT_LOI"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["BM_PHOS_PLANT_LOI"]);
                                model.BM_AL2O3_PLANT_LOI = reader["BM_AL2O3_PLANT_LOI"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["BM_Al2O3_PLANT_LOI"]);
                                model.BM_MGO_PLANT_LOI = reader["BM_Mgo_PLANT_LOI"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["BM_Mgo_PLANT_LOI"]);
                                model.BM_C_PLANT_LOI = reader["BM_C_PLANT_LOI"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["BM_C_PLANT_LOI"]);
                                model.BM_OIL_PLANT_LOI = reader["BM_Oil_PLANT_LOI"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["BM_Oil_PLANT_LOI"]);
                                model.BM_FEO_PLANT_LOI = reader["BM_Feo_PLANT_LOI"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["BM_Feo_PLANT_LOI"]);

                            }
                        }

                    }
                }
                if (!recordFound)
                {
                    ViewBag.Message = "No record exists for the Given Pile No and Source.";
                    model = new RmbbPile
                    {
                        PileNo = input.PileNo,
                        Source = input.Source
                    };                               
                }               
            }
           return View(model);         

        }
        @model iMonitor_Web.Models.RmbbPile
@{
    Layout = null;
}
@*Created BY:- Pabir Kumar Dey
    Created Date:-01-JUL-2025
    Requested By:-Gaurav Sir.*@
<!DOCTYPE html>
<html>
<head>
    <title>Pile</title>
    <link href="~/Bootstrap5/bootstrap.css" rel="stylesheet" />
    <link href="~/Content/FlatPickr/FlatPickr.css" rel="stylesheet" />
    <style>
        .form-label {
            font-weight:bolder;
            font-family: Georgia, 'Times New Roman', Times, serif;
            font-size:2vh;
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

        h6 {
            font-family: Georgia, 'Times New Roman', Times, serif;
            font-weight: bold;
            color: #8e2626;
        }

        .form-control {
            border-radius: 6px;
            font-family:Courier New, Courier, monospace;
            font-size:2vh;
            font-weight:bold;
        }
        #Main_Heading{
            font-family:Allan,cursive!important;
            font-weight:bold;
            font-size:5vh;
            text-align:center;
            padding:20px;   
            color:brown;
            text-shadow: rgba(13, 0, 77, 0.08) 0px 2px 4px, rgba(13, 0, 77, 0.08) 0px 3px 6px, rgba(13, 0, 77, 0.08) 0px 8px 16px!important;
            border-radius:10px;
        }
        select {
            appearance: auto !important;
            -webkit-a ppearance: auto !important;
            -moz-appearance: auto !important;
            }
    </style>
</head>
<body>
    <div class="container-fluid mt-4">
        <h4 class="mb-4" id="Main_Heading">Raw Material Quantity</h4>
        <hr class="section-divider">
     @if (!string.IsNullOrEmpty(ViewBag.Message))
     {
        <script type="text/javascript">
        alert('@ViewBag.Message');
        </script>
     }

        
        <form method="post" action="/RmbbPile/RmbbPile" id="rawMaterialForm">
            <div class="container-fluid" style="margin-left:280px;">
                <div class="d-flex flex-nowrap gap-2 align-items-end">
                    <div style="width:8%;">
                        <label class="form-label" style="margin-left:40px;">Pile No</label>
                        <input class="form-control" type="text" value="@Model.PileNo" name="PileNo" placeholder="Enter PileNo" autocomplete="off">
                    </div>
                    <div style="width:8%;">
                        <label class="form-label" style="margin-left:40px;">Select Source</label>
                        <select name="Source" id="SourceSelect" class="form-control" onchange="document.getElementById('rawMaterialForm').submit();">
                            <option value="">Select Source</option>
                            <option value="RMBB_KNR" @(Model != null && Model.Source == "RMBB_KNR" ? "selected" : "")>RMBB_KNR</option>
                            <option value="RMBB" @(Model != null && Model.Source == "RMBB" ? "selected" : "")>RMBB</option>
                            <option value="RMBBN" @(Model != null && Model.Source == "RMBBN" ? "selected" : "")>RMBBN</option>
                        </select>


                    </div>
                    <div style="width:8%">
                        <label class="form-label" style="margin-left:40px;">Shift</label>
                        <select class="form-select">
                            <option value="A">A</option>
                            <option value="B">B</option>
                            <option value="C">C</option>
                        </select>
                    </div>
                    <div style="width:12%;">
                        <label class="form-label fw-bold" style="margin-left:40px;">Start Date</label>
                        <input type="text" class="form-control" name="StartDate" id="StartDate" value="@(Model.StartDate.HasValue ? Model.StartDate.Value.ToString("dd-MMM-yyyy HH:mm") : "")" />
                    </div>


                    <div style="width:12%;">
                        <label class="form-label" style="margin-left:40px;">End Date</label>
                        <input type="text" class="form-control" name="EndDate" id="EndDate" value="@(Model.EndDate.HasValue ? Model.EndDate.Value.ToString("dd-MMM-yyyy HH:mm") : "")" />
                    </div>
                    <div style="width:12%;">
                        <label class="form-label" style="margin-left:40px;">Cons.St.Date</label>
                        <input type="text" class="form-control" name="ConsStartDate" id="ConsStartDate" value="@(Model.ConsStartDate.HasValue ? Model.ConsStartDate.Value.ToString("dd-MMM-yyyy HH:mm") : "")" />
                    </div>
                </div>
            </div>
            <hr class="section-divider">
            <!-- First row of materials -->
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Noa Fines</label>
                    <input class="form-control" type="text" value="@Model.NOA_FINES" name="NOA_FINES" id="NOA_FINES" onblur="IOFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Joda Fines</label>
                    <input class="form-control" type="text" value="@Model.JODA_FINES" name="JODA_FINES" id="JODA_FINES" onblur="IOFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">KB Fines</label>
                    <input class="form-control" type="text" value="@Model.KB_FINES" name="KB_FINES" id="KB_FINES" onblur="IOFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Yard Fines</label>
                    <input class="form-control" type="text" value="@Model.YARD_FINES" name="YARD_FINES" id="YARD_FINES" onblur="IOFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">BHJ</label>
                    <input class="form-control" type="text" value="@Model.TXT_BHJ" name="TXT_BHJ" id="TXT_BHJ" onblur="IOFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Namisa</label>
                    <input class="form-control" type="text" value="@Model.IO_NAMISA" name="IO_NAMISA" id="IO_NAMISA" onblur="IMPOreFinesSum()" autocomplete="off">
                </div>
            </div>
            <!-- Second row of materials -->
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Fortescue BF</label>
                    <input class="form-control" type="text" value="@Model.IO_FORTESCUE_BF" name="IO_FORTESCUE_BF" id="IO_FORTESCUE_BF" onblur="IMPOreFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Noa Crushed</label>
                    <input class="form-control" type="text" value="@Model.IRON_ORE_NOA_CRUSHED" name="IRON_ORE_NOA_CRUSHED" id="IRON_ORE_NOA_CRUSHED" onblur="IOFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Joda Crushed</label>
                    <input class="form-control" type="text" value="@Model.IRON_ORE_JODA_CRUSHED" name="IRON_ORE_JODA_CRUSHED" id="IRON_ORE_JODA_CRUSHED" onblur="IOFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">KB Crushed</label>
                    <input class="form-control" type="text" value="@Model.IRON_ORE_KB_CRUSHED" name="IRON_ORE_KB_CRUSHED" id="IRON_ORE_KB_CRUSHED" onblur="IOFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Pilbhara</label>
                    <input class="form-control" type="text" name="IO_PILBHARA" id="IO_PILBHARA" onblur="IMPOreFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Kumba</label>
                    <input class="form-control" type="text" value="@Model.IO_KUMBA" name="IO_KUMBA" id="IO_KUMBA" onblur="IMPOreFinesSum()" autocomplete="off">
                </div>
            </div>
            <!-- Third row of materials -->
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Coastal Fines</label>
                    <input class="form-control" type="text" value="@Model.IO_COASTAL_FINES" name="IO_COASTAL_FINES" id="IO_COASTAL_FINES" onblur="IMPOreFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Deobhar/ Katamati Fines</label>
                    <input class="form-control" type="text" value="@Model.KATAMATI_FINES" name="KATAMATI_FINES" id="KATAMATI_FINES" style="margin:4px;" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Kirandual S/O(Lump)</label>
                    <input class="form-control" type="text" value="@Model.IO_KIRANDUL_SIZE_ORE" name="IO_KIRANDUL_SIZE_ORE" id="IO_KIRANDUL_SIZE_ORE" onblur="IMPOreFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Kirandual Fines</label>
                    <input class="form-control" type="text" value="@Model.IO_KIRANDUL_FINES" name="IO_KIRANDUL_FINES" id="IO_KIRANDUL_FINES" onblur="IMPOreFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">FSF Venezuelan</label>
                    <input class="form-control" type="text" value="@Model.IO_FSF_VENEZUELAN" name="IO_FSF_VENEZUELAN" id="IO_FSF_VENEZUELAN" onblur="IMPOreFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">SN Feed Value</label>
                    <input class="form-control" type="text" value="@Model.IO_SN_FEED_VALE" name="IO_SN_FEED_VALE" id="IO_SN_FEED_VALE" onblur="IMPOreFinesSum()" autocomplete="off">
                </div>

            </div>
            <!-- Fourth row of materials -->
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Other Imp Ore</label>
                    <input class="form-control" type="text" value="@Model.IO_OTHER_IMP_ORE" name="IO_OTHER_IMP_ORE" id="IO_OTHER_IMP_ORE" onblur="IMPOreFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Imp Ore Fines</label>
                    <input class="form-control" type="text" readonly value="@Model.TXT_IMP_ORE_FINES" name="TXT_IMP_ORE_FINES" id="TXT_IMP_ORE_FINES" onblur="IOFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Bacheli</label>
                    <input class="form-control" type="text" value="@Model.DO_BACHELI" name="DO_BACHELI" id="DO_BACHELI" onblur="DomesticOreFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Jaroli</label>
                    <input class="form-control" type="text" value="@Model.DO_JAROLI_FINES" name="DO_JAROLI_FINES" id="DO_JAROLI_FINES" onblur="DomesticOreFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Kay Pee Entp</label>
                    <input class="form-control" type="text" value="@Model.DO_KAY_PEE_ENTERPRISE" name="DO_KAY_PEE_ENTERPRISE" id="DO_KAY_PEE_ENTERPRISE" onblur="DomesticOreFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Ahluwalia Fines</label>
                    <input class="form-control" type="text" value="@Model.DO_AHLUWALIA_FINES" name="DO_AHLUWALIA_FINES" id="DO_AHLUWALIA_FINES" onblur="DomesticOreFinesSum()" autocomplete="off">
                </div>
            </div>
            <!-- Fifth row of materials -->
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Diatari</label>
                    <input class="form-control" type="text" value="@Model.DO_DIATARI_FINES" name="DO_DIATARI_FINES" id="DO_DIATARI_FINES" onblur="DomesticOreFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Domestic IOF</label>
                    <input class="form-control" type="text" value="@Model.TXT_DOMESTIC_ORE_FINES" name="TXT_DOMESTIC_ORE_FINES" id="TXT_DOMESTIC_ORE_FINES" onblur="IOFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Iron Ore Fines</label>
                    <input class="form-control" type="text" readonly value="@Model.IO_FINES" name="IO_FINES" id="IO_FINES" oninput="TOTAL_PILEsum()" autocomplete="off">
                </div>
            </div>
            <hr class="section-divider">
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Limestone HI Silica</label>
                    <input class="form-control" type="text" value="@Model.LS_HI_SILICA" name="LS_HI_SILICA" id="LS_HI_SILICA" onblur="MixedFluxSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Limestaone RPD</label>
                    <input class="form-control" type="text" value="@Model.LS_RPD" name="LS_RPD" id="LS_RPD" onblur="MixedFluxSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Limestone SP Grade</label>
                    <input class="form-control" type="text" value="@Model.LS_SP_GRADE" name="LS_SP_GRADE" id="LS_SP_GRADE" onblur="MixedFluxSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">LD Slag(O/S)</label>
                    <input class="form-control" type="text" value="@Model.LD_SLAG_OS" name="LD_SLAG_OS" id="LD_SLAG_OS" onblur="MixedFluxSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Soap Stone</label>
                    <input class="form-control" type="text" value="@Model.SOAP_STONE" name="SOAP_STONE" id="SOAP_STONE" onblur="MixedFluxSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Limestone Gotan</label>
                    <input class="form-control" type="text" value="@Model.LS_GOTTAN" name="LS_GOTTAN" id="LS_GOTTAN" onblur="MixedFluxSum()" autocomplete="off">
                </div>
            </div>
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Limestone Stone(Imported)</label>
                    <input class="form-control" type="text" value="@Model.LIME_STONE_IMP" name="LIME_STONE_IMP" id="LIME_STONE_IMP" onblur="MixedFluxSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Limestaone Himachal</label>
                    <input class="form-control" type="text" value="@Model.LS_HIMACHAL" name="LS_HIMACHAL" id="LS_HIMACHAL" style="margin:4px;" onblur="MixedFluxSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Bhutan Dolo</label>
                    <input class="form-control" type="text" value="@Model.BHUTAN_DOLO" name="BHUTAN_DOLO" id="BHUTAN_DOLO" style="margin:8px;" onblur="MixedFluxSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Gomardih Dolo</label>
                    <input class="form-control" type="text" value="@Model.GOMARDIH_DOLO" name="GOMARDIH_DOLO" id="GOMARDIH_DOLO" onblur="MixedFluxSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Limestone (Phillipines)</label>
                    <input class="form-control" type="text" value="@Model.LS_PHILLIPINES" name="LS_PHILLIPINES" id="LS_PHILLIPINES" onblur="MixedFluxSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Pyroxenite(Local)</label>
                    <input class="form-control" type="text" value="@Model.PYROXENITE_LOCAL" name="PYROXENITE_LOCAL" id="PYROXENITE_LOCAL" onblur="MixedFluxSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Pyroxenite (Sukinda)</label>
                    <input class="form-control" type="text" value="@Model.PYROXENITE_SUKINDA" name="PYROXENITE_SUKINDA" id="PYROXENITE_SUKINDA" onblur="MixedFluxSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Pyroxenite  (Imp)</label>
                    <input class="form-control" type="text" value="@Model.PYROXENITE_IMPORTED" name="PYROXENITE_IMPORTED" id="PYROXENITE_IMPORTED" onblur="MixedFluxSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Limestone(CP Gr.)</label>
                    <input class="form-control" type="text" value="@Model.LS_CP_GRADE" name="LS_CP_GRADE" id="LS_CP_GRADE" onblur="MixedFluxSum()" style="margin:8px;" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Olivine</label>
                    <input class="form-control" type="text" value="@Model.Olivine" name="Olivine" id="Olivine" onblur="MixedFluxSum()" autocomplete="off">
                </div>
            </div>
            <hr class="section-divider">
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Mixed Flux</label>
                    <input class="form-control" type="text" readonly value="@Model.MIXED_FLUX" name="MIXED_FLUX" id="MIXED_FLUX" oninput="TOTAL_PILEsum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">LD Sludge</label>
                    <input class="form-control" type="text" readonly value="@Model.LD_SLUDGE" name="LD_SLUDGE" id="LD_SLUDGE" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Mill Scale</label>
                    <input class="form-control" type="text" readonly value="@Model.MILL_SCALE" name="MILL_SCALE" id="MILL_SCALE" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Kiln Dust</label>
                    <input class="form-control" type="text" readonly value="@Model.KILN_DUST" name="KILN_DUST" id="KILN_DUST" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Solid Waste</label>
                    <input class="form-control" type="text" style="background-color:#ffd800;border:1px solid black;" value="@Model.SOLID_WASTE" name="SOLID_WASTE" id="SOLID_WASTE" oninput="REVERT_MATSum()" autocomplete="off">
                </div>
                @*<div class="col-md-2" id="pswBlock1" style="display:none">
                        <label class="form-label">PSW_CONS1</label>
                        <input class="form-control" type="text" value="@Model.PSW_CONS1" name="PSW_CONS1" id="PSW_CONS1" onblur="SolidWasteSum()" autocomplete="off">
                    </div>*@
                <div class="col-md-2" id="pswBlock1">
                    <label class="form-label">PSW1</label>
                    <input class="form-control" type="text" value="@Model.PSW_CONS1" name="PSW_CONS1" id="PSW_CONS1" onblur="SolidWasteSum()" autocomplete="off">
                </div>
            </div>
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Mill Sludge</label>
                    <input class="form-control" type="text" readonly value="@Model.MILL_SLUDGE" name="MILL_SLUDGE" id="MILL_SLUDGE" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Flue Dust</label>
                    <input class="form-control" type="text" readonly value="@Model.FLUE_DUST" name="FLUE_DUST" id="FLUE_DUST" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Esp Dust</label>
                    <input class="form-control" type="text" readonly value="@Model.ESP_DUST" name="ESP_DUST" id="ESP_DUST" autocomplete="off">
                </div>
                <div class="col-md-1">
                </div>
                <div class="col-md-2">
                </div>
                <div class="col-md-1">
                    <button type="button" class="btn btn-warning">OK</button>
                </div>
                @*<div class="col-md-2" id="pswBlock2" style="display:none">
                        <label class="form-label">PSW_CONS2</label>
                        <input class="form-control" type="text" value="@Model.PSW_CONS2" name="PSW_CONS2" id="PSW_CONS2" onblur="SolidWasteSum()" autocomplete="off">
                    </div>*@
                <div class="col-md-2" id="pswBlock2">
                    <label class="form-label">PSW2</label>
                    <input class="form-control" type="text" value="@Model.PSW_CONS2" name="PSW_CONS2" id="PSW_CONS2" onblur="SolidWasteSum()" autocomplete="off">
                </div>
            </div>
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">GCP Sludge</label>
                    <input class="form-control" type="text" value="@Model.GCP_SLUDGE" name="GCP_SLUDGE" id="GCP_SLUDGE" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">LD Sludge Fresh</label>
                    <input class="form-control" type="text" value="@Model.LD_SLUDGE_PRM" name="LD_SLUDGE_PRM" id="LD_SLUDGE_PRM" oninput="CopyValue()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Lime Fines</label>
                    <input class="form-control" type="text" value="@Model.LIME_FINES" name="LIME_FINES" id="LIME_FINES" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">LD Slag Fines</label>
                    <input class="form-control" type="text" value="@Model.LD_SLAG_FINES" name="LD_SLAG_FINES" id="LD_SLAG_FINES" autocomplete="off">
                </div>
                <div class="col-md-2">
                </div>               
                <div class="col-md-2" id="pswBlock3">
                    <label class="form-label">Blend-I</label>
                    <select id="PSW_BL1" name="PSW_BL1" onchange="CheckPSW_CONS1()" class="form-control">
                        <option value="">Select</option>
                        @if (ViewBag.PSW_BL1 != null)
                        {
                            foreach(var item in (List<SelectListItem>)ViewBag.PSW_BL1)
                            {
                                <option value="@item.Value">@item.Value</option>
                            }
                        }
                    </select>
                </div>

            </div>
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">WRP</label>
                    <input class="form-control" type="text" value="@Model.WRP" name="WRP" id="WRP" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Dolo Fines</label>
                    <input class="form-control" type="text" value="@Model.DOLO_FINES" name="DOLO_FINES" id="DOLO_FINES" oninput="REVERT_MATSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Flue Dust</label>
                    <input class="form-control" type="text" value="@Model.FLUE_DUST_PRM" name="FLUE_DUST_PRM" id="FLUE_DUST_PRM" oninput="CopyValue()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Mill Sludge</label>
                    <input class="form-control" type="text" value="@Model.MILL_SLUDGE_PRM" name="MILL_SLUDGE_PRM" id="MILL_SLUDGE_PRM" oninput="CopyValue()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">ESP Dust</label>
                    <input class="form-control" type="text" value="@Model.ESP_DUST_PRM" name="ESP_DUST_PRM" id="ESP_DUST_PRM" oninput="CopyValue()" autocomplete="off">
                </div>
                <div class="col-md-2" id="pswBlock4">
                    <label class="form-label">Blend-II</label>
                    <select id="PSW_BL2" name="PSW_BL2" onchange="CheckPSW_CONS2()" class="form-control">
                        <option value="">Select</option>
                        @if (ViewBag.PSW_BL2 != null)
                        {
                            foreach (var item in (List<SelectListItem>)ViewBag.PSW_BL2)
                            {
                                <option value="@item.Value">@item.Value</option>
                            }
                        }
                    </select>
                </div>
            </div>
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Revert Material</label>
                    <input class="form-control" type="text" readonly value="@Model.REVERT_MAT" name="REVERT_MAT" id="REVERT_MAT" oninput="TOTAL_PILEsum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">LD Sludge Mix</label>
                    <input class="form-control" type="text" value="@Model.LD_SLUDGE_MIX_PRM" name="LD_SLUDGE_MIX_PRM" id="LD_SLUDGE_MIX_PRM" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Soild Mix</label>
                    <input class="form-control" type="text" value="@Model.SOLID_MIX" name="SOLID_MIX" id="SOLID_MIX" oninput="REVERT_MATSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Mill Scale</label>
                    <input class="form-control" type="text" value="@Model.MILL_SCALE_PRM" name="MILL_SCALE_PRM" id="MILL_SCALE_PRM" autocomplete="off">
                    @*<input class="form-control" type="text" value="" autocomplete="off">*@
                </div>
                <div class="col-md-2">
                    <label class="form-label">Kiln Dust</label>
                    <input class="form-control" type="text" value="@Model.KILN_DUST_PRM" name="KILN_DUST_PRM" id="KILN_DUST_PRM" autocomplete="off">
                </div>
            </div>
            <hr class="section-divider">
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Coke Breeze</label>
                    <input class="form-control" type="text"  value="@Model.COKE_BREEZE" name="COKE_BREEZE" id="COKE_BREEZE" oninput="TOTAL_PILEsum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">RPC</label>
                    <input class="form-control" type="text"  value="@Model.RPC" name="RPC" id="RPC" oninput="TOTAL_PILEsum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Jhama Coal</label>
                    <input class="form-control" type="text"  value="@Model.JHAMA" name="JHAMA" id="JHAMA" oninput="TOTAL_PILEsum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">G Sinter Fines</label>
                    <input class="form-control" type="text" value="@Model.G_SINTER_FINES" name="G_SINTER_FINES" id="G_SINTER_FINES" onblur="MIXED_MATERIALSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Pellet SN Fines</label>
                    <input class="form-control" type="text" value="@Model.G_PELLET_FINES" name="G_PELLET_FINES" id="G_PELLET_FINES" onblur="MIXED_MATERIALSum()" autocomplete="off">
                </div>
            </div>
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">G ORE Fines</label>
                    <input class="form-control" type="text" value="@Model.G_ORE_FINES" name="G_ORE_FINES" id="G_ORE_FINES" onblur="MIXED_MATERIALSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">BM(End Cone)</label>
                    <input class="form-control" type="text" value="@Model.BM_END_CONE" name="BM_END_CONE" id="BM_END_CONE" onblur="MIXED_MATERIALSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Anthracite</label>
                    <input class="form-control" type="text" value="@Model.ANTHRACITE" name="ANTHRACITE" id="ANTHRACITE" oninput="TOTAL_PILEsum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">BM Previous</label>
                    <input class="form-control" type="text" value="@Model.BM_PREVIOUS" name="BM_PREVIOUS" id="BM_PREVIOUS" onblur="MIXED_MATERIALSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Mixed Material</label>
                    <input class="form-control" type="text" readonly value="@Model.MIXED_MATERIAL" name="MIXED_MATERIAL" id="MIXED_MATERIAL" oninput="TOTAL_PILEsum()" autocomplete="off">
                </div>
            </div>
            <hr class="section-divider">
            <div class="row material-row mb-2">
                <h6>Pile Chemistery</h6>
                <div class="col-md-2">
                    <label class="form-label">Sio2</label>
                    <input class="form-control" type="text" value="@Model.BM_SIO2_PLANT" name="BM_SIO2_PLANT" id="BM_SIO2_PLANT" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Cao</label>
                    <input class="form-control" type="text" value="@Model.BM_CAO_PLANT" name="BM_CAO_PLANT" id="BM_CAO_PLANT" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Phos</label>
                    <input class="form-control" type="text" value="@Model.BM_PHOS_PLANT" name="BM_PHOS_PLANT" id="BM_PHOS_PLANT" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Al2o3</label>
                    <input class="form-control" type="text" value="@Model.BM_AL2O3_PLANT" name="BM_AL2O3_PLANT" id="BM_AL2O3_PLANT" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Total Pile</label>
                    <input class="form-control" type="text" style="background-color:#ffd800;border:1px solid black;" readonly value="@Model.TOTAL_PILE" name="TOTAL_PILE" id="TOTAL_PILE" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">No Of Layers</label>
                    <input class="form-control" type="text" value="@Model.NO_OF_LAYERS" name="NO_OF_LAYERS" id="NO_OF_LAYERS" autocomplete="off">
                </div>
            </div>
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Mgo</label>
                    <input class="form-control" type="text" value="@Model.BM_MGO_PLANT" name="BM_MGO_PLANT" id="BM_MGO_PLANT" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">C</label>
                    <input class="form-control" type="text" value="@Model.BM_C_PLANT" name="BM_C_PLANT" id="BM_C_PLANT" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Oil</label>
                    <input class="form-control" type="text" value="@Model.BM_OIL_PLANT" name="BM_OIL_PLANT" id="BM_OIL_PLANT" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Feo</label>
                    <input class="form-control" type="text" value="@Model.BM_FEO_PLANT" name="BM_FEO_PLANT" id="BM_FEO_PLANT" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <input type="submit" value="Save" name="SaveRawMaterial" class="btn btn-primary" />
                </div>
            </div>

            <hr class="section-divider">
            <div class="row material-row mb-2">
                <h6>Pile Chemistery LOI</h6>
                <div class="col-md-2">
                    <label class="form-label">Sio2</label>
                    <input class="form-control" type="text" value="@Model.BM_SIO2_PLANT_LOI" name="BM_SIO2_PLANT_LOI" id="BM_SIO2_PLANT_LOI" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Cao</label>
                    <input class="form-control" type="text" value="@Model.BM_CAO_PLANT_LOI" name="BM_CAO_PLANT_LOI" id="BM_CAO_PLANT_LOI" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Phos</label>
                    <input class="form-control" type="text" value="@Model.BM_PHOS_PLANT_LOI" name="BM_PHOS_PLANT_LOI" id="BM_PHOS_PLANT_LOI" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Al2o3</label>
                    <input class="form-control" type="text" value="@Model.BM_AL2O3_PLANT_LOI" name="BM_AL2O3_PLANT_LOI" id="BM_AL2O3_PLANT_LOI" autocomplete="off">
                </div>
            </div>
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Mgo</label>
                    <input class="form-control" type="text" value="@Model.BM_MGO_PLANT_LOI" name="BM_MGO_PLANT_LOI" id="BM_MGO_PLANT_LOI" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">C</label>
                    <input class="form-control" type="text" value="@Model.BM_C_PLANT_LOI" name="BM_C_PLANT_LOI" id="BM_C_PLANT_LOI" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Oil</label>
                    <input class="form-control" type="text" value="@Model.BM_OIL_PLANT_LOI" name="BM_OIL_PLANT_LOI" id="BM_OIL_PLANT_LOI" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Feo</label>
                    <input class="form-control" type="text" value="@Model.BM_FEO_PLANT_LOI" name="BM_FEO_PLANT_LOI" id="BM_FEO_PLANT_LOI" autocomplete="off">
                </div>
            </div>
        </form>
    </div>
    <hr class="section-divider">
   
    <script src="~/Content/FlatPickr/FlatPickr.js"></script>
</body>
</html>
<script type="text/javascript"> 
    flatpickr("#StartDate", {
        enableTime: true,
        dateFormat: "d-M-Y H:i",
        time_24hr: true,
        defaultHour:00        
    });

    flatpickr("#EndDate", {
        enableTime: true,
        dateFormat: "d-M-Y H:i",
        time_24hr: true,
        defaultHour: 00
    });

    flatpickr("#ConsStartDate", {
        enableTime: true,
        dateFormat: "d-M-Y H:i",
        time_24hr: true,
        defaultHour: 00
    });


    function DomesticOreFinesSum() {
        var n1 = parseFloat(document.getElementById("DO_BACHELI").value) || 0;
        var n2 = parseFloat(document.getElementById("DO_JAROLI_FINES").value) || 0;
        var n3 = parseFloat(document.getElementById("DO_DIATARI_FINES").value) || 0;
        var n4 = parseFloat(document.getElementById("DO_KAY_PEE_ENTERPRISE").value) || 0;
        var n5 = parseFloat(document.getElementById("DO_AHLUWALIA_FINES").value) || 0;
        var tot_DomesticIOF = n1 + n2 + n3 + n4 + n5;
        document.getElementById("TXT_DOMESTIC_ORE_FINES").value = tot_DomesticIOF;
    }

    function IMPOreFinesSum() {
        var n1 = parseFloat(document.getElementById("IO_NAMISA").value) || 0;
        var n2 = parseFloat(document.getElementById("IO_COASTAL_FINES").value) || 0;
        var n3 = parseFloat(document.getElementById("IO_FORTESCUE_BF").value) || 0;
        var n4 = parseFloat(document.getElementById("IO_PILBHARA").value) || 0;
        var n5 = parseFloat(document.getElementById("IO_SN_FEED_VALE").value) || 0;
        var n6 = parseFloat(document.getElementById("IO_FSF_VENEZUELAN").value) || 0;
        var n7 = parseFloat(document.getElementById("IO_KUMBA").value) || 0;
        var n8 = parseFloat(document.getElementById("IO_KIRANDUL_FINES").value) || 0;
        var n9 = parseFloat(document.getElementById("IO_KIRANDUL_SIZE_ORE").value) || 0;
        var n10 = parseFloat(document.getElementById("IO_OTHER_IMP_ORE").value) || 0;
        var tot_IMPOreFines = n1 + n2 + n3 + n4 + n5 + n6 + n7 + n8 + n9 + n10;        
        document.getElementById("TXT_IMP_ORE_FINES").value = tot_IMPOreFines;
    }

    function IOFinesSum() {
        var n1 = parseFloat(document.getElementById("NOA_FINES").value) || 0;
        var n2 = parseFloat(document.getElementById("JODA_FINES").value) || 0;
        var n3 = parseFloat(document.getElementById("KB_FINES").value) || 0;
        var n4 = parseFloat(document.getElementById("YARD_FINES").value) || 0;
        var n5 = parseFloat(document.getElementById("TXT_BHJ").value) || 0;
        var n6 = parseFloat(document.getElementById("IRON_ORE_NOA_CRUSHED").value) || 0;
        var n7 = parseFloat(document.getElementById("IRON_ORE_JODA_CRUSHED").value) || 0;
        var n8 = parseFloat(document.getElementById("IRON_ORE_KB_CRUSHED").value) || 0;
        var n9 = parseFloat(document.getElementById("TXT_IMP_ORE_FINES").value) || 0;
        var n10 = parseFloat(document.getElementById("TXT_DOMESTIC_ORE_FINES").value) || 0;
        var n11 = parseFloat(document.getElementById("KATAMATI_FINES").value) || 0;
        var tot_IOFines = n1 + n2 + n3 + n4 + n5 + n6 + n7 + n8 + n9 + n10 + n11;
        document.getElementById("IO_FINES").value = tot_IOFines;
        TOTAL_PILEsum();
    }

    function MixedFluxSum() {
        var n1 = parseFloat(document.getElementById("LS_HI_SILICA").value) || 0;
        var n2 = parseFloat(document.getElementById("LS_RPD").value) || 0;
        var n3 = parseFloat(document.getElementById("LS_SP_GRADE").value) || 0;
        var n4 = parseFloat(document.getElementById("LS_GOTTAN").value) || 0;
        var n5 = parseFloat(document.getElementById("BHUTAN_DOLO").value) || 0;
        var n6 = parseFloat(document.getElementById("LS_HIMACHAL").value) || 0;
        var n7 = parseFloat(document.getElementById("PYROXENITE_LOCAL").value) || 0;
        var n8 = parseFloat(document.getElementById("PYROXENITE_IMPORTED").value) || 0;
        var n9 = parseFloat(document.getElementById("PYROXENITE_SUKINDA").value) || 0;
        var n10 = parseFloat(document.getElementById("SOAP_STONE").value) || 0;
        var n11 = parseFloat(document.getElementById("LD_SLAG_OS").value) || 0;
        var n12 = parseFloat(document.getElementById("LIME_STONE_IMP").value) || 0;
        var n13 = parseFloat(document.getElementById("LS_PHILLIPINES").value) || 0;
        var n14 = parseFloat(document.getElementById("LS_CP_GRADE").value) || 0;
        var n15 = parseFloat(document.getElementById("GOMARDIH_DOLO").value) || 0;
        var n16 = parseFloat(document.getElementById("Olivine").value) || 0;
        var tot_MixedFlux = n1 + n2 + n3 + n4 + n5 + n6 + n7 + n8 + n9 + n10 + n11 + n12 + n13 + n14 + n15 + n16;
        document.getElementById("MIXED_FLUX").value = tot_MixedFlux;
        TOTAL_PILEsum();
    }

    function MIXED_MATERIALSum() {
        var n1 = parseFloat(document.getElementById("G_PELLET_FINES").value) || 0;
        var n2 = parseFloat(document.getElementById("G_SINTER_FINES").value) || 0;
        var n3 = parseFloat(document.getElementById("G_ORE_FINES").value) || 0;
        var n4 = parseFloat(document.getElementById("BM_END_CONE").value) || 0;
        var n5 = parseFloat(document.getElementById("BM_PREVIOUS").value) || 0;
        var tot_MIXED_MATERIAL = n1 + n2 + n3 + n4 + n5;
        document.getElementById("MIXED_MATERIAL").value = tot_MIXED_MATERIAL;
        TOTAL_PILEsum();
    }

    function TOTAL_PILEsum() {
        var n1 = parseFloat(document.getElementById("IO_FINES").value) || 0;
        var n2 = parseFloat(document.getElementById("MIXED_FLUX").value) || 0;
        var n3 = parseFloat(document.getElementById("REVERT_MAT").value) || 0;
        var n4 = parseFloat(document.getElementById("COKE_BREEZE").value) || 0;
        var n5 = parseFloat(document.getElementById("MIXED_MATERIAL").value) || 0;
        var n6 = parseFloat(document.getElementById("RPC").value) || 0;
        var n7 = parseFloat(document.getElementById("JHAMA").value) || 0;
        var n8 = parseFloat(document.getElementById("ANTHRACITE").value) || 0;
        var tot_TOTAL_PILE = n1 + n2 + n3 + n4 + n5 + n6+ n7 + n8;
        document.getElementById("TOTAL_PILE").value = tot_TOTAL_PILE;
    }
    function REVERT_MATSum() {
        var n1 = parseFloat(document.getElementById("DOLO_FINES").value) || 0;
        var n2 = parseFloat(document.getElementById("SOLID_MIX").value) || 0;
        var n3 = parseFloat(document.getElementById("SOLID_WASTE").value) || 0;
        var tot_REVERT_MAT = n1 + n2 + n3;
        document.getElementById("REVERT_MAT").value = tot_REVERT_MAT;
        TOTAL_PILEsum();
    }

    function SolidWasteSum(){
        var n1 = parseFloat(document.getElementById("PSW_CONS1").value)||0;
        var n2 = parseFloat(document.getElementById("PSW_CONS2").value)||0;
        var Tot_SolidWaste = n1 + n2;
        document.getElementById("SOLID_WASTE").value = Tot_SolidWaste;
        REVERT_MATSum();
    }
  
    function DisplayPswBlock() {        
        var source = document.getElementById("SourceSelect").value;       
        if (source === 'RMBB_KNR') {
            
        } else {
           
        }
    }
    function CheckPSW_CONS1() {
        var PSW_CONS1Value = document.getElementById("PSW_CONS1").value.trim();
        var dropdown = document.getElementById("PSW_BL1");
        if (PSW_CONS1Value === "") {
            alert("PSW1 is blank.Pls. enter a value.");
            dropdown.value = ""; 
        }
    }
 
    function CheckPSW_CONS2() {
        var PSW_CONS2Value = document.getElementById("PSW_CONS2").value.trim();
        var dropdown = document.getElementById("PSW_BL2");
        if (PSW_CONS2Value === "") {
            alert("PSW2 is blank.Pls. enter a value.");
            dropdown.value = "";
        }
}
    

</script>

using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.Mvc;

namespace iMonitor_Web.Models
{
           public class RmbbPile
    {
            public string PileNo { get; set; }
            public string Source { get; set; }
            public string Shift { get; set; }
            public DateTime? StartDate { get; set; }
            public DateTime? EndDate { get; set; }
            public DateTime? ConsStartDate { get; set; }
            public decimal? NOA_FINES { get; set; }
            public decimal? JODA_FINES { get; set; }
            public decimal? KB_FINES { get; set; }
            public decimal? YARD_FINES { get; set; }
            public decimal? TXT_BHJ { get; set; }
            public decimal? IO_NAMISA { get; set; }
            public decimal? IO_FORTESCUE_BF { get; set; }
            public decimal? IRON_ORE_NOA_CRUSHED { get; set; }
            public decimal? IRON_ORE_JODA_CRUSHED { get; set; }
            public decimal? IRON_ORE_KB_CRUSHED { get; set; }
            public decimal? IO_PILBHARA { get; set; }
            public decimal? IO_KUMBA { get; set; }
            public decimal? IO_COASTAL_FINES { get; set; }
            public decimal? KATAMATI_FINES { get; set; }
            public decimal? IO_KIRANDUL_SIZE_ORE { get; set; }
            public decimal? IO_KIRANDUL_FINES { get; set; }
            public decimal? IO_FSF_VENEZUELAN { get; set; }
            public decimal? IO_SN_FEED_VALE { get; set; }
            public decimal? IO_OTHER_IMP_ORE { get; set; }
            public decimal? TXT_IMP_ORE_FINES { get; set; }
            public decimal? DO_BACHELI { get; set; }
            public decimal? DO_JAROLI_FINES { get; set; }
            public decimal? DO_KAY_PEE_ENTERPRISE { get; set; }
            public decimal? DO_AHLUWALIA_FINES { get; set; }
            public decimal? DO_DIATARI_FINES { get; set; }
            public decimal? TXT_DOMESTIC_ORE_FINES { get; set; }
            public decimal? IO_FINES { get; set; }
            public decimal? LS_HI_SILICA { get; set; }
            public decimal? LS_RPD { get; set; }
            public decimal? LS_SP_GRADE { get; set; }
            public decimal? LD_SLAG_OS { get; set; }
            public decimal? SOAP_STONE { get; set; }
            public decimal? LS_GOTTAN { get; set; }
            public decimal? LIME_STONE_IMP { get; set; }
            public decimal? LS_HIMACHAL { get; set; }
            public decimal? BHUTAN_DOLO { get; set; }
            public decimal? GOMARDIH_DOLO { get; set; }
            public decimal? LS_PHILLIPINES { get; set; }
            public decimal? PYROXENITE_LOCAL { get; set; }
            public decimal? PYROXENITE_SUKINDA { get; set; }
            public decimal? PYROXENITE_IMPORTED { get; set; }
            public decimal? LS_CP_GRADE { get; set; }
            public decimal? Olivine { get; set; }
            public decimal? MIXED_FLUX { get; set; }
            public decimal? LD_SLUDGE { get; set; }
            public decimal? MILL_SCALE { get; set; }            
            public decimal? KILN_DUST { get; set; }
            public decimal? SOLID_WASTE { get; set; }
            public decimal? PSW_CONS1 { get; set; }            
            public  List<SelectListItem> PSW_BL1 { get; set; }
            public decimal? MILL_SLUDGE { get; set; }
            public decimal? FLUE_DUST { get; set; }
            public decimal? ESP_DUST { get; set; }
            public decimal? OK { get; set; }
            public decimal? PSW_CONS2 { get; set; }
            public List<SelectListItem> PSW_BL2 { get; set; }
            public decimal? GCP_SLUDGE { get; set; }
            public decimal? LD_SLUDGE_PRM { get; set; }
            public decimal? LIME_FINES { get; set; }
            public decimal? LD_SLAG_FINES { get; set; }            
            public decimal? WRP { get; set; }
            public decimal? DOLO_FINES { get; set; }
            public decimal? FLUE_DUST_PRM { get; set; }
            public decimal? MILL_SLUDGE_PRM { get; set; }
            public decimal? ESP_DUST_PRM { get; set; }            
            public decimal? REVERT_MAT { get; set; }
            public decimal? LD_SLUDGE_MIX_PRM { get; set; }
            public decimal? SOLID_MIX { get; set; }    
            public decimal? MILL_SCALE_PRM { get; set; }
            public decimal? KILN_DUST_PRM { get; set; }
            public decimal? COKE_BREEZE { get; set; }
            public decimal? RPC { get; set; }
            public decimal? JHAMA { get; set; }
            public decimal? G_SINTER_FINES { get; set; }
            public decimal? G_PELLET_FINES { get; set; }
            public decimal? G_ORE_FINES { get; set; }
            public decimal? BM_END_CONE { get; set; }
            public decimal? ANTHRACITE { get; set; }
            public decimal? BM_PREVIOUS { get; set; }
            public decimal? MIXED_MATERIAL { get; set; }
            public decimal? TOTAL_PILE { get; set; }
            public decimal? NO_OF_LAYERS { get; set; }
            public decimal? BM_SIO2_PLANT { get; set; }
            public decimal? BM_CAO_PLANT { get; set; }
            public decimal? BM_PHOS_PLANT { get; set; }
            public decimal? BM_AL2O3_PLANT { get; set; }                        
            public decimal? BM_MGO_PLANT { get; set; }
            public decimal? BM_C_PLANT { get; set; }
            public decimal? BM_OIL_PLANT { get; set; }
            public decimal? BM_FEO_PLANT { get; set; }
            public decimal? BM_SIO2_PLANT_LOI { get; set; }
            public decimal? BM_CAO_PLANT_LOI { get; set; }
            public decimal? BM_PHOS_PLANT_LOI { get; set; }
            public decimal? BM_AL2O3_PLANT_LOI { get; set; }
            public decimal? BM_MGO_PLANT_LOI  { get; set; }
            public decimal? BM_C_PLANT_LOI  { get; set; }
            public decimal? BM_OIL_PLANT_LOI { get; set; }
            public decimal? BM_FEO_PLANT_LOI { get; set; }



        
    }
}
    }
}

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
        [HttpPost]
        public ActionResult RmbbPile(RmbbPile input, string SaveRawMaterial)
        {
            RmbbPile model = new RmbbPile();
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
                        blendCmd.Parameters.Add(":BL1", OracleDbType.Int32).Value = input.PSW_BL1 ?? 0;
                        blendCmd.Parameters.Add(":BL2", OracleDbType.Int32).Value = input.PSW_BL2 ?? 0;
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
                                model.PSW_BL1 = reader["PSW_BL1"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["PSW_BL1"]);
                                model.PSW_BL2 = reader["PSW_BL2"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["PSW_BL2"]);
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
    }
}

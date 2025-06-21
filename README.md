 [HttpPost]
        public ActionResult RawMaterialEntry(RawMaterialQuantity input,string SaveRawMaterial)
        {
            RawMaterialQuantity model = new RawMaterialQuantity();
           
            if (!string.IsNullOrEmpty(SaveRawMaterial))
            {
                using (OracleConnection conn = new OracleConnection(mycon))
                {
                    conn.Open();

                    using (OracleCommand cmd = new OracleCommand("Proc_Save_Pile_RawMat_Quantity_Entry", conn))
                    {
                        cmd.CommandType = CommandType.StoredProcedure;
                        cmd.Parameters.Add("P_PileNo", OracleDbType.Varchar2).Value = input.PileNo ?? "";
                        cmd.Parameters.Add("P_Source", OracleDbType.Varchar2).Value = input.Source ?? "";
                        cmd.Parameters.Add("P_NoaFines", OracleDbType.Decimal).Value = input.NoaFines ?? 0;
                        cmd.Parameters.Add("P_JodaFines", OracleDbType.Decimal).Value = input.JodaFines ?? 0;
                        cmd.Parameters.Add("P_KBFines", OracleDbType.Decimal).Value = input.KBFines ?? 0;
                        cmd.Parameters.Add("P_YardFines", OracleDbType.Decimal).Value = input.YardFines ?? 0;

                        cmd.ExecuteNonQuery();
                    }
                }

                ViewBag.Message = "Data Saved Successfully";
                model = input;
            }
           else if (!string.IsNullOrEmpty(input.PileNo) && !string.IsNullOrEmpty(input.Source))
            {

                using (OracleConnection conn = new OracleConnection(mycon))
                {
                    conn.Open();
                    string query = "SELECT * FROM imtg.T_PILE_RAWMAT_QUANTITY_NEW WHERE PILE_NO ='" + input.PileNo + "' AND SOURCE ='" + input.Source + "'";
                    using (OracleCommand cmd = new OracleCommand(query, conn))
                    {

                        using (OracleDataReader reader = cmd.ExecuteReader())
                        {
                            if (reader.Read())
                            {
                                model.PileNo = input.PileNo;
                                model.Source = input.Source;
                                model.StartDate = reader["PREP_START_DATE"] == DBNull.Value ? (DateTime?)null : Convert.ToDateTime(reader["PREP_START_DATE"]);
                                model.EndDate = reader["PREP_END_DATE"] == DBNull.Value ? (DateTime?)null : Convert.ToDateTime(reader["PREP_END_DATE"]);
                                model.ConsStartDate = reader["CONS_ST_DATE"] == DBNull.Value ? (DateTime?)null : Convert.ToDateTime(reader["CONS_ST_DATE"]);
                                model.NoaFines = reader["NOA_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["NOA_FINES"]);
                                model.JodaFines = reader["JODA_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["JODA_FINES"]);
                                model.KBFines = reader["KB_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["KB_FINES"]);
                                model.YardFines = reader["YARD_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["YARD_FINES"]);
                                model.BHJ = reader["BHJ"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["BHJ"]);
                                model.Namisa = reader["IO_NAMISA"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["IO_NAMISA"]);
                                model.FortescueBF = reader["IO_FORTESCUE_BF"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["IO_FORTESCUE_BF"]);
                                model.NoaCrushed = reader["IRON_ORE_NOA_CRUSHED"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["IRON_ORE_NOA_CRUSHED"]);
                                model.JodaCrushed = reader["IRON_ORE_JODA_CRUSHED"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["IRON_ORE_JODA_CRUSHED"]);
                                model.KbCrushed = reader["IRON_ORE_KB_CRUSHED"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["IRON_ORE_KB_CRUSHED"]);
                                model.Pilbhara = reader["IO_PILBHARA"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["IO_PILBHARA"]);
                                model.Kumba = reader["IO_KUMBA"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["IO_KUMBA"]);
                                model.CoastalFines = reader["IO_COASTAL_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["IO_COASTAL_FINES"]);
                                model.KatamatiFines = reader["KATAMATI_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["KATAMATI_FINES"]);
                                model.KirandulLump = reader["IO_KIRANDUL_SIZE_ORE"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["IO_KIRANDUL_SIZE_ORE"]);
                                model.KirandulFines = reader["IO_KIRANDUL_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["IO_KIRANDUL_FINES"]);
                                model.FSFVenezuelan = reader["IO_FSF_VENEZUELAN"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["IO_FSF_VENEZUELAN"]);
                                model.SnFeedValue = reader["IO_SN_FEED_VALE"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["IO_SN_FEED_VALE"]);
                                model.OtherImpOre = reader["IO_OTHER_IMP_ORE"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["IO_OTHER_IMP_ORE"]);
                                model.ImpOreFines = reader["IMP_ORE_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["IMP_ORE_FINES"]);
                                model.Bacheli = reader["DO_BACHELI"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["DO_BACHELI"]);
                                model.Jaroli = reader["DO_JAROLI_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["DO_JAROLI_FINES"]);
                                model.KayPeeEntp = reader["DO_KAY_PEE_ENTERPRISE"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["DO_KAY_PEE_ENTERPRISE"]);
                                model.AhluwaliaFines = reader["DO_AHLUWALIA_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["DO_AHLUWALIA_FINES"]);
                                model.Daitari = reader["DO_DIATARI_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["DO_DIATARI_FINES"]);
                                model.DomesticIOF = reader["DOMESTIC_ORE_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["DOMESTIC_ORE_FINES"]);
                                model.IronOreFines = reader["IO_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["IO_FINES"]);
                                model.LimestoneHISilica = reader["LS_HI_SILICA"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["LS_HI_SILICA"]);
                                model.LimestoneRPD = reader["LS_RPD"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["LS_RPD"]);
                                model.LimestoneSPGrade = reader["LS_SP_GRADE"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["LS_SP_GRADE"]);
                                model.LDSlagOs = reader["LD_SLAG_OS"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["LD_SLAG_OS"]);
                                model.SoapStone = reader["SOAP_STONE"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["SOAP_STONE"]);
                                model.LimestoneGotan = reader["LS_GOTTAN"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["LS_GOTTAN"]);
                                model.LimestoneImp = reader["LS_IMPORTED"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["LS_IMPORTED"]);
                                model.LimestoneHimachal = reader["LS_HIMACHAL"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["LS_HIMACHAL"]);
                                model.BhutanDolo = reader["BHUTAN_DOLO"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["BHUTAN_DOLO"]);
                                model.GomardihDolo = reader["GOMARDIH_DOLO"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["GOMARDIH_DOLO"]);
                                model.LimestonePhilipines = reader["LS_PHILLIPINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["LS_PHILLIPINES"]);
                                model.PyroxeniteLocal = reader["PYROXENITE_LOCAL"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["PYROXENITE_LOCAL"]);
                                model.PyroxeniteImp = reader["PYROXENITE_IMPORTED"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["PYROXENITE_IMPORTED"]);
                                model.MixedFlux = reader["MIXED_FLUX"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["MIXED_FLUX"]);
                                model.LdSludge = reader["LD_SLUDGE"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["LD_SLUDGE"]);
                                model.MillScale1 = reader["MILL_SCALE"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["MILL_SCALE"]);
                                model.Kilndust = reader["KILN_DUST"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["KILN_DUST"]);
                                model.SolidWaste = reader["SOLID_WASTE"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["SOLID_WASTE"]);
                                model.MillSludge = reader["MILL_SLUDGE"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["MILL_SLUDGE"]);
                                model.Fluedust = reader["FLUE_DUST"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["FLUE_DUST"]);
                                model.ESPdust = reader["ESP_DUST"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["ESP_DUST"]);
                                model.PSW1 = reader["PSW_CONS1"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["PSW_CONS1"]);
                                model.PSW2 = reader["PSW_CONS2"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["PSW_CONS2"]);
                                model.PSW_BL1 = reader["PSW_BL1"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["PSW_BL1"]);
                                model.PSW_BL2 = reader["PSW_BL2"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["PSW_BL2"]);
                                model.GCPSludge = reader["GCP_SLUDGE"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["GCP_SLUDGE"]);
                                model.LDSludgeFresh = reader["LD_SLUDGE_PRM"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["LD_SLUDGE_PRM"]);
                                model.LimeFines = reader["LIME_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["LIME_FINES"]);
                                model.LDSlagFines = reader["LD_SLAG_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["LD_SLAG_FINES"]);
                                model.WRP = reader["WRP"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["WRP"]);
                                model.DoloFines = reader["DOLO_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["DOLO_FINES"]);
                                model.FlueDustPrm = reader["FLUE_DUST_PRM"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["FLUE_DUST_PRM"]);
                                model.MillSludgePrm = reader["MILL_SLUDGE_PRM"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["MILL_SLUDGE_PRM"]);
                                model.ESPDustPrm = reader["ESP_DUST_PRM"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["ESP_DUST_PRM"]);
                                model.RevertMat = reader["REVERT_MAT"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["REVERT_MAT"]);
                                model.LDSludgeMix = reader["LD_SLUDGE_MIX_PRM"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["LD_SLUDGE_MIX_PRM"]);
                                model.SolidMix = reader["SOLID_MIX"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["SOLID_MIX"]);
                                model.MIllScale = reader["MILL_SCALE_PRM"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["MILL_SCALE_PRM"]);
                                model.KilnDust1 = reader["KILN_DUST_PRM"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["KILN_DUST_PRM"]);
                                model.CokeBreeze = reader["COKE_BREEZE"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["COKE_BREEZE"]);
                                //model.RPC = reader["COKEBREEZE"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["COKEBREEZE"]);
                                //model.JhamaCoal = reader["COKEBREEZE"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["COKEBREEZE"]);
                                model.GSinterFines = reader["G_SINTER_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["G_SINTER_FINES"]);
                                model.PelletSNFines = reader["G_PELLET_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["G_PELLET_FINES"]);
                                model.GOreFines = reader["G_ORE_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["G_ORE_FINES"]);
                                model.BMEndCone = reader["BM_END_CONE"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["BM_END_CONE"]);
                                model.Anthracite = reader["ANTHRACITE"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["ANTHRACITE"]);
                                model.BMPrevious = reader["BM_PREVIOUS"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["BM_PREVIOUS"]);
                                model.MixedMaterial = reader["MIXED_MATERIAL"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["MIXED_MATERIAL"]);
                                model.PileChemSio2 = reader["BM_SIO2_PLANT"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["BM_SIO2_PLANT"]);
                                model.PileChemCao = reader["BM_CAO_PLANT"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["BM_CAO_PLANT"]);
                                model.PileChemPhos = reader["BM_PHOS_PLANT"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["BM_PHOS_PLANT"]);
                                model.PileChemAl2O3 = reader["BM_AL2O3_PLANT"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["BM_AL2O3_PLANT"]);
                                model.TotalPile = reader["TOTAL_PILE"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["TOTAL_PILE"]);
                                model.NoOfLayer = reader["NO_OF_LAYERS"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["NO_OF_LAYERS"]);
                                model.PileChemMgo = reader["BM_MGO_PLANT"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["BM_MGO_PLANT"]);
                                model.PileChemC = reader["BM_C_PLANT"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["BM_C_PLANT"]);
                                model.PileChemOil = reader["BM_OIL_PLANT"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["BM_OIL_PLANT"]);
                                model.PileChemFeo = reader["BM_FEO_PLANT"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["BM_FEO_PLANT"]);
                                model.PileChemLoiSio2 = reader["BM_SIO2_PLANT_LOI"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["BM_SIO2_PLANT_LOI"]);
                                model.PileChemLoiCao = reader["BM_CAO_PLANT_LOI"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["BM_CAO_PLANT_LOI"]);
                                model.PileChemLoiPhos = reader["BM_PHOS_PLANT_LOI"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["BM_PHOS_PLANT_LOI"]);
                                model.PileChemLoiAl2O3 = reader["BM_AL2O3_PLANT_LOI"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["BM_Al2O3_PLANT_LOI"]);
                                model.PileChemLoiMgo = reader["BM_Mgo_PLANT_LOI"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["BM_Mgo_PLANT_LOI"]);
                                model.PileChemLoiC = reader["BM_C_PLANT_LOI"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["BM_C_PLANT_LOI"]);
                                model.PileChemLoiOil = reader["BM_Oil_PLANT_LOI"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["BM_Oil_PLANT_LOI"]);
                                model.PileChemLoiFeo = reader["BM_Feo_PLANT_LOI"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["BM_Feo_PLANT_LOI"]);
                            }
                        }
                    }
                }
            }

            return View(model);
        }

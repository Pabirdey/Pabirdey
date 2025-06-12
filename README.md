  [HttpPost]
        public ActionResult RawMaterialEntry(RawMaterialQuantity input)
        {
            RawMaterialQuantity model = new RawMaterialQuantity();
            
            model.Source = input.Source;
           model.PileNo=input.PileNo;
            

            using (OracleConnection conn = new OracleConnection(mycon))
            {
                conn.Open();

                //string query = "SELECT * FROM imtg.T_PILE_RAWMAT_QUANTITY_NEW WHERE PILE_NO ='"+input.PileNo+"'  AND SOURCE ='"+input.Source+"'";
                    string query = "SELECT * FROM imtg.T_PILE_RAWMAT_QUANTITY_NEW WHERE PILE_NO ='" + input.PileNo + "' AND SOURCE ='" + input.Source + "'";
                using (OracleCommand cmd = new OracleCommand(query, conn))
                {
                    
                    using (OracleDataReader reader = cmd.ExecuteReader())
                    {
                        if (reader.Read())
                        {                                                       
                            model.NoaFines = reader["NOA_FINES"] != DBNull.Value ? Convert.ToDecimal(reader["NOA_FINES"]) : 0;
                            model.JodaFines = reader["JODA_FINES"] != DBNull.Value ? Convert.ToDecimal(reader["JODA_FINES"]) : 0;
                            model.KBFines = reader["KB_FINES"] != DBNull.Value ? Convert.ToDecimal(reader["KB_FINES"]) : 0;
                            model.YardFines=reader["YARD_FINES"] != DBNull.Value ? Convert.ToDecimal(reader["YARD_FINES"]) : 0;
                            model.BHJ = reader["BHJ"] != DBNull.Value ? Convert.ToDecimal(reader["BHJ"]) : 0;
                            model.Namisa = reader["IO_NAMISA"] != DBNull.Value ? Convert.ToDecimal(reader["IO_NAMISA"]) : 0;
                            model.FortescueBF = reader["IO_FORTESCUE_BF"] != DBNull.Value ? Convert.ToDecimal(reader["IO_FORTESCUE_BF"]) : 0;
                            model.NoaCrushed = reader["IRON_ORE_NOA_CRUSHED"] != DBNull.Value ? Convert.ToDecimal(reader["IRON_ORE_NOA_CRUSHED"]) : 0;
                            model.JoaCrushed = reader["IRON_ORE_JODA_CRUSHED"] != DBNull.Value ? Convert.ToDecimal(reader["IRON_ORE_JODA_CRUSHED"]) : 0;
                            model.KbCrushed = reader["IRON_ORE_KB_CRUSHED"] != DBNull.Value ? Convert.ToDecimal(reader["IRON_ORE_KB_CRUSHED"]) : 0;
                            model.Pilbhara = reader["IO_PILBHARA"] != DBNull.Value ? Convert.ToDecimal(reader["IO_PILBHARA"]) : 0;
                            model.Kumba = reader["IO_KUMBA"] != DBNull.Value ? Convert.ToDecimal(reader["IO_KUMBA"]) : 0;
                            //model.CoastalFines = reader["COASTALFINES"] != DBNull.Value ? Convert.ToDecimal(reader["COASTALFINES"]) : 0;
                           // model.KatamatiFines = reader["KATAMATIFINES"] != DBNull.Value ? Convert.ToDecimal(reader["KATAMATIFINES"]) : 0;
                           // model.KirandulLump = reader["KIRANDULLUMP"] != DBNull.Value ? Convert.ToDecimal(reader["KIRANDULLUMP"]) : 0;
                            //model.KirandulFines = reader["KIRANDULFINES"] != DBNull.Value ? Convert.ToDecimal(reader["KIRANDULFINES"]) : 0;
                            model.FSFVenezuelan = reader["IO_FSF_VENEZUELAN"] != DBNull.Value ? Convert.ToDecimal(reader["IO_FSF_VENEZUELAN"]) : 0;
                            model.SnFeedValue = reader["IO_SN_FEED_VALE"] != DBNull.Value ? Convert.ToDecimal(reader["IO_SN_FEED_VALE"]) : 0;
                          //  model.OtherImpOre = reader["OTHERIMPORE"] != DBNull.Value ? Convert.ToDecimal(reader["OTHERIMPORE"]) : 0;
                          //  model.ImpOreFines = reader["IMPOREFINES"] != DBNull.Value ? Convert.ToDecimal(reader["IMPOREFINES"]) : 0;
                            model.Bacheli = reader["DO_BACHELI"] != DBNull.Value ? Convert.ToDecimal(reader["DO_BACHELI"]) : 0;
                            model.Jaroli = reader["DO_JAROLI_FINES"] != DBNull.Value ? Convert.ToDecimal(reader["DO_JAROLI_FINES"]) : 0;
                            model.KayPeeEntp = reader["DO_KAY_PEE_ENTERPRISE"] != DBNull.Value ? Convert.ToDecimal(reader["DO_KAY_PEE_ENTERPRISE"]) : 0;
                            model.AhluwaliaFines = reader["DO_AHLUWALIA_FINES"] != DBNull.Value ? Convert.ToDecimal(reader["DO_AHLUWALIA_FINES"]) : 0;
                            model.Daitari = reader["DO_DIATARI_FINES"] != DBNull.Value ? Convert.ToDecimal(reader["DO_DIATARI_FINES"]) : 0;
                            model.DomesticIOF = reader["DOMESTIC_ORE_FINES"] != DBNull.Value ? Convert.ToDecimal(reader["DOMESTIC_ORE_FINES"]) : 0;
                            model.IronOreFines = reader["IO_FINES"] != DBNull.Value ? Convert.ToDecimal(reader["IO_FINES"]) : 0;
                            model.LimestoneHISilica = reader["LS_HI_SILICA"] != DBNull.Value ? Convert.ToDecimal(reader["LS_HI_SILICA"]) : 0;
                            model.LimestoneRPD = reader["LS_RPD"] != DBNull.Value ? Convert.ToDecimal(reader["LS_RPD"]) : 0;
                            model.LimestoneSPGrade = reader["LS_SP_GRADE"] != DBNull.Value ? Convert.ToDecimal(reader["LS_SP_GRADE"]) : 0;
                           // model.LDSlagOs = reader["LDSLAGOS"] != DBNull.Value ? Convert.ToDecimal(reader["LDSLAGOS"]) : 0;
                            model.SoapStone = reader["SOAP_STONE"] != DBNull.Value ? Convert.ToDecimal(reader["SOAP_STONE"]) : 0;
                            model.LimestoneGotan = reader["LS_GOTTAN"] != DBNull.Value ? Convert.ToDecimal(reader["LS_GOTTAN"]) : 0;
                            model.LimestoneImp = reader["LS_IMPORTED"] != DBNull.Value ? Convert.ToDecimal(reader["LS_IMPORTED"]) : 0;
                            model.LimestoneHimachal = reader["LS_HIMACHAL"] != DBNull.Value ? Convert.ToDecimal(reader["LS_HIMACHAL"]) : 0;
                            model.BhutanDolo = reader["BHUTAN_DOLO"] != DBNull.Value ? Convert.ToDecimal(reader["BHUTAN_DOLO"]) : 0;
                            model.GomardihDolo = reader["GOMARDIH_DOLO"] != DBNull.Value ? Convert.ToDecimal(reader["GOMARDIH_DOLO"]) : 0;
                            model.LimestonePhilipines = reader["LS_PHILLIPINES"] != DBNull.Value ? Convert.ToDecimal(reader["LS_PHILLIPINES"]) : 0;
                         //   model.PyroxeniteLocal = reader["PYROXENITELOCAL"] != DBNull.Value ? Convert.ToDecimal(reader["PYROXENITELOCAL"]) : 0;
                            model.MixedFlux = reader["MIXED_FLUX"] != DBNull.Value ? Convert.ToDecimal(reader["MIXED_FLUX"]) : 0;
                            model.LdSludge = reader["LD_SLUDGE"] != DBNull.Value ? Convert.ToDecimal(reader["LD_SLUDGE"]) : 0;
                            model.MillScale1 = reader["MILL_SCALE"] != DBNull.Value ? Convert.ToDecimal(reader["MILL_SCALE"]) : 0;
                            model.Kilndust = reader["KILN_DUST"] != DBNull.Value ? Convert.ToDecimal(reader["KILN_DUST"]) : 0;
                            model.SolidWaste = reader["SOLID_WASTE"] != DBNull.Value ? Convert.ToDecimal(reader["SOLID_WASTE"]) : 0;
                           // model.MillSludge = reader["MILLSLUDGE"] != DBNull.Value ? Convert.ToDecimal(reader["MILLSLUDGE"]) : 0;
                            model.Fluedust = reader["FLUE_DUST"] != DBNull.Value ? Convert.ToDecimal(reader["FLUE_DUST"]) : 0;
                            model.ESPdust = reader["ESP_DUST"] != DBNull.Value ? Convert.ToDecimal(reader["ESP_DUST"]) : 0;
                           // model.GCPSludge = reader["GCPSLUDGE"] != DBNull.Value ? Convert.ToDecimal(reader["GCPSLUDGE"]) : 0;
                            model.LDSludgeFresh = reader["LD_SLUDGE_FRESH"] != DBNull.Value ? Convert.ToDecimal(reader["LD_SLUDGE_FRESH"]) : 0;
                           // model.LimeFines = reader["LIMEFINES"] != DBNull.Value ? Convert.ToDecimal(reader["LIMEFINES"]) : 0;
                          //  model.LDSlagFines = reader["LDSLAGFINES"] != DBNull.Value ? Convert.ToDecimal(reader["LDSLAGFINES"]) : 0;
                            model.WRP = reader["WRP"] != DBNull.Value ? Convert.ToDecimal(reader["WRP"]) : 0;
                            model.DoloFines = reader["DOLO_FINES"] != DBNull.Value ? Convert.ToDecimal(reader["DOLO_FINES"]) : 0;
                          //  model.Fludust = reader["FLUDUST"] != DBNull.Value ? Convert.ToDecimal(reader["FLUDUST"]) : 0;
                            model.MillSludge1 = reader["MILL_SLUDGE_PRM"] != DBNull.Value ? Convert.ToDecimal(reader["MILL_SLUDGE_PRM"]) : 0;
                            model.ESPDust2 = reader["ESP_DUST_PRM"] != DBNull.Value ? Convert.ToDecimal(reader["ESP_DUST_PRM"]) : 0;
                           // model.RevertMat = reader["REVERTMAT"] != DBNull.Value ? Convert.ToDecimal(reader["REVERTMAT"]) : 0;
                            model.LDSludgeMix = reader["LD_SLUDGE_MIX_PRM"] != DBNull.Value ? Convert.ToDecimal(reader["LD_SLUDGE_MIX_PRM"]) : 0;
                          //  model.SolidMix = reader["SOLIDMIX"] != DBNull.Value ? Convert.ToDecimal(reader["SOLIDMIX"]) : 0;
                            model.MIllScale = reader["MILL_SCALE_PRM"] != DBNull.Value ? Convert.ToDecimal(reader["MILL_SCALE_PRM"]) : 0;
                            model.KilnDust1 = reader["KILN_DUST_PRM"] != DBNull.Value ? Convert.ToDecimal(reader["KILN_DUST_PRM"]) : 0;
                           // model.CokeBreeze = reader["COKEBREEZE"] != DBNull.Value ? Convert.ToDecimal(reader["COKEBREEZE"]) : 0;
                            // model.RPC = reader["COKEBREEZE"] != DBNull.Value ? Convert.ToDecimal(reader["COKEBREEZE"]) : 0;
                            //model.JhamaCoal = reader["COKEBREEZE"] != DBNull.Value ? Convert.ToDecimal(reader["COKEBREEZE"]) : 0;
                           // model.GSinterFines = reader["GSINTERFINES"] != DBNull.Value ? Convert.ToDecimal(reader["GSINTERFINES"]) : 0;
                            model.PelletSNFines = reader["G_PELLET_FINES"] != DBNull.Value ? Convert.ToDecimal(reader["G_PELLET_FINES"]) : 0;
                          //  model.GOreFines = reader["GOREFINES"] != DBNull.Value ? Convert.ToDecimal(reader["GOREFINES"]) : 0;
                          //  model.BMEndCone = reader["BMENDCONE"] != DBNull.Value ? Convert.ToDecimal(reader["BMENDCONE"]) : 0;
                            model.Anthracite = reader["ANTHRACITE"] != DBNull.Value ? Convert.ToDecimal(reader["ANTHRACITE"]) : 0;
                           // model.BMPrevious = reader["BMPREVIOUS"] != DBNull.Value ? Convert.ToDecimal(reader["BMPREVIOUS"]) : 0;
                            model.MixedMaterial = reader["MIXED_MATERIAL"] != DBNull.Value ? Convert.ToDecimal(reader["MIXED_MATERIAL"]) : 0;
                            model.PileChemSio2 = reader["BM_SIO2_PLANT"] != DBNull.Value ? Convert.ToDecimal(reader["BM_SIO2_PLANT"]) : 0;
                            model.PileChemCao = reader["BM_CAO_PLANT"] != DBNull.Value ? Convert.ToDecimal(reader["BM_CAO_PLANT"]) : 0;
                            model.PileChemPhos = reader["BM_PHOS_PLANT"] != DBNull.Value ? Convert.ToDecimal(reader["BM_PHOS_PLANT"]) : 0;
                            model.PileChemAl2O3 = reader["BM_AL2O3_PLANT"] != DBNull.Value ? Convert.ToDecimal(reader["BM_AL2O3_PLANT"]) : 0;
                            model.TotalPile = reader["TOTAL_PILE"] != DBNull.Value ? Convert.ToDecimal(reader["TOTAL_PILE"]) : 0;
                            model.NoOfLayer = reader["NO_OF_LAYERS"] != DBNull.Value ? Convert.ToDecimal(reader["NO_OF_LAYERS"]) : 0;
                            model.PileChemMgo = reader["BM_MGO_PLANT"] != DBNull.Value ? Convert.ToDecimal(reader["BM_MGO_PLANT"]) : 0;
                            model.PileChemC = reader["BM_C_PLANT"] != DBNull.Value ? Convert.ToDecimal(reader["BM_C_PLANT"]) : 0;
                            model.PileChemOil = reader["BM_OIL_PLANT"] != DBNull.Value ? Convert.ToDecimal(reader["BM_OIL_PLANT"]) : 0;
                            model.PileChemFeo = reader["BM_FEO_PLANT"] != DBNull.Value ? Convert.ToDecimal(reader["BM_FEO_PLANT"]) : 0;
                            model.PileChemLoiSio2 = reader["BM_SIO2_PLANT_LOI"] != DBNull.Value ? Convert.ToDecimal(reader["BM_SIO2_PLANT_LOI"]) : 0;
                        }
                    }
                }
            }

            return View(model);
        }

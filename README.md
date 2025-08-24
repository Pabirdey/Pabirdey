 string insertSql = @"INSERT INTO imtg.T_PILE_RAWMAT_QUANTITY_NEW_BK 
                            (PILE_NO,PREP_START_DATE,PREP_END_DATE,CONS_ST_DATE,NOA_FINES,JODA_FINES,KB_FINES,YARD_FINES,BHJ,IO_NAMISA,IRON_ORE_NOA_CRUSHED,IRON_ORE_JODA_CRUSHED,IRON_ORE_KB_CRUSHED,IO_PILBHARA,
                            IO_KUMBA,IO_COASTAL_FINES,KATAMATI_FINES,IO_KIRANDUL_SIZE_ORE,IO_KIRANDUL_FINES,IO_FSF_VENEZUELAN,IO_SN_FEED_VALE,IO_OTHER_IMP_ORE,IMP_ORE_FINES,DO_BACHELI,DO_JAROLI_FINES,
                            DO_KAY_PEE_ENTERPRISE,DO_AHLUWALIA_FINES,DO_DIATARI_FINES,DOMESTIC_ORE_FINES,IO_FINES,LS_HI_SILICA,LS_RPD,LS_SP_GRADE,LD_SLAG_OS,SOAP_STONE,LS_GOTTAN,LS_IMPORTED,LS_HIMACHAL,
                            BHUTAN_DOLO,GOMARDIH_DOLO,LS_PHILLIPINES,PYROXENITE_LOCAL,PYROXENITE_IMPORTED,MIXED_FLUX,LD_SLUDGE,MILL_SCALE,KILN_DUST,SOLID_WASTE,MILL_SLUDGE,FLUE_DUST,ESP_DUST,PSW_CONS2,
                            PSW_BL2,GCP_SLUDGE,LD_SLUDGE_FRESH,LIME_FINES,LD_SLAG_FINES,PSW_BL1,WRP,DOLO_FINES,FLUE_DUST_PRM,MILL_SLUDGE_PRM,ESP_DUST_PRM,REVERT_MAT,LD_SLUDGE_MIX_PRM,SOLID_MIX,MILL_SCALE_PRM,
                            KILN_DUST_PRM,COKE_BREEZE,RPC,JHAMA,G_SINTER_FINES,G_PELLET_FINES,G_ORE_FINES,ANTHRACITE,BM_PREVIOUS,MIXED_MATERIAL,TOTAL_PILE,BM_SIO2_PLANT,BM_CAO_PLANT,BM_PHOS_PLANT,BM_AL2O3_PLANT,
                            BM_MGO_PLANT,BM_C_PLANT,BM_OIL_PLANT,BM_FEO_PLANT,BM_SIO2_PLANT_LOI,BM_CAO_PLANT_LOI,BM_PHOS_PLANT_LOI,BM_AL2O3_PLANT_LOI,BM_MGO_PLANT_LOI,BM_C_PLANT_LOI) 
                            values(:PILE_NO,:PREP_START_DATE,:PREP_END_DATE,:CONS_ST_DATE,:NOA_FINES,:JODA_FINES,:KB_FINES,:YARD_FINES,:BHJ,:IO_NAMISA,:IRON_ORE_NOA_CRUSHED,:IRON_ORE_JODA_CRUSHED,:IRON_ORE_KB_CRUSHED,
                            :IO_PILBHARA,:IO_KUMBA,:IO_COASTAL_FINES,:KATAMATI_FINES,:IO_KIRANDUL_SIZE_ORE,:IO_KIRANDUL_FINES,:IO_FSF_VENEZUELAN,:IO_SN_FEED_VALE,:IO_OTHER_IMP_ORE,:IMP_ORE_FINES,
                            :DO_BACHELI,:DO_JAROLI_FINES,:DO_KAY_PEE_ENTERPRISE,:DO_AHLUWALIA_FINES,:DO_DIATARI_FINES,:DOMESTIC_ORE_FINES,:IO_FINES,:LS_HI_SILICA,:LS_RPD,:LS_SP_GRADE,:LD_SLAG_OS,
                            :SOAP_STONE,:LS_GOTTAN,:LS_IMPORTED,:LS_HIMACHAL,:BHUTAN_DOLO,:GOMARDIH_DOLO,:LS_PHILLIPINES,:PYROXENITE_LOCAL,:PYROXENITE_IMPORTED,:MIXED_FLUX,:LD_SLUDGE,:MILL_SCALE,
                            :KILN_DUST,:SOLID_WASTE,:MILL_SLUDGE,:FLUE_DUST,:ESP_DUST,:PSW_CONS2,:PSW_BL2,:GCP_SLUDGE,:LD_SLUDGE_FRESH,:LIME_FINES,:LD_SLAG_FINES,:PSW_BL1,:WRP,:DOLO_FINES,
                            :FLUE_DUST_PRM,:MILL_SLUDGE_PRM,:ESP_DUST_PRM,:REVERT_MAT,:LD_SLUDGE_MIX_PRM,:SOLID_MIX,:MILL_SCALE_PRM,:KILN_DUST_PRM,:COKE_BREEZE,:RPC,:JHAMA,:G_SINTER_FINES,
                            :G_PELLET_FINES,:G_ORE_FINES,:ANTHRACITE,:BM_PREVIOUS,:MIXED_MATERIAL,:TOTAL_PILE,:BM_SIO2_PLANT,:BM_CAO_PLANT,:BM_PHOS_PLANT,:BM_AL2O3_PLANT,:BM_MGO_PLANT,:BM_C_PLANT,
                            :BM_OIL_PLANT,:BM_FEO_PLANT,:BM_SIO2_PLANT_LOI,:BM_CAO_PLANT_LOI,:BM_PHOS_PLANT_LOI,:BM_AL2O3_PLANT_LOI,:BM_MGO_PLANT_LOI,:BM_C_PLANT_LOI)";
                            using (OracleCommand insertCmd = new OracleCommand(insertSql, conn))
                            {
                                insertCmd.Parameters.Add("PileNo", OracleDbType.Varchar2).Value = input.PileNo ?? "";
                                insertCmd.Parameters.Add("Source", OracleDbType.Varchar2).Value = input.Source ?? "";
                                //insertCmd.Parameters.Add("EndDate", OracleDbType.Date).Value = input.EndDate ?? (object)DBNull.Value;
                                //insertCmd.Parameters.Add("ConstStartDate", OracleDbType.Date).Value = input.ConsStartDate ?? (object)DBNull.Value;
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
                                insertCmd.Parameters.Add("PSW_CONS2", OracleDbType.Decimal).Value = input.PSW_CONS2 ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("PSW_BL2", OracleDbType.Decimal).Value = input.PSW_BL2 ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("GCP_SLUDGE", OracleDbType.Decimal).Value = input.GCP_SLUDGE ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("LD_SLUDGE_FRESH", OracleDbType.Decimal).Value = input.LD_SLUDGE_FRESH ?? (object)DBNull.Value;
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
                                //insertCmd.Parameters.Add("BM_OIL_PLANT_LOI", OracleDbType.Decimal).Value = input.BM_OIL_PLANT_LOI ?? (object)DBNull.Value;
                                //insertCmd.Parameters.Add("BM_FEO_PLANT_LOI", OracleDbType.Decimal).Value = input.BM_FEO_PLANT_LOI ?? (object)DBNull.Value;
                                insertCmd.ExecuteNonQuery();
                            }

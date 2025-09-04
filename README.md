<div class="col-md-2" id="pswBlock4">
                    <label class="form-label">Blend-II</label>
                    <select id="PSW_BL1" name="PSW_BL1" onchange="CheckPSW_CONS1()" class="form-control">
                        <option value="">Select</option>
                        @if (ViewBag.PSW_BL1 != null)
                        {
                            foreach (var item in (List<SelectListItem>)ViewBag.PSW_BL1)
                            {
                                <option value="@item.Value">@item.Value</option>
                            }
                        }
                    </select>
                </div>


                  public  List<SelectListItem> PSW_BL1 { get; set; }

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

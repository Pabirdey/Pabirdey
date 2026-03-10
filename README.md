 <div class="mb-2">
                                    <button type="button" class="btnSaveCastHouse" onclick="SaveCastHouseData()">Save</button>
                                    <button type="button" class="btnHMLogistics" onclick="gotoHMLPage()">HML</button>
                                    @Html.ActionLink("HML Ladle", "HML_Ladle_Details", "HML", new { bf = @urlBF }, new { @class = "btn btn-custom" })
                                </div>     

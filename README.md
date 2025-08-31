   <div class="col-md-2" id="pswBlock3">
                    <label class="form-label">Blend-I</label>                    
                    <select id="PSW_BL1" name="PSW_BL1" onclick="CheckPSW1()" class="form-control">
                        <option value="@Model.PSW_BL1" name="PSW_BL1">Select</option>
                        <option value="1">1</option>
                        <option value="2">2</option>
                        <option value="3">3</option>
                        <option value="4">4</option>
                        <option value="5">5</option>
                        <option value="6">6</option>
                        <option value="7">7</option>
                        <option value="8">8</option>
                        <option value="9">9</option>
                        <option value="10">10</option>
                        <option value="11">11</option>
                        <option value="12">12</option>
                        <option value="13">13</option>
                        <option value="14">14</option>
                        <option value="15">15</option>
                    </select>
                </div>
                <div class="col-md-2" id="pswBlock1">
                    <label class="form-label">PSW1</label>
                    <input class="form-control" type="text" value="@Model.PSW1" name="PSW1" id="PSW1" onblur="SolidWasteSum()" autocomplete="off">
                </div>
                function CheckPSW1(){
        var psw1Value = document.getElementById("PSW1").value.trim();
        if (psw1Value === "") {
            alert("PSW1 is blank.Pls. enter a value");
        }
        
    }

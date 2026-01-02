tableBody += `
<td>
  <input list="MG_CLAY_USED_${i}" 
         class="form-control"
         placeholder="Select or Type"
         value="${parsedData[i].MG_CLAY_USED || ''}">

  <datalist id="MG_CLAY_USED_${i}">
    <option value="LRH">
    <option value="UBQ">
    <option value="SARVESH">
    <option value="CALDYRS">
    <option value="HARIMA(S)">
    <option value="HARIMA(D)">
    <option value="CORUS">
    <option value="TRB">
    <option value="VISUVIUS">
    <option value="HARIMA-TWH4">
    <option value="HARIMA-CPH4">
    <option value="HARIMA(D)-TWH5">
    <option value="HARIMA(D)-TWH5K">
    <option value="HARIMA(D)-TWH5-T">
  </datalist>
</td>`;
int Tlc_repair = 0;

if (vTrp_No >= 7 && vTrp_No <= 37)
{
    DateTime? finalDate = null;
    ThermalImage = null;
    FurCircuit = null;

    if (vTrp_No > 0 &&
        finalDate.HasValue &&
        !string.IsNullOrEmpty(ThermalImage) &&
        !string.IsNullOrEmpty(FurCircuit))
    {
        // Your Tlc_repair logic here
        Tlc_repair = 1;
    }
}

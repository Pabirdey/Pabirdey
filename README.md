public class BFViewModel
{
    public BFViewModel()
    {
        Furnaces = new List<GBFTOIBFPRODUCTION>();
    }

    public List<GBFTOIBFPRODUCTION> Furnaces { get; set; }

    public decimal DISPLAY_ACTUAL { get; set; }

    public decimal DISPLAY_REPORTED { get; set; }

    public decimal DISPLAY_BALANCE { get; set; }

    public decimal DISPLAY_ACTUAL_TD { get; set; }

    public decimal DISPLAY_REPORTED_TD { get; set; }
}



public class GBFTOIBFPRODUCTION
{
    #region BASIC DETAILS

    public string FURNACE { get; set; }

    public DateTime TIMESTAMP { get; set; }

    #endregion

    #region DAILY PRODUCTION

    public decimal ACTUAL { get; set; }

    public decimal REPORTED { get; set; }

    public decimal BALANCE { get; set; }

    #endregion

    #region MONTH TD

    public decimal ACTUAL_TD { get; set; }

    public decimal REPORTED_TD { get; set; }

    #endregion

    #region LADLE TONS

    public decimal LD1_TONS { get; set; }

    public decimal LD2_TONS { get; set; }

    public decimal LD3_TONS { get; set; }

    public decimal MRDTP_TONS { get; set; }

    public decimal NOOFTP { get; set; }

    #endregion

    #region ACTUAL LADLE TONS

    public decimal LD1_TONS_ACTUAL { get; set; }

    public decimal LD2_TONS_ACTUAL { get; set; }

    public decimal LD3_TONS_ACTUAL { get; set; }

    public decimal MRDTP_TONS_ACTUAL { get; set; }

    #endregion

    #region OPTIONAL DISPLAY FIELDS

    public decimal DISPLAY_ACTUAL { get; set; }

    public decimal DISPLAY_REPORTED { get; set; }

    public decimal DISPLAY_BALANCE { get; set; }

    public decimal DISPLAY_ACTUAL_TD { get; set; }

    public decimal DISPLAY_REPORTED_TD { get; set; }

    #endregion

    #region EXTRA OPTIONAL FIELDS

    public string REMARKS { get; set; }

    public string CREATED_BY { get; set; }

    public DateTime CREATED_DATE { get; set; }

    public string UPDATED_BY { get; set; }

    public DateTime UPDATED_DATE { get; set; }

    #endregion
}

public class FurnaceEntry
    {
        public string DateTime { get; set; }
        public string Furnace { get; set; }
        public string OnDate1 { get; set; }
        public string ToDate1 { get; set; }
        public string OnDate2 { get; set; }
        public string ToDate2 { get; set; }
        public string Balance { get; set; }
    }

    public class FurnaceViewModel
    {
        public FurnaceEntry Row1 { get; set; }
        public FurnaceEntry Row2 { get; set; }
        public FurnaceEntry Row3 { get; set; }
    }

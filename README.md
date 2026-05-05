public class SaveModel
{
    public List<MainData> main { get; set; }
    public List<TonnageData> coke { get; set; }
    public List<TonnageData> nut { get; set; }
}

public class MainData
{
    public string Date { get; set; }
    public string Shift { get; set; }
    public string Bunker { get; set; }

    public string C { get; set; }
    public string E { get; set; }
    public string F { get; set; }

    public string Total { get; set; }
    public string Position { get; set; }
    public string Balance { get; set; }
}

public class TonnageData
{
    public string Bunker { get; set; }

    public string C { get; set; }
    public string E { get; set; }
    public string F { get; set; }

    public string Total { get; set; }
}
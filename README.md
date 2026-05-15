string prodDate = "15/MAY/2026";

DateTime dt = DateTime.ParseExact(
                  prodDate,
                  "dd/MMM/yyyy",
                  System.Globalization.CultureInfo.InvariantCulture);

string formattedDate =
    dt.ToString("dd/MMM/yyyy").ToUpper();

Console.WriteLine(formattedDate);

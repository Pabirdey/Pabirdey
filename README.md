string prodDate = "15/05/2026";

DateTime dt = DateTime.ParseExact(
                  prodDate,
                  "dd/MM/yyyy",
                  System.Globalization.CultureInfo.InvariantCulture);

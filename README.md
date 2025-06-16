public ActionResult RawMaterialForm()
{
    var model = new RawMaterialQuantityViewModel();

    for (int i = 0; i < 5; i++) // 5 rows
    {
        model.Items.Add(new RawMaterialQuantity());
    }

    return View(model);
}
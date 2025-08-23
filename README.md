@if (!string.IsNullOrEmpty(ViewBag.Message))
{
    <script type="text/javascript">
        alert('@ViewBag.Message');
    </script>
}

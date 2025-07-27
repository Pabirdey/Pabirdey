<style>
  .pretty-table {
    width: 100%;
    border-collapse: collapse;
    font-family: 'Segoe UI', sans-serif;
    box-shadow: 0 0 10px rgba(0,0,0,0.1);
  }

  .pretty-table th, .pretty-table td {
    padding: 12px 15px;
    border: 1px solid #ccc;
    text-align: center;
  }

  .pretty-table thead {
    background-color: #4CAF50;
    color: white;
  }

  .pretty-table tbody tr:nth-child(even) {
    background-color: #f9f9f9;
  }

  .pretty-table tbody tr:hover {
    background-color: #e6f7ff;
  }
</style>

<table class="pretty-table">
  <thead>
    <tr>
      <th>Item</th>
      <th>Price</th>
      <th>Available</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Pen</td>
      <td>$1.00</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>Notebook</td>
      <td>$3.50</td>
      <td>No</td>
    </tr>
  </tbody>
</table>
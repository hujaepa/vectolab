<template>
  <nav class="navbar navbar-dark bg-primary">
    <div class="container-fluid">
      <a class="navbar-brand" href="#"> Home </a>
    </div>
  </nav>
  <div class="container-fluid">
    <div class="row justify-content-center">
      <div class="col-md-4 m-2">
        <button class="btn btn-success" @click="downloadData()">
          <i class="fas fa-download"></i> Download as CSV
        </button>
      </div>
    </div>
    <div class="row justify-content-center">
      <div class="col-md-4">
        <table class="table" ref="table">
          <table class="table table-bordered table-light">
            <thead class="table-success">
              <th>Asset</th>
              <th>Department</th>
            </thead>
            <tr>
              <td>Printer</td>
              <td>HR</td>
            </tr>
            <tr>
              <td>Scanner</td>
              <td>IT</td>
            </tr>
            <tr>
              <td>Barcode Scanner</td>
              <td>ACCOUNT</td>
            </tr>
          </table>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HomeView",
  methods: {
    downloadData() {
      console.log(this.refs);
      const table = this.$refs.table; // Select the table element

      // Get all rows of the table except the header row
      const rows = Array.from(table.querySelectorAll("tr"));
      console.log(rows);
      // Extract table headers
      const headers = Array.from(rows.shift().querySelectorAll("th")).map(
        (header) => header.textContent
      );
      // Extract the table data into a 2D array
      const data = rows.map((row) =>
        Array.from(row.querySelectorAll("td")).map((cell) => cell.textContent)
      );
      // Convert the data to CSV format
      let csvContent = `${headers.join(",")}\n`;
      csvContent += data.map((row) => row.join(",")).join("\n");

      // Create a temporary <a> element and set the CSV data as its href
      const link = document.createElement("a");
      link.href = "data:text/csv;charset=utf-8," + encodeURI(csvContent);
      link.download = "table_data.csv"; // Set the filename for the downloaded file

      // Programmatically click the link to trigger the download
      link.click();
    },
  },
};
</script>

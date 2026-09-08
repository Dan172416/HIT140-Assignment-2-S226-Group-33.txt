// Extract the largest HTML table from the webpage and download it as a UTF-8 CSV file.
(() => {
  const tables = [...document.querySelectorAll("table")];

  if (tables.length === 0) {
    alert(
      "No HTML table found. Scroll down until the data appears, then try again.",
    );
    return;
  }

  // Select the table containing the most rows
  const table = tables.sort(
    (a, b) => b.querySelectorAll("tr").length - a.querySelectorAll("tr").length,
  )[0];

  const rows = [...table.querySelectorAll("tr")];

  const csvData = rows
    .map((row) => {
      const cells = [...row.querySelectorAll("th, td")];

      return cells
        .map((cell) => {
          const text = cell.innerText
            .replace(/\s+/g, " ")
            .trim()
            .replace(/"/g, '""');

          return `"${text}"`;
        })
        .join(",");
    })
    .join("\n");

  // Add UTF-8 BOM so Excel displays characters correctly
  const blob = new Blob(["\uFEFF" + csvData], {
    type: "text/csv;charset=utf-8;",
  });

  const link = document.createElement("a");
  link.href = URL.createObjectURL(blob);
  link.download = "fifa_goalkeeper_statistics.csv";
  document.body.appendChild(link);
  link.click();
  link.remove();

  setTimeout(() => URL.revokeObjectURL(link.href), 1000);

  console.log(`Downloaded ${rows.length - 1} data rows.`);
})();

---
layout: page
title: SCI CERT Rules (Sorted by Severity)
permalink: /sci-cert-rules/
---

<div id="csv-table-container" style="overflow-x: auto; width: 100%;">
    <table id="data-table">
        <thead>
            <tr>
                <th>Category</th>
                <th>Description</th>
                <th>Rule</th>
                <th>Severity</th>
                <th>Likelihood</th>
                <th>Remediation Cost</th>
                <th>Priority</th>
                <th>Level</th>
            </tr>
        </thead>
        <tbody></tbody>
    </table>
</div>
<div id="pagination" style="text-align: center; margin-top: 20px;"></div>

<script>
    async function loadCSV() {
        const response = await fetch('/sci-cert/sci-cert-coding-standard-rules.csv');
        const data = await response.text();
        const rows = data.split('\n').map(row => row.split(','));

        let currentPage = 1;
        const rowsPerPage = 10;
        const totalRows = rows.length - 1; // Exclude header row
        const totalPages = Math.ceil(totalRows / rowsPerPage);

        function displayPage(page) {
            const table = document.getElementById('data-table').getElementsByTagName('tbody')[0];
            table.innerHTML = ''; // Clear existing rows

            const start = (page - 1) * rowsPerPage + 1; // Skip header row
            const end = Math.min(start + rowsPerPage, rows.length);
            const pageRows = rows.slice(start, end);

            pageRows.forEach(row => {
                const newRow = table.insertRow();
                let severityClass = '';
                if (row[7].trim() === 'L1') severityClass = 'severity-high';
                if (row[7].trim() === 'L2') severityClass = 'severity-medium';
                if (row[7].trim() === 'L3') severityClass = 'severity-low';
                newRow.classList.add(severityClass);
                row.forEach(cell => {
                    const newCell = newRow.insertCell();
                    newCell.textContent = cell;
                });
            });

            displayPagination();
        }

        function displayPagination() {
            const pagination = document.getElementById('pagination');
            pagination.innerHTML = '';

            for (let i = 1; i <= totalPages; i++) {
                const pageLink = document.createElement('a');
                pageLink.href = '#';
                pageLink.textContent = i;
                pageLink.classList.add('page-link');
                if (i === currentPage) {
                    pageLink.classList.add('active');
                }
                pageLink.addEventListener('click', (event) => {
                    event.preventDefault();
                    currentPage = i;
                    displayPage(currentPage);
                });
                pagination.appendChild(pageLink);
            }
        }

        displayPage(currentPage);
    }
    loadCSV().catch(error => console.error('Error loading CSV:', error));
</script>

<style>
    table {
        width: 100%;
        border-collapse: collapse;
        table-layout: fixed;
    }
    th, td {
        border: 1px solid #ddd;
        padding: 8px;
        white-space: nowrap; /* Prevent content wrapping */
    }
    th {
        background-color: #f2f2f2;
        font-weight: bold;
    }
    .severity-high {
        background-color: #FA8072; /* Salmon */
        color: white;
    }
    .severity-medium {
        background-color: #FFA500; /* Tangerine */
    }
    .severity-low {
        background-color: #F0FFF0; /* HoneyDew */
        color: black;
    }
    .page-link {
        margin: 0 5px;
        text-decoration: none;
        color: #007bff;
        padding: 5px 10px;
    }
    .page-link.active {
        font-weight: bold;
        color: #0056b3;
    }
    .severity-high .page-link {
        background-color: #FA8072; /* Salmon */
        color: black;
    }
    .severity-medium .page-link {
        background-color: #FFA500; /* Tangerine */
        color: black;
    }
    .severity-low .page-link {
        background-color: #F0FFF0; /* HoneyDew */
        color: black;
    }
</style>

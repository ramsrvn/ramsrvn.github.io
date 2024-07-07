---
layout: page
title: Resources
permalink: /resources/
---

This page contains useful resources. 
## SCI CERT Coding Standards

SCI CERT Coding Standards are a set of rules and recommendations  developed by the [Secure Coding Initiative (SCI)](https://insights.sei.cmu.edu/documents/3601/2010_017_001_50692.pdf) at [CERT](https://www.sei.cmu.edu/about/divisions/cert), a division of the [Software Engineering Institute (SEI)](https://www.sei.cmu.edu/about/index.cfm) at [Carnegie Mellon University](https://www.cmu.edu). These standards aim to enhance software security by promoting secure coding practices throughout the software development lifecycle. 

The use of secure coding standards defines a proscriptive set of rules and recommendations to which the source code can be evaluated for compliance

### SCI CERT Secure Coding Initiative Objective 
- Reduce the number of vulnerabilities to a level where they can be handled by computer security incident response teams (CSIRTs)
- Decrease remediation costs by eliminating vulnerabilities before software is deployed

### SCI CERT RULES (Sorted by Severity)

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

<script>
    async function loadCSV() {
        const response = await fetch('sci-cert/sci-cert-coding-standard-rules.csv');
        const data = await response.text();
        const rows = data.split('\\n').map(row => row.split(','));
        const table = document.getElementById('data-table').getElementsByTagName('tbody')[0];
        rows.forEach((row, rowIndex) => {
            if (rowIndex === 0) return; // Skip header row
            const newRow = table.insertRow();
            row.forEach((cell, cellIndex) => {
                const newCell = newRow.insertCell();
                newCell.textContent = cell;
                if (cellIndex === 7) { // Apply class based on Level
                    if (cell === 'L1') newCell.classList.add('severity-high');
                    if (cell === 'L2') newCell.classList.add('severity-medium');
                    if (cell === 'L3') newCell.classList.add('severity-low');
                }
            });
        });
    }
    loadCSV();
</script>

<style>
    table {
        width: 100%;
        border-collapse: collapse;
    }
    th, td {
        border: 1px solid #ddd;
        padding: 8px;
    }
    th {
        background-color: #f2f2f2;
    }
    .severity-high {
        background-color: Salmon;
        color: white;
    }
    .severity-medium {
        background-color: Tangerine;
    }
    .severity-low {
        background-color: HoneyDew;
        color: black;
    }
</style>

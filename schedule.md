---
layout: page
title: Course Schedule
permalink: /schedule/
nav_order: 2
---

<style>
  .table-wrap {
    overflow-x: auto;
    -webkit-overflow-scrolling: touch;
    border-radius: 0.5rem;
  }

  .schedule-table {
    width: 100%;
    border-collapse: collapse;
    font-size: 0.95rem;
    min-width: 720px;
    table-layout: fixed;
    background: #2d2d2d; /* dark panel background */
    color: #ddd;
  }

  /* Narrow widths for the first 3 columns */
  .schedule-table colgroup col:nth-child(1) { width: 40px; }  /* Week */
  .schedule-table colgroup col:nth-child(2) { width: 70px; }  /* Date */
  .schedule-table colgroup col:nth-child(3) { width: 64px; }  /* Day */

  /* Header */
  .schedule-table thead th {
    background: #333;
    color: #eee;
    font-weight: 600;
    text-align: left;
    border: 1px solid #444;
    padding: 0.5rem 0.6rem;
    white-space: nowrap;
  }

  /* Data cells */
  .schedule-table td {
    border: 1px solid #444;
    padding: 0.4rem 0.6rem;
    vertical-align: top;
    background: #2d2d2d;
    color: #ddd;
    overflow-wrap: anywhere;
  }

  /* Week cell (grouped rowspan) */
  .schedule-table .week-cell {
    text-align: center;
    font-weight: 700;
    background: #3a3a3a; /* subtle contrast */
    color: #fff;
  }

  /* Zebra striping for readability (skip week cell) */
  .schedule-table tbody tr:nth-child(odd) td:not(.week-cell) {
    background: #262626;
  }

  /* Tight spacing inside markdownify content */
  .schedule-table td p {
    margin: 0.25rem 0;
  }
</style>

<div class="table-wrap">
  <table class="schedule-table">
    <colgroup>
      <col>
      <col>
      <col>
      <col>
      <col>
      <col>
    </colgroup>

    <thead>
      <tr>
        <th>Week</th>
        <th>Date</th>
        <th>Day</th>
        <th>Topic / Lecture</th>
        <th>Lab / Activity / Checkpoint</th>
        <th>Notes / Readings</th>
      </tr>
    </thead>

    <tbody>
      {%- assign groups = site.data.schedule | group_by: "Week" -%}
      {%- for g in groups -%}
        {%- assign span = g.items | size -%}
        {%- for row in g.items -%}
          <tr>
            {%- if forloop.first -%}
              <td class="week-cell" rowspan="{{ span }}">{{ g.name }}</td>
            {%- endif -%}
            <td>{{ row.Date }}</td>
            <td>{{ row.Day }}</td>
            <td>{{ row["Topic / Lecture"] | markdownify | strip }}</td>
            <td>{{ row["Lab / Activity / Checkpoint"] | markdownify | strip }}</td>
            <td>{{ row["Notes/Readings"] | markdownify | strip }}</td>
          </tr>
        {%- endfor -%}
      {%- endfor -%}
    </tbody>
  </table>
</div>
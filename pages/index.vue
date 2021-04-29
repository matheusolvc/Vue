<template>
  <div class="leads">
    <Logo />
    <!-- <Logo dark-background /> -->
    <h1 class="leads__title">Leads</h1>
    <section>
      <table>
        <thead>
          <tr>
            <th class="r-top-left" data-type="numeric">
              ID <span class="resize-handle"></span>
            </th>
            <th data-type="text-short">
              First name <span class="resize-handle"></span>
            </th>
            <th data-type="text-short">
              Last name <span class="resize-handle"></span>
            </th>
            <th data-type="text-short">
              Email <span class="resize-handle"></span>
            </th>
            <th data-type="text-long">
              Street <span class="resize-handle"></span>
            </th>
            <th data-type="text-short">
              Country <span class="resize-handle"></span>
            </th>
            <th class="r-top-right" data-type="text-long">
              University <span class="resize-handle"></span>
            </th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td data-label="id">000001</td>
            <td data-label="First name">Lani</td>
            <td data-label="Last name">Ovendale</td>
            <td data-label="E-mail">lovendale0@w3.org</td>
            <td data-label="Street">7850 Old Shore Drive</td>
            <td data-label="Country">United Kingdom</td>
            <td class="r-bottom-right" data-label="University">
              University of Plymouth
            </td>
          </tr>
          <tr>
            <td data-label="id">000001</td>
            <td data-label="First name">Lani</td>
            <td data-label="Last name">Ovendale</td>
            <td data-label="E-mail">lovendale0@w3.org</td>
            <td data-label="Street">7850 Old Shore Drive</td>
            <td data-label="Country">United Kingdom</td>
            <td class="r-bottom-right" data-label="University">
              University of Plymouth
            </td>
          </tr>
        </tbody>
      </table>
    </section>
  </div>
</template>

<script>
export default {}
</script>

<style lang="scss" scoped="true">
.leads {
  &__title {
    margin: 1.4rem 0;
    padding: 1.4rem 0;
    border-top: $border-color 1px solid;
  }
}
table {
  min-width: 100%;
  width: 100%;
  border-collapse: collapse;
  box-shadow: 1px 0px 35px #ddd;
  margin-bottom: 50px;
}

table,
thead {
  border-radius: 10px;
}

.r-top-left {
  border-top-left-radius: 10px;
}
.r-top-right {
  border-top-right-radius: 10px;
}
.r-bottom-left {
  border-bottom-left-radius: 10px;
}
.r-bottom-right {
  border-bottom-right-radius: 10px;
}

th,
td {
  padding: 15px;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

th {
  position: sticky;
  top: 0;
  background: #3d9df2;
  text-align: left;
  font-weight: normal;
  font-size: 1.1rem;
  color: white;
  position: relative;
}

th:last-child {
  border: 0;
}

.resize-handle {
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  background: black;
  opacity: 0;
  width: 3px;
  cursor: col-resize;
}

.resize-handle:hover,
.header--being-resized .resize-handle {
  opacity: 0.5;
}

th:hover .resize-handle {
  opacity: 0.3;
}

td {
  padding-top: 10px;
  padding-bottom: 10px;
  color: #808080;
}

tr:nth-child(even) td {
  background: #f8f6ff;
}

@media screen and (max-width: 600px) {
  table {
    border: 0;
  }
  table caption {
    font-size: 1.3em;
  }
  table thead {
    display: none;
  }
  table tr {
    border-bottom: 3px solid #ddd;
    display: block;
    margin-bottom: 0.625em;
  }
  table td {
    border-bottom: 1px solid #ddd;
    display: block;
    font-size: 0.8em;
    text-align: right;
  }
  table td:before {
    content: attr(data-label);
    float: left;
    font-weight: bold;
    text-transform: uppercase;
    color: #3d9df2;
  }
  table td:last-child {
    border-bottom: 0;
  }
}
</style>

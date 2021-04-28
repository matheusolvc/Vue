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
            <td>000001</td>
            <td>Lani</td>
            <td>Ovendale</td>
            <td>lovendale0@w3.org</td>
            <td>7850 Old Shore Drive</td>
            <td>United Kingdom</td>
            <td>University of Plymouth</td>
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
:root {
  --radius: 10px;
}
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
  flex: 1;
  display: grid;
  border-collapse: collapse;
  box-shadow: 1px 0px 35px #ddd;
  grid-template-columns:
    minmax(150px, 1fr)
    minmax(150px, 1.67fr)
    minmax(150px, 1.67fr)
    minmax(150px, 1.67fr)
    minmax(150px, 3.33fr)
    minmax(150px, 1.67fr)
    minmax(150px, 3.33fr);
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

thead,
tbody,
tr {
  display: contents;
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
/* The following selector is needed so the handle is visible during resize even if the mouse isn't over the handle anymore */
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
</style>

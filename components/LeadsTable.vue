<script src="https://cdn.jsdelivr.net/npm/vue"></script>

<template>
  <table id="leads">
    <thead>
      <tr>
        <th class="r-top-left" data-type="numeric">
          Id <span class="resize-handle"></span>
        </th>
        <th data-type="text-short">Name <span class="resize-handle"></span></th>
        <th data-type="text-short">
          Username <span class="resize-handle"></span>
        </th>
        <th data-type="text-short">
          E-mail <span class="resize-handle"></span>
        </th>
        <th data-type="text-long">Phone <span class="resize-handle"></span></th>
        <th class="r-top-right" data-type="text-short">
          Website <span class="resize-handle"></span>
        </th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="lead of leads" :key="lead.id">
        <td data-label="Id">{{ lead.id }}</td>
        <td data-label="Name">{{ lead.name }}</td>
        <td data-label="Username">{{ lead.username }}</td>
        <td data-label="E-mail">{{ lead.email }}</td>
        <td data-label="Phone">{{ lead.phone }}</td>
        <td class="r-bottom-right" data-label="Website">{{ lead.website }}</td>
      </tr>
    </tbody>
  </table>
</template>

<script>
import axios from 'axios'

export default {
  el: '#leads',
  data() {
    return {
      leads: [],
    }
  },
  mounted() {
    axios.get('https://jsonplaceholder.typicode.com/users').then((response) => {
      console.log(response.data)
      this.leads = response.data
    })
  },
}
</script>

<style>
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

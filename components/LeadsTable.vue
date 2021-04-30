<script src="https://cdn.jsdelivr.net/npm/vue"></script>

<template>
  <div>
    <div class="wrapper">
      <img
        class="search-icon"
        src="data:image/svg+xml;utf8;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iaXNvLTg4NTktMSI/Pgo8IS0tIEdlbmVyYXRvcjogQWRvYmUgSWxsdXN0cmF0b3IgMTkuMC4wLCBTVkcgRXhwb3J0IFBsdWctSW4gLiBTVkcgVmVyc2lvbjogNi4wMCBCdWlsZCAwKSAgLS0+CjxzdmcgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiB4bWxuczp4bGluaz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94bGluayIgdmVyc2lvbj0iMS4xIiBpZD0iQ2FwYV8xIiB4PSIwcHgiIHk9IjBweCIgdmlld0JveD0iMCAwIDU2Ljk2NiA1Ni45NjYiIHN0eWxlPSJlbmFibGUtYmFja2dyb3VuZDpuZXcgMCAwIDU2Ljk2NiA1Ni45NjY7IiB4bWw6c3BhY2U9InByZXNlcnZlIiB3aWR0aD0iMTZweCIgaGVpZ2h0PSIxNnB4Ij4KPHBhdGggZD0iTTU1LjE0Niw1MS44ODdMNDEuNTg4LDM3Ljc4NmMzLjQ4Ni00LjE0NCw1LjM5Ni05LjM1OCw1LjM5Ni0xNC43ODZjMC0xMi42ODItMTAuMzE4LTIzLTIzLTIzcy0yMywxMC4zMTgtMjMsMjMgIHMxMC4zMTgsMjMsMjMsMjNjNC43NjEsMCw5LjI5OC0xLjQzNiwxMy4xNzctNC4xNjJsMTMuNjYxLDE0LjIwOGMwLjU3MSwwLjU5MywxLjMzOSwwLjkyLDIuMTYyLDAuOTIgIGMwLjc3OSwwLDEuNTE4LTAuMjk3LDIuMDc5LTAuODM3QzU2LjI1NSw1NC45ODIsNTYuMjkzLDUzLjA4LDU1LjE0Niw1MS44ODd6IE0yMy45ODQsNmM5LjM3NCwwLDE3LDcuNjI2LDE3LDE3cy03LjYyNiwxNy0xNywxNyAgcy0xNy03LjYyNi0xNy0xN1MxNC42MSw2LDIzLjk4NCw2eiIgZmlsbD0iIzAwMDAwMCIvPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8L3N2Zz4K"
      />
      <input
        v-model="filter"
        class="search"
        type="text"
        placeholder="Filter by contact or company bs"
      />
    </div>
    <table id="leads">
      <thead>
        <tr>
          <th class="r-top-left" data-type="numeric">
            Id <span class="resize-handle"></span>
          </th>
          <th data-type="text-short">
            Name <span class="resize-handle"></span>
          </th>
          <th data-type="text-short">
            Username <span class="resize-handle"></span>
          </th>
          <th data-type="text-short">
            Company <span class="resize-handle"></span>
          </th>
          <th data-type="text-short">
            E-mail <span class="resize-handle"></span>
          </th>
          <th data-type="text-short">
            Address <span class="resize-handle"></span>
          </th>
          <th data-type="text-long">
            Phone <span class="resize-handle"></span>
          </th>
          <th class="r-top-right" data-type="text-short">
            Website <span class="resize-handle"></span>
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="lead of filteredRows" :key="lead.id">
          <td data-label="Id">{{ lead.id }}</td>
          <td data-label="Name" v-html="highlightMatches(lead.name)">
            {{ lead.name }}
          </td>
          <td data-label="Username">{{ lead.username }}</td>
          <td data-label="Company" v-html="highlightMatches(lead.company.bs)">
            {{ lead.company.name }}<br />{{ lead.company.bs }}
          </td>
          <td data-label="E-mail">{{ lead.email }}</td>
          <td data-label="Address">
            {{ lead.address.street }}, {{ lead.address.suite }}<br />{{
              lead.address.city
            }}
          </td>
          <td data-label="Phone">{{ lead.phone }}</td>
          <td class="r-bottom-right" data-label="Website">
            {{ lead.website }}
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  el: '#leads',
  data() {
    return {
      filter: '',
      leads: [],
    }
  },
  mounted() {
    axios.get('https://jsonplaceholder.typicode.com/users').then((response) => {
      console.log(response.data)
      this.leads = response.data
    })
  },
  methods: {
    highlightMatches(text) {
      const matchExists = text.toLowerCase().includes(this.filter.toLowerCase())
      if (!matchExists) return text

      const re = new RegExp(this.filter, 'ig')
      return text.replace(
        re,
        (matchedText) => `<strong>${matchedText}</strong>`
      )
    },
  },
  computed: {
    filteredRows() {
      return this.leads.filter((lead) => {
        const contact = lead.name.toString().toLowerCase()
        const categorie = lead.company.bs.toLowerCase()
        const searchTerm = this.filter.toLowerCase()

        return categorie.includes(searchTerm) || contact.includes(searchTerm)
      })
    },
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
.wrapper {
  position: relative;
  display: flex;
  min-width: 100px;
  margin-bottom: 15px;
}

.search {
  border: none;
  border-radius: 5px;
  height: 25px;
  width: 100%;
  padding: 5px 23px 5px 30px;
  outline: 0;
  background-color: white;
  border-radius: 25px;
  box-shadow: 1px 1px 6px #ddd;
}

.search-icon {
  position: absolute;
  top: 10px;
  left: 8px;
  width: 14px;
}
</style>

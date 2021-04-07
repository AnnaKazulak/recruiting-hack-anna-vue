<template>
  <div>
    <h1>Systemübersicht</h1>
    <table class="table">
      <tr>
        <th
          v-for="(head, index) in headers"
          :key="index"
          class="customerName"
          @click="head.text == 'Kundenname' ? sortBy() : () => {}"
        >
          {{ head.text }}
        </th>
      </tr>
      <tr v-for="(kunde, index) in json" :key="index">
        <td>
          {{ kunde.name }}
        </td>
        <td>
          <a href="#">{{ kunde.url }}</a>
        </td>
        <td>{{ kunde.login }}</td>
      </tr>
    </table>
  </div>
</template>

<script>
import Kunden from "./assets/kunden.json";

export default {
  name: "App",
  components: {},
  data: () => ({
    search: "",
    json: Kunden,
    sortState: false,
    headers: [
      {
        text: "Kundenname",

        value: "name",
      },
      { text: "Externe URL", value: "url" },
      { text: "Login Seite", value: "login" },
    ],
  }),
  methods: {
    sortBy() {
      this.sortState = !this.sortState;
      const compare = (a, b) => {
        if (a.name > b.name) {
          return 1;
        } else if (a.name < b.name) {
          return -1;
        } else {
          return 0;
        }
      };
      this.json = this.json.sort(compare);
      if (this.sortState == false) {
        this.json = this.json.reverse();
      }
    },
  },
};
</script>
<style>
html {
  font-size: 16px;
  font-family: sans-serif;
}
body {
  background-color: #003a5d;
}
div {
  margin-left: auto;
  margin-right: auto;
  margin-top: 40px;
  background-color: #fff;
  width: 80vw;
  border-radius: 0.25rem;
}
a {
  text-decoration: none;
}
h1 {
  margin-left: 50px;
  padding: 15px;
  border-bottom: 2px solid;
  width: 80%;
  font-weight: normal;
  color: #003a5d;
}

table {
  border-collapse: collapse;
  width: 100%;
  margin-top: 20px;
  background-color: #fff;
}

td,
th {
  padding: 20px;
  color: #003a5d;
}

/* tr:nth-child(even) {
  background-color: rgb(231, 229, 229);
} */
tr:hover {
  background-color: #dbedf8;
}
table th {
  color: #003a5d;
  font-weight: 600;
  letter-spacing: 0.17em;
  text-align: left;
}

.customerName:first-child {
  cursor: pointer;
}
</style>

<template>
  <div id="hello">
    <h1>teste teste teste</h1>
    <h2>{{ item }}</h2>

    <button @click="listHosts(hosts)">teste listHosts</button>
  </div>
</template>

<script>
const dotenv = require("dotenv");
const axios = require("axios");

dotenv.config({ path: "./" });

export default {
  name: "hello",
  data() {
    return {
      item: "",
      hosts: [],
    };
  },
  mounted() {
    axios
      .get("http://10.11.0.22/zabbix/api_jsonrpc.php", {
        headers: {
          "Content-Type": "application/json",
          Authorization: "Basic Og==",
        },
        data: {
          jsonrpc: "2.0",
          method: "host.get",
          params: {
            output: ["hostid", "host"],
            selectInterfaces: ["interfaceid", "ip"]},
          id: 2,
          auth: "e4457827e9e0c381bcc4a1231830c33a"
        }
      })
      .then((response) => (this.item = response.data))

      .catch((errors) => error.response(console.log(errors)));
  },
  methods: {
    listHosts: (hosts) => {
      axios
        .get("http://10.11.0.22/zabbix/api_jsonrpc.php", {
          headers: { "Content-Type": "application/json" },
          data: {
            jsonrpc: "2.0",
            method: "host.get",
            params: {
              output: ["hostid", "host"],
              selectInterfaces: ["interfaceid", "ip"],
              id: 2,
              auth: "e4457827e9e0c381bcc4a1231830c33a"
            }
          }
        })
        .then(function(response){
          data = JSON.parse(response.data)
          console.log(data)
        })
      
        
        .catch(function (error) {
          
        });
    },
  },
};
</script>

<style scoped>
#hello {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1,
h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>


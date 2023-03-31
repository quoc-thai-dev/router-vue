<template>
  <div class="home">
    <h1>This is a home page</h1>
    <hr />

    <SelectTransaction id="select-transaction" :transactions="transactions" />
    <button @click="addData()">Add Transaction</button>
  </div>
</template>

<script>
// @ is an alias to /src
import SelectTransaction from "../components/SelectTransaction.vue";
import { HTTP } from "../common/http";
export default {
  name: "HomeView",
  components: {
    SelectTransaction,
  },
  data() {
    return {
      transactions: [],
    };
  },
  created() {
    fetch("http://localhost:3000/transactions")
      .then((res) => res.json())
      .then((data) => (this.transactions = data))
      .then(() => {
        console.log(this.transactions);
      });
  },
  mounted() {
    console.log("mounted");
  },
  methods: {
    addData() {
      let newObj = {
        id: 5,
        name: "Nồi cơm điện",
        price: 1233333,
      };
      HTTP.post(`transactions`, newObj).then((res) => {
        this.transactions.push(res.data);
      });
    },
  },
};
</script>

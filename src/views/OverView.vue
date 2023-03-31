<template>
  <h1>Overview page</h1>

  <hr />
  <h3>{{ firstName }}</h3>
  <h3>{{ firstObject }}</h3>
  <h3>{{ secondObject }}</h3>

  <div class="simple-list">
    <input type="text" v-model="searchStr" />
    <ul style="list-style: none">
      <li v-for="(data, index) in filterList" :key="index">{{ data }}</li>
    </ul>
  </div>
  <button @click="onChangeName()">Change Name</button>
</template>

<script>
import { ref, reactive, computed, watch, watchEffect } from "vue";
export default {
  name: "OverView",
  props: {
    theme: {
      type: String,
      default: "light",
    },
  },
  setup(props, { emit }) {
    console.log("setup");
    console.log(props.theme);
    console.log(emit);
    const firstName = ref("Quốc Thái");
    const firstObject = ref({
      name: "Thái",
      price: 123456,
    });
    const secondObject = reactive({
      name: "Tố Uyên",
      price: 999999,
    });
    const searchStr = ref("");
    const dataList = reactive(["Thái", "Dương", "Quốc", "Nguyễn"]);
    const filterList = computed(() => {
      return dataList
        .map((list) => list.toLowerCase())
        .filter((list) => list.includes(searchStr.value.toLowerCase()));
    });
    function onChangeName() {
      firstName.value = "Tố Uyên";
      console.log(firstName);
      firstObject.value.name = "Uyên";
      console.log(firstObject);
      secondObject.name = "Thái Pro Vip";
      console.log(secondObject);
    }
    watch(searchStr, (pa, pb) => {
      console.log(pa, pb);
    });
    watchEffect(() => {
      if (searchStr.value) {
        console.log("Run again");
      }
    });
    return {
      firstName,
      onChangeName,
      firstObject,
      secondObject,
      dataList,
      filterList,
      searchStr,
    };
  },
};
</script>

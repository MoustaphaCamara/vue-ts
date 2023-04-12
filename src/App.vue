<template>
  <div class="app">
    <header>
      <div class="title">
        <img src="./assets/heart.svg" alt="logo" />
        <h1>Hyrule jobs</h1>
      </div>
      <div class="order">
        Filtrer par :
        <button @click="handleClick('title')">Titre</button>
        <button @click="handleClick('salary')">Salaire</button>
        <button @click="handleClick('location')">Lieu</button>
      </div>
    </header>
    <JobList :jobs="jobs" :order="order" />
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, toRefs, ref } from "vue";
import Job from "./types/Job";
import JobList from "./components/JobList.vue";
import OrderFilter from "./types/OrderFilter";

export default defineComponent({
  name: "App",
  components: { JobList },
  setup() {
    const jobs = ref<Job[]>([
      { title: "développeur", location: "remote", salary: 36000, id: "1" },
      {
        title: "Pêcheur",
        location: "Lac Laba",
        salary: 40000,
        id: "2",
      },
      {
        title: "Joueur de flute",
        location: "Bois perdus",
        salary: 40000,
        id: "3",
      },
      { title: "Postier", location: "Vagabond", salary: 21000, id: "4" },
      {
        title: "gardien",
        location: "prison gerudo",
        salary: 30000,
        id: "5",
      },
    ]);
    const order = ref<OrderFilter>("title");

    const handleClick = (filter: OrderFilter) => {
      order.value = filter;
    };
    return { jobs, handleClick, order };
  },
  methods: {},
});
</script>

<style scoped>
header {
  text-align: center;
}
header .order {
  margin-top: 20px;
}
header .title {
  display: flex;
  justify-content: center;
}
header img {
  width: 60px;
  margin-right: 20px;
}
header h1 {
  font-size: 3em;
}

button {
  margin: 0 10px;
  color: #1195c9;
  border: 3px solid #1195c9;
  background: #d5f0ff;
  padding: 8px 16px;
  border-radius: 4px;
  cursor: pointer;
  font-weight: bold;
}
</style>

<template>
  <div class="job-list">
    <p>
      Filtré par <strong>{{ order }}</strong>
    </p>
    <transition-group name="list" tag="ul">
      <li v-for="job in orderedJobs" :key="job.id">
        <h2>{{ job.title }}, {{ job.location }}</h2>
        <div class="salary">
          <img src="../assets/rupee.svg" alt="rupees" />
          <p>{{ job.salary }} €</p>
        </div>
        <div class="description">
          <p>
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Quae fugiat
            laboriosam laudantium optio doloribus, ab dignissimos qui sunt
            maiores. Aliquam nesciunt numquam in sed ex odio alias, amet harum
            exercitationem.
          </p>
        </div>
      </li>
    </transition-group>
  </div>
</template>

<script lang="ts">
import { computed, defineComponent, PropType } from "vue";
import Job from "../types/Job";
import OrderFilter from "../types/OrderFilter";
// import Job from '@/types/Job';

export default defineComponent({
  props: {
    jobs: {
      required: true,
      type: Array as PropType<Job[]>,
    },
    order: {
      required: true,
      type: String as PropType<OrderFilter>,
    },
  },
  setup(props) {
    const orderedJobs = computed(() => {
      // instead of props.jobs.sort (mutating the actual array) we create a new temporary array wit spread operator
      return [...props.jobs].sort((a: Job, b: Job) => {
        return a[props.order] > b[props.order] ? 1 : -1;
      });
    });
    return { orderedJobs };
  },
});
</script>
<style scoped>
.job-list {
  max-width: 960px;
  margin: 40px auto;
}
.job-list ul {
  padding: 0;
}
.job-list li {
  list-style-type: none;
  background: white;
  padding: 16px;
  margin: 16px 0;
  border-radius: 4px;
}
.job-list h2 {
  margin: 0 0 10px;
  text-transform: capitalize;
}
.salary {
  display: flex;
}
.salary img {
  width: 30px;
}
.salary p {
  color: #17bf66;
  font-weight: bold;
  margin: 10px 4px;
}
.list-move {
  transition: all 1s;
}
</style>

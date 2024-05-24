<template>
  <div class="app">
    <header>
      <div class="order">
        <button @click="handleFilter('title')">Order by title</button>
        <button @click="handleFilter('salary')">Order by salary</button>
        <button @click="handleFilter('location')">Order by location</button>
      </div>
    </header>
    <JobsList :jobs="jobs" :order="order" /> <!-- Passing data in Props   -->

    <!-- Learning component  -->
    <Ref_Reactive />
    <LifecycleHHooks />
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import Job from './types/jobs';
import JobsList from './components/JobsList.vue';
import orderTerm from './types/orderTerms';
import Ref_Reactive from './components/Ref_Reactive.vue';
import LifecycleHHooks from './components/LifecycleHHooks.vue';

export default defineComponent({
  name: 'App',
  components: { JobsList, Ref_Reactive, LifecycleHHooks },

  setup() {
    const jobs = ref<Job[]>([
      { title: "Front-End Developer", location: "Nairobi", salary: 1500, id: '1' },
      { title: "Back-End Developer", location: "Cape Town", salary: 1300, id: '2' },
      { title: "Full Stack Developer", location: "Lagos", salary: 1400, id: '3' },
      { title: "DevOps Engineer", location: "Accra", salary: 1600, id: '4' },
      { title: "Data Scientist", location: "Johannesburg", salary: 1700, id: '5' }
    ])

    //State to truck filter change
    const order = ref<orderTerm>('title')

    // Func to filter jobs by type: orderTerm,
    const handleFilter = (term: orderTerm) => {
      order.value = term
    }

    return { jobs, handleFilter, order }; //if not return it cann't be used in template
  },
});
</script>

<style>
  header {
    text-align: center;
  }
  header .order {
    margin-top: 20px;
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

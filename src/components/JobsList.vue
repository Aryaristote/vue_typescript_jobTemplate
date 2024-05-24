<template>
    <div class="job-list">
        <p>Orded by: {{ order }}</p>    
        <ul>
            <li v-for="job in jobs" :key="job.id">
                <h2>{{ job.title }} in {{ job.location }}</h2>
                <div class="salary">
                    <p>{{ job.salary }} Rwfc</p>
                </div>
                <div class="description">
                    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Sequi, commodi aperiam! Reprehenderit possimus doloribus aperiam 
                        illum aspernatur minus, debitis dicta, sed numquam ipsam qui magni voluptates a saepe itaque vitae.
                    </p>
                </div>
            </li>
        </ul>
    </div>
</template>

<script lang="ts">
import Job from '@/types/jobs';
import orderTerm from '@/types/orderTerms';
import { PropType, computed, defineComponent } from 'vue'; 

export default defineComponent({
    props: {
        // Data received from app through props. 
        jobs: {
            required: true, // Make the props required for this component
            type: Array as PropType<Job[]>, // Make the prors to have to type of interface defined.
        },
        // Fiter by from props.
        order: {
            required: true,
            type: String as PropType<orderTerm>,
        }
    },
    // To change list state 
    setup(props) {
    const orderedJobs = computed(() => {
      return [...props.jobs].sort((a: Job, b: Job) => {
        return a[props.order] > b[props.order] ? 1 : -1
      })
    })

    return { orderedJobs }
  },
})
</script>

<style scoped>
    .job-list {
    max-width: 960px;
    margin: 40px auto;
  }
  .job-list ul {
    padding: 0
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
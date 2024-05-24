<template>
    <h1>Hello VueJS & TypeScript</h1>
    <div>
      <p>{{ name }} - {{ age }}</p>
      <button @click="changeName('John Chishugi')">Change the name: </button>
      <button @click="changeAge('26')">Change the Age: </button>
  
      <!-- In case Reactive 
        <p>Typed Surname: {{ surName }}</p> 
        <input v-model="surName" placeholder="Change name" />   -->
    </div>
  </template>
  
  <script lang="ts">
  import { defineComponent, reactive, ref, toRefs } from 'vue';
  import Job from './types/jobs';
  
  export default defineComponent({
    name: 'App',
    components: {},
  
    //In case you use setup func 
    setup() {
      // In case using Reactive 
      // const state = reactive({
      //   surName: 'Kalume Ernest',
      // })
      // return{ ...toRefs(state) };
  
      // In case using ref 
      const name = ref('Kalume Ernest');
      const age = ref<number | string>(20)
      
       return { name, age } 
    },
  
    //In case you use data func.
    // data() {
    //   return {
    //     name: 'Kalume Ernest',
    //     age: 25 as string | number, // To assign a type to it.
    //   }
    // },
  
    methods: {
      changeName(name: string): number{
        this.name = name;
        return 12;
      },
  
      changeAge(age: number | string){
        this.age = age;
      }
    }
  });
  </script>
  
  <style>
  </style>
  
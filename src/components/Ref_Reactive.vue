<template>
  <div class="main">
    <div class="col">
      <p>Count using REF: {{ count }}</p>
      <button @click="increment">Increment the Number</button>
    </div>

    <div>
      <p>Count using REACTIVE: {{ reactCount }}</p>
      <button @click="reactIncrement">Increment the Number</button>
    </div>
  </div>
  <hr>
  <div>
    <p>Count from OBJECT Name: <b>{{ user.name }}</b> - Age: <b>{{ user.age }}</b></p>
    <button @click="changeName('Kalumee Ernest')">Change the name</button> 
  </div><hr>
</template>

<script>
import { reactive, ref, toRefs } from 'vue';
export default {
  setup() {
    const count = ref(0);
    const errors = ref({})
    const increment = () => {
      count.value ++;
    }

    const user = ref({
      name: 'John Doe',
      age: 30
    });

    const changeName = (newName) => {
      user.value.name = newName;
    }

    // Reactive.
    const state = reactive({ reactCount: 0 })
    function reactIncrement() {
      state.reactCount ++;
      console.log(state);
    }
    
    // Ref
    const validation = (username) => {
      if(username.lengtth < 5) {
        errors.value.username = "Invalid length of the username"
      }else {
        errors.value.username = null;
      }
    }
    
    return { count, increment, changeName, user, validation, errors, reactIncrement, ...toRefs(state) }
  }
}
</script>

<style>
  .main{
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-around;
  }
</style>
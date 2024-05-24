<template>
  <div>
    <p v-if="loading">Loading...</p>
    <p v-else>{{ message }}</p>
  </div><hr/>
  <div>
    <p>{{ time }}</p>
  </div><hr/>
</template>

<script>
import { onMounted, ref } from 'vue';
export default {
    // onMounted using Options API
    data(){
        return {
            message: "Loading...",
            loading: false,

            // onUnmounted
            time: 0,
            intervalId: null,
        }
    },

    created(){
        this.fetchMessage();
        this.startTimer();
    },

    // onUnmounted
    beforeUnmount() {
        clearInterval(this.intervalId);
    },

    methods: {
        async fetchMessage() { 
            setTimeout(() => {
                this.message = 'Hello, world! we are ready.';
                this.loading = true;
            }, 3000);
        },

        //onUnmounted
        startTimer() {
            this.intervalId = setInterval(() => {
                this.time++;
            }, 1000);
        },
    },
    
    // Composition API
    setup() {
        const message1 = ref('Loading...');
        const loading1 = ref(false); 

        const fetchMessage = async() => {
            setTimeout(() => {
                message1.value = 'Hello, world! we are ready';
                loading1.value = true;
            }, 1000);
        }

        // Run the func when ready.
        onMounted(fetchMessage());

        return { message1, loading1 }
    },
}
</script>
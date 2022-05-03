<template>
  <div id="app">
    <ol>
      <li v-for="(question) of users" :key=question.id>
         <div>
           <div>
             <p>test</p>
           </div>
         </div>
      </li>
    </ol>
  </div>
</template>

<script>
  import usersData from "../../users.json";

  export default {
    data() {
      return {
        users: usersData,
      };
    },


  methods: {
     increment() {
       this.users
     }
   },

  mounted() {
     console.log(`Testing ${this.users}.`)
   }
 }
</script>

<!-- <style>
 li
</style> -->

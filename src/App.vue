<template>
  <v-app>
     <hello-world  @search-input-emit="search"/>
    <v-app-bar app color= "white" dark >
        <button class="user">
        <span class="material-icons">person
      <v-spacer></v-spacer>
      </span>
      </button>
    </v-app-bar>
    <v-main>
      <router-view/>
    </v-main>
</v-app>
</template>

<script>
import HelloWorld from '@/components/HelloWorld.vue'
export default {
  name: 'App',
  components: {
    HelloWorld
  },
  methods: {
    search (val) {

    }
  }
}
</script>

<style></style>

<style scoped>
.material-icons{
  color: black;
}
.menu{
  border:none; /* Remove borders */
  color: white; /* White text */
  cursor: pointer;
   padding: 5px 5px;
}

.menu:hover {
  background-color: rgb(152, 153, 156);
}
.user{
  padding: 15px 5px;
  margin-left: 1150px;
  display: flex;
  height: 100%;
  width: 100%;
  border-radius: 12px;
}
.user:hover {
  background-color: #4941f0;
}
</style>

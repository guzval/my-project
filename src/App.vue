<template>
 <main>
   <v-app>
      <v-content>
        <guest-navigation />
        <v-container class="mt-3 mb-3">
          <router-view/>
        </v-container>

        <app-footer/>

      </v-content>
   </v-app>
 </main>
</template>

<script>
  import GuestNavigation from '@/navigations/guest';
  import AppFooter from '@/components/Footer';
  export default {
    components:{
      AppFooter,
      GuestNavigation
    },
    name: 'App'
  }
</script>

<style>
#app {
  text-align: center;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
   /*
   font-family: 'Avenir', Helvetica, Arial, sans-serif;
   margin-top: 60px; */
}
</style>

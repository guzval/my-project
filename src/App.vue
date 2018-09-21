<template>
 <main>
   <v-app>
      <v-content v-if="$store.state.loaded">
        
        <guest-navigation v-if="role === 'guest'"/>
        <admin-navigation v-if="role === 'admin'"/>

        <v-container class="mt-3 mb-3">
          <router-view/>
        </v-container>

        <app-footer/>

      </v-content>

      <v-container v-else fill-height>
        <v-layout flex align-center justify-center>
          <v-progress-circular indeterminate :size="100" :width="10" color="purple" />
        </v-layout>
      </v-container>
   </v-app>
 </main>
</template>

<script>
  import GuestNavigation from '@/navigations/guest';
  import AppFooter from '@/components/Footer';
  import AdminNavigation from '@/navigations/admin';
  import {mapGetters} from 'vuex';
  export default {
    components:{
      AdminNavigation,
      AppFooter,
      GuestNavigation
    },
    name: 'App',
    computed: {
      ...mapGetters(['role'])
    }
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

<template id="app">
  <!-- <keep-alive> -->
    <router-view v-on:callParent="listenChild($event)"></router-view>
  <!-- </keep-alive> -->
</template>

<script>
import AuthService from './auth/AuthService'
const auth = new AuthService()
const { login, logout, authenticated, authNotifier } = auth

import loginPage from './components/loginPage/loginPage.vue'
import locations from './components/locations/locations.vue'
import patients from './components/patients/patients.vue'
import newPatient from './components/newPatient/newPatient.vue'
import updatePatient from './components/updatePatient/updatePatient.vue'
import status from './components/status/status.vue'

export default {
  name: 'app',
  components: {
    loginPage,
    locations,
    patients,
    newPatient,
    updatePatient,
    status
  },
  data() {
    authNotifier.on('authChange', authState => {
      this.authenticated = authState.authenticated
    })
    return {
      auth,
      authenticated,
      locationClicked: '',
      user: '',
      patient: ''
    }
  },
  methods: {
    login,
    logout,
    listenChild(update){
      this.locationClicked = update;
      // console.log(this.locationClicked);
    }
  }
}
</script>

<style src="./style.css"></style>

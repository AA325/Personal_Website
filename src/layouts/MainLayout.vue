<template>
  <q-layout view="hHh lpR fFf">

    <q-header flat :class="!isDarkTheme?'bg-indigo-12':'bg-grey-10'">
      <q-toolbar>
        <q-toolbar-title>
          <q-avatar>
            <img src="~assets/profile.jpg">
          </q-avatar>
          Title
        </q-toolbar-title>

        <q-btn dense flat round icon="nightlight_round" v-if="!isDarkTheme" @click="setDarkTheme" />
        <q-btn dense flat round icon="wb_sunny" v-if="isDarkTheme" @click="setLightTheme" />
      </q-toolbar>
    </q-header>

    <q-page-container style="width:100%;">
    <q-page style="max-width:1920px;margin:0 auto;" class="q-pa-md">
      <router-view />
    </q-page>

    </q-page-container>

    <q-footer flat :class="!isDarkTheme?'bg-indigo-12':'bg-grey-10'">
      <q-toolbar>
        <q-toolbar-title style="display:grid">
          <div style="margin:0 auto;">
          <q-btn dense class="bg-white" flat round :icon="'img:github-light.svg'" @click="openURL('http://www.github.com/aa325')" />
          </div>
        </q-toolbar-title>
      </q-toolbar>
    </q-footer>

  </q-layout>
</template>

<script>
import { openURL } from 'quasar'
export default {
  name:'MainLayout',
  mounted(){
    let dark =  this.$q.localStorage.getItem('app-dark-theme') || true
    if (dark){
      this.setDarkTheme()
    } else {
      this.setLightTheme()
    }
  },
  data(){
    return {

    }
  },
  computed:{
    isDarkTheme(){
      return this.$q.dark.isActive
    }
  },
  methods:{
    openURL(url){
      return openURL(url)
    },
    setDarkTheme(){
      this.$q.dark.set(true)
      this.$q.localStorage.set('app-dark-theme', true)
    },
    setLightTheme(){
      this.$q.dark.set(false)
      this.$q.localStorage.set('app-dark-theme', false)
    }
  }
}

</script>

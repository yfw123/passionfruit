<template>
  <div class="container is-fluid">
    <div class="columns section">
      <div class="column is-one-quarter">
        <h1 class="title has-text-grey-darker"><img class="logo" src="../assets/logo.svg" alt="Passionfruit"></h1>
        <aside class="menu">
          <p class="menu-label">
            Frida version: {{ version }} 
          </p>
          <p class="menu-label">
            Devices <loading v-if="loadingDevices" class="is-pulled-right"></loading>
          </p>
          <ul class="menu-list">
            <li v-for="dev in devices" :key="dev.id">
              <router-link :to="{ name: 'apps', params: { device: dev.id } }">
                <icon :icon="dev.icon" :width="24" :height="24"></icon> {{ dev.name }}
              </router-link>
            </li>
            <li v-if="!devices.length"><b-icon icon="error"></b-icon> No device found</li>
          </ul>
          <p class="menu-label">
            General
          </p>
          <ul class="menu-list">
            <!-- <li><a><b-icon icon="settings"></b-icon> <span>Preference</span></a></li> -->
            <li><a target="_blank" href="http://github.com/chaitin/passionfruit">
              <b-icon icon="open_in_browser"></b-icon> <span>Github</span></a></li>
          </ul>
        </aside>
      </div>

      <div class="column">
        <router-view></router-view>
      </div>

    </div>
  </div>

</template>

<script>
import { mapGetters, mapActions } from 'vuex'
import { GET_VERSION, GET_DEVICES, LOAD_DEVICES, DEVICES_LOADING } from '~/vuex/types'
import Icon from '~/components/Icon.vue'
import Loading from '~/components/Loading.vue'

export default {
  components: {
    Icon,
    Loading,
  },
  computed: {
    ...mapGetters({
      version: GET_VERSION,
      devices: GET_DEVICES,
      loadingDevices: DEVICES_LOADING,
    })
  },
  methods: {
    ...mapActions({
      refresh: LOAD_DEVICES
    })
  },
  mounted() {
    this.refresh()
  }
}
</script>

<style>

</style>

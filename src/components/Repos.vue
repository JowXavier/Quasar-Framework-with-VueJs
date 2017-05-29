<template>
  <q-layout>
      <div slot="header" class="toolbar">
          <q-toolbar-title>
              Repositórios - Quasar Framework v{{ $q.version }}
              <!-- Repositórios - Quasar Framework v{{ $q | json }} -->
          </q-toolbar-title>
      </div>

      <button class="primary" v-link="'/'">Voltar</button>

      <div class="layout-view">
          <h4>Últimos {{ list.length}} repositórios publicados</h4>

          <div class="list">
              <div class="item" v-for="repo in list">
                  <img :src="repo.owner.avatar_url" class="item-primary">
                  <div class="item-content">
                      {{ repo.name }}
                  </div>
                  <div class="item-secondary">
                      <a :href="repo.html_url" target="_blank">
                          <i class="material-icons">open_in_browser</i>
                      </a>
                  </div>
              </div>
          </div>
      </div>
  </q-layout>
</template>

<script>
import axios from 'axios'
let user = 'JowXavier'

export default {
    data () {
        return {
            list: []
        }
    },
    mounted () {
        axios.get('https://api.github.com/users/' + user + '/repos?direction=asc')
            .then((res) => {
                this.list = res.data
                console.log(this.list)
            })
    }
}
</script>

<style>
    .layout-view {
        padding: 10px;
    }
</style>

<template>
  <div>
    <podlove-web-player :config="example" @ready="initPlayer" />

    <h4>Config</h4>
    <json-editor :json="example" @update="updateConfig" height="500px" />
  </div>
</template>

<script>
  import { INIT } from '@podlove/player-actions/types'
  import example from '../public/fixtures/example.json'

  export default {
    data () {
      return {
        example,
        store: null
      }
    },

    methods: {
      initPlayer (store) {
        this.store = store
      },

      updateConfig (payload) {
        this.store.dispatch({
          type: INIT,
          payload
        })
      }
    }
  }
</script>

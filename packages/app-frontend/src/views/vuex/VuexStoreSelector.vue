<template lang="html">
  <action-header slot="header">
    <VueSelect
      v-model="currentInspectedStateIndex"
      placeholder="Select Vuex store to inspect..."
      button-class="flat"
      class="available-stores-select"
    >
      <VueSelectButton
        v-for="index in storeCount"
        :key="index"
        :value="index"
        :label="'' + index"
      />
      <div
        v-if="storeCount === 0"
        class="vue-ui-empty"
      >
        No available Vuex store
      </div>
    </VueSelect>
  </action-header>
</template>

<script>
import { mapState, mapActions } from 'vuex'
import ActionHeader from '@front/components/ActionHeader.vue'

export default {
  components: {
    ActionHeader
  },
  computed: {
    ...mapState('vuex', ['storeCount']),
    currentInspectedStateIndex: {
      get () {
        return this.$store.state.vuex.inspectedStoreIndex
      },
      set (index) {
        this.$store.dispatch('vuex/changeStore', index)
      }
    }
  },
  methods: {
    ...mapActions('vuex', ['changeStore'])
  }
}
</script>

<style lang="stylus" scoped>
.available-stores-select {
  width: 250px;
}
</style>

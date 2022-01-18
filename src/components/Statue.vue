<template>
  <div>
    <table>
      <thead>
        <tr>
          <th>Id</th>
          <th>Person</th>
          <th>Height</th>
          <th>Price</th>
          <th>Operation</th>
        </tr>
      </thead>
      <tbody>
        <StatueItem
          v-for="statue in statues"
          v-bind:key="statue.id"
          :statue="statue"
        />
        <button v-if="mod_new" @click="newStatue" :disabled="saving">New</button>
      </tbody>
    </table>
    <!--<button @click="loadData">Load Data</button>-->
  </div>
</template>

<script>
import StatueItem from './StatueItem.vue'
export default {
  props: ['statues'],
  components: {StatueItem},
  methods: {
    /*Changed(e) {
        this.$emit('statue-item-changed', e)
    }*/
  }
}
</script>

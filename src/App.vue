<template>
  <Statue :statues="statues" />
</template>

<script>
import Statue from './components/Statue.vue'
export default {
  name: 'App',
  components: {Statue},
   data() {
    return {
      mod_new: true,
      saving: false,
      statue: {
          id: null,
          person: '',
          height: 0,
          price: 0
      },
      statues: []
    }
  },
  methods: {
    async loadData () {
      let Response = await fetch('http://127.0.0.1:8000/api/statues')
      let data = await Response.json()
      this.statues = data
    },
    async deleteStatue(id) {
      let Response = await fetch(`http://127.0.0.1:8000/api/statues/${id}`, {
          method: 'DELETE'
      })
      console.log(Response)
      await this.loadData()
    },
    async newStatue() {
      this.saving='disabled'
      await fetch('http://127.0.0.1:8000/api/statues', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
            'Accept': 'application/json'
        },
        body: JSON.stringify(this.statue) 
      })
      await this.loadData()
      this.saving=false
      this.resetForm()
    },
    async saveStatue() {
      this.saving='disabled'
      await fetch(`http://127.0.0.1:8000/api/statues/${this.statue.id}`, {
        method: 'PATCH',
        headers: {
            'Content-Type': 'application/json',
            'Accept': 'application/json'
        },
        body: JSON.stringify(this.statue) 
      })
    await this.loadData()
/*
      this.$emit('todo-item-changed', {
          original: this.statue,
          new: {
              person: this.statue.person,
              height: this.statue.height,
              price: this.statue.price
          },
      })
*/
        this.saving=false
        this.resetForm()
      },
      async editStatue(id) {
          let Response = await fetch(`http://127.0.0.1:8000/api/statues/${id}`)
          let data = await Response.json()
          this.statue = {...data};
          this.mod_new = false
      },
      cancelEdit () {
          this.resetForm()
      },
      resetForm() {
          this.statue = {
              id: null,
              person: '',
              height: 0,
              price: 0
          }
          this.mod_new = true
      }
    },
    mounted() {
        this.loadData()
    },
    Changed(e) {
      this.statues.map(function (statue) {
        if (statue.person != e.original.person) {
          return statue
        }
        if (statue.height != e.original.height) {
          return statue
        }
        if (statue.price != e.original.price) {
          return statue
        }
        statue.title = e.new.title
        statue.height = e.new.height
        statue.price = e.new.price
        return statue
      })
    }
  }

</script>

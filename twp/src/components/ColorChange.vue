<template>
<select @change="changeCol(evt)" :value='style' v-model='style'>
      <option v-for="item in items" :key="item" :class="item.style"> {{item.name}} </option>
</select>
</template>

<script>

export default {
  name: 'ColorChange',
  data () {
    return {
      items: [
        { name: 'rouge', style: 'red' },
        { name: 'blue', style: 'blue' },
        { name: 'vert', style: 'green' },
        { name: 'jaune', style: 'yellow' },
        { name: 'orange', style: 'orange' }
      ]
    }
  },
  methods: {
    changeCol (event) {
      this.items = event.target.value
      if (event) {
        event.preventDefault()
      }
      alert('message')
    }
  }
}
</script>
<style>
select{
  width:200px;
  height:2em;
  margin:1em;
  border-radius:8px;
}
</style>

<template>
  <div>
      <button id="btn" @click="deleteComment(comid)" class="btn btn-danger">Delete</button>
  </div>
</template>
<script>
import WPAPI from '@/api/WPAPI.js'
export default {
  props: [
    'comid'
  ],
  data () {
    return {
    }
  },
  methods: {
    deleteComment (id) {
      WPAPI.deleteComment(id)
        .then(function (response) {
          console.log(response)
          location.reload()
        })
    }
  }
}
</script>
<style scoped>
.btn{
  margin-left:1em;
  height:2em;
  border-radius:3px;
  background-color: rgb(189, 191, 217);
  font-weight: bold;
}
</style>

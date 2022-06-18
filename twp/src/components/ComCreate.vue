<template>
  <div>
    <input type='text' v-model='formComment.content' placeholder='Commentez...'/> <br>
    <button id="btn" @click="createComment()" class="btn btn-secondary">Commentez</button>
  </div>
</template>
<script>
import WPAPI from '@/api/WPAPI.js'
export default {
  props: [
    'po'
  ],
  data () {
    return {
      formComment: {
        post: this.po,
        content: '',
        karma: 0,
        approuved: '1'
      }
    }
  },
  methods: {
    createComment () {
      WPAPI.createComment(this.formComment)
        .then(function (response) {
          console.log(response)
          location.reload()
        })
    }
  }
}
</script>
<style scoped>
input{
  margin: .6em;
  width: 90%;
  height: 3em;
  border-radius:8px;
}
.btn{
  height:2em;
  border-radius:3px;
  background-color: rgb(189, 191, 217);
  font-weight: bold;
}
</style>

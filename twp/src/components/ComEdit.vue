<template>
  <div>
    <div id="back">
        <textarea class="textarea" v-model='formCom.content'></textarea><br>
        <button  v-on:click="editComment()" class="btn btn-danger">Edit</button>
        <button  class="btn btn-danger" @click="closeComm">X</button>
    </div>
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
      comment: [],
      formCom: {
        content: ''
      }
    }
  },
  methods: {
    editComment () {
      WPAPI.editComment(this.comid, this.formCom)
        .then(function (response) {
          console.log(response)
          location.reload()
        })
    },
    closeComm () {
      this.$emit('closeComm')
    }
  }
}
</script>
<style scoped>
#back {
  position :fixed;
  z-index: 999;
  text-align: center;
  width: 30%;
  height: 30%;
  display: table;
  transition: opacity 0.3s ease;
  background-color:white;
  background-color: #a1bdec;
  border-radius: 3px;
}
.textarea {
  width: 80%;
  height: 20%;
  margin:2em;
}
.btn{
  height:2em;
  border-radius:8px;
  background-color: rgb(189, 191, 217);
  font-weight: bold;
  margin-left:1em;
}
</style>

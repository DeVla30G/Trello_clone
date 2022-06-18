<template>
    <div>
        <div id="back">
            <div class="post">
              <div class="head-post">
                <span><button id="btnclose" class="btn btn-danger" @click="closePost">X</button>
                <button id="btn" @click="deletePost(po)" class="btn btn-danger">Delete</button>
                <button id="btn" @click="openEdit(po)" class="btn btn-secondary">
                <span v-if="showedit">Edit</span>
                <span v-else>Update</span></button></span>
                <div>
                </div>
                 </div>
                <p class="title"><strong>{{title}}</strong></p>
                <p v-html="description"></p>
    <div class="body-post">
                <EditPost v-if="showedit" :idedit='idedit'/>

                <p>Commentaires :</p>
                <div>
                  <CommentsShow v-bind:po='po'/>
                </div>
                <ComCreate v-bind:po='po'/>
            </div>
        </div>
      </div>
    </div>
</template>
s
<script>
import WPAPI from '@/api/WPAPI.js'
import EditPost from '@/components/EditPost.vue'
import CommentsShow from '@/components/CommentsShow.vue'
import ComCreate from '@/components/ComCreate.vue'
export default {
  components: {
    EditPost,
    CommentsShow,
    ComCreate
  },
  props: [
    'po'
  ],
  data () {
    return {
      description: '',
      title: '',
      idedit: '',
      showedit: false,
      showeditC: false,
      idc: '',
      coms: [],
      formc: {
        content: ''
      },
      formedit: {
        content: ''
      }
    }
  },
  mounted () {
    WPAPI.getpost(this.po)
      .then(response => {
        this.description = response.data.content.rendered
        this.title = response.data.title.rendered
      })
      .catch(error => {
        console.log('Error :', error.response)
      })
  },
  methods: {
    deletePost (id) {
      WPAPI.deletePost(id)
        .then(function (response) {
          console.log(response)
        })
    },
    closePost () {
      this.$emit('closePost')
    },
    openEdit (id) {
      if (this.showedit === true) {
        this.showedit = false
      } else {
        this.showedit = true
        this.idedit = id
      }
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
  height: 50%;
  display:inline-block;
  transition: opacity 0.3s ease;
  background-color:white;
  border-radius: 10px;
  top:0;

}
.head-post{
  background-color: #b266df;
  color:black;
  padding:1em;
}
.body-post{
 background-color: white;
 padding-bottom: 22px;
 margin: 30px;
 width:90%;
 align-content: center;
}
.title{
  text-align: left;
  font-size: 26px;
  font-weight:200;
  margin:.5em;
}
.btnclose{
float:right;
}
.btn{
  margin-left:1em;
  height:2em;
  border-radius:3px;
  background-color: transparent;
  font-weight: bold;
}
</style>

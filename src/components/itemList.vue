<template>
  <div>
    <ol class ="list" >
      <li v-for="(item,index) in show(this.$store.state.itemList)" v-bind:key="index" :class="{rackA:index%2==0}" >
        <input type="checkbox" @click="changeStatus(item)" v-bind:checked="item.isFinish" >
        <span v-if="!item.isEdit" v-bind:class="{itemIsFinish:item.isFinish}"  v-on:dblclick="changeToEdit(item)" >{{item.content}}</span>
        <input v-else  type="text" v-model="item.currentContent" v-on:keyup.enter="changeContent(item)" >
      </li>
    </ol>
  </div>
</template>

<script>
export default {
  name: 'itemList',
  props: {
    msg: String
  },
  data(){
      return {
          currentContent:null,
          selectTpye:'ALL',
          itemList:[]
      }
  },
  methods:{
      changeStatus:function(item){
          this.$store.commit("changeStatus",item);
      },
      show:function(list){
          this.selectTpye = this.$store.state.selectTpye;
          if(this.selectTpye == 'ALL') return list;
          else if(this.selectTpye == 'Active') return list.filter(item => !item.isFinish);
          else return list.filter(item => item.isFinish);
      },
      changeToEdit:function(item){
         this.$store.commit("changeToEdit",item);
         this.currentContent = item.content;
      },
      changeContent:function(item){
        //  this.$store.commit("changeContent",{item : item , currentContent : this.currentContent});
        this.$store.commit("changeContent",item);
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>

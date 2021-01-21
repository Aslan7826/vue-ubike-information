<template>
   <div class="right"> 
        分頁筆數:
        <select class="myMOUSE" v-model.number="pageSize" >
          <option v-for="size in 20" :key="size">{{size}}</option>
        </select>
      </div>
</template>
<script>
export default {
  props:{
    thePageSize:Number
  },
  data(){
    return {
      pageSize:this.thePageSize
    }
  },watch:{
    pageSize(val){
      this.$emit('ChangeSize',val);
    }
  }
}
</script>
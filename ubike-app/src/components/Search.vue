<template>
      <p>
        站點名稱搜尋: <input type="text" v-model="selectstr" @keyup="SelectStr" >
      </p>
</template>

<script>
export default {
  data(){
    return{
      selectstr:'',
    }
  },
  methods:{
    SelectStr(){
      this.$emit('GetStr',this.selectstr);
    }
  }
}
</script>
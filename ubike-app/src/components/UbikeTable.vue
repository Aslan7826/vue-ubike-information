<template>
  <table class="table table-striped">
    <thead>
      <tr>
        <th>#編號</th>
        <th>場站名稱</th>
        <th>場站區域</th>
        <th class="myMOUSE" @click="SetOrder('sbi')">
          目前可用車輛
          <i class="fa fa-sort-asc" aria-hidden="true"></i>
          <i class="fa fa-sort-desc" aria-hidden="true"></i>
        </th>
        <th class="myMOUSE" @click="SetOrder('tot')">
          總停車格
          <i class="fa fa-sort-asc" aria-hidden="true"></i>
          <i class="fa fa-sort-desc" aria-hidden="true"></i>
        </th>
        <th>資料更新時間</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="i in theTableData" 
          v-bind="i"
          :key="i.sno">
        <td>{{i.sno}}</td>
        <td>{{i.sna}}</td>
        <td>{{i.sarea}}</td>
        <td>{{i.sbi}}</td>
        <td>{{i.tot}}</td>
        <td>{{i.mday}}</td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  props: {
    theTableData: Array
  },
  data(){
    return{
      field:"sbi",
      order:true
    }
  },
  methods: {
    SetOrder(value) {
      this.order = !this.order;
      this.$emit('TableOrder',value,this.order);
    }
  },
};
</script>
<style scoped>
.myMOUSE {
  cursor: pointer;
}
</style>
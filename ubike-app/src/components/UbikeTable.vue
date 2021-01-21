<template>
  <table class="table table-striped">
    <thead>
      <tr>
        <th></th>
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
      <tr v-for="o in theTableData" 
          :key="o.sno"
          >
        <td><i class="fa myMOUSE" :class="o.showTop?'fa-star':'fa-star-o'" @click="click(o)"></i></td> 
        <td>{{o.sno}}</td>
        <td>{{o.sna}}</td>
        <td>{{o.sarea}}</td>
        <td>{{o.sbi}}</td>
        <td>{{o.tot}}</td>
        <td>{{o.mday}}</td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  props: {
    theTableData: Array,
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
    },
    click(obj){
      this.$emit('SelectObj',obj);
    }
  },
};
</script>
<style scoped>
.myMOUSE {
  cursor: pointer;
}
</style>
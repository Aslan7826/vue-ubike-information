<template>
  <div id="app">
    <div>
      <tag-search-page 
        @GetStr="ChangeSearch"
        ></tag-search-page>
      <tag-page-index 
        :thePageSize="pageSize" 
        @ChangeSize="ChangeSize"
        ></tag-page-index>
    </div>
    <div>
      <tag-u-bike-table 
        :theTableData="pageData" 
        @TableOrder="(fn,or)=>{field=fn; order=or}"
        @SelectObj="FunClick"
        ></tag-u-bike-table>
    </div>
    <div>
      <tag-pagination
        :thePageIndex="pageIndex"
        :thePageSize="pageSize"
        :theData="searchPage"
        @ChangeIndex="(o)=>pageIndex=o"
      ></tag-pagination>
    </div>
  </div>
</template>

<script>
import tagPageIndex from "./components/PageIndex";
import tagPagination from "./components/Pagination";
import tagSearchPage from "./components/Search";
import tagUBikeTable from "./components/UbikeTable";

export default {
  name: "App",
  components: {
    tagPageIndex,
    tagPagination,
    tagSearchPage,
    tagUBikeTable,
  },
  data() {
    return {
      uBikeStops: [],
      search:'',
      pageIndex: 0,
      pageSize: 10,
      field: "sbi",
      order: true,
    };
  },
  computed: {
    searchPage(){
      return this.FunPageSearch([...this.uBikeStops]);
    },
    pageData() {
      return this.FunPageSize(this.FunPageOrder(this.searchPage));
    }
  },
  methods: {
    FunPageSearch(list) {
      if (this.search != null) {
        return list.filter((o) => o.sna.includes(this.search));
      }
      return list;
    },
    FunPageOrder(list) {
      let func = this.order
        ? (a, b) => a[this.field] - b[this.field]
        : (a, b) => b[this.field] - a[this.field];
      return list.sort(func).sort((a,b)=>b.showTop-a.showTop);
    },
    FunPageSize(list) {
      const skipNum = this.pageIndex * this.pageSize;
      return list.slice(skipNum, skipNum + parseInt(this.pageSize));
    },
    FunClick(obj){
      obj.showTop = !obj.showTop;
    },
    ChangeSize(size){
      this.pageSize = size;
      this.PageIndexToZero();
    },
    ChangeSearch(search){
      this.search = search;
      this.PageIndexToZero();
    },
    PageIndexToZero(){
      this.pageIndex = 0;
      console.log(this.pageIndex);
    }
  },
  created() {
    fetch("https://tcgbusfs.blob.core.windows.net/blobyoubike/YouBikeTP.gz")
      .then((res) => res.json())
      .then((json) => {
        const stops = Object.keys(json.retVal)
        .map((key) => {
            var data = json.retVal[key] 
            data['showTop']=false
            return data;
           });
        this.uBikeStops = stops;
      });
  },
};
</script>
<style lang="scss">
@import "https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0-beta/css/bootstrap.min.css";
@import "https://stackpath.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css";
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  //    text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.right {
  float: right;
}
</style>

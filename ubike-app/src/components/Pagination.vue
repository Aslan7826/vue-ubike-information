<template>
  <ul class="pagination right">
    <li @click="ChangePageIndex(pIndex-1)">
      <a>&lt;</a>
    </li>
    <li v-for="page in showPage" @click="ChangePageIndex(page + pIndex - 1)" :key="page">
      <a v-show="showPageIndex(page+pIndex)" :class=" {active: page === 1}">{{page+pIndex}}</a>
    </li>
    <li @click="ChangePageIndex(pIndex+1)">
      <a>&gt;</a>
    </li>
  </ul>
</template>
<script>
export default {
  props: {
    thePageIndex: Number,
    thePageSize: Number,
    theData: Array,
  },
  data() {
    return {
      pIndex: this.thePageIndex,
      showPage: 5,
    };
  },
  computed: {
    pageCount() {
      return Math.ceil(this.theData.length / this.thePageSize);
    }

  },
  methods: {
    ChangePageIndex(value) {
      if (value < 0) {
        this.pIndex = 0;
      } else if (value > this.pageCount) {
        this.pIndex = this.pageCount;
      } else {
        this.pIndex = value;
      }
      this.$emit("ChangeIndex", this.pIndex);
    },
    showPageIndex(value) {
        return this.pageCount >= value;
    },
  },
};
</script>
<style scoped>
ul.pagination {
  display: inline-block;
  padding: 0;
  margin: 0;
}
ul.pagination li {
  display: inline;
}

ul.pagination li a {
  color: black;
  float: left;
  padding: 8px 16px;
  text-decoration: none;
  cursor: pointer;
}
ul.pagination li a.active {
  background-color: #4caf50;
  color: white;
}

ul.pagination li a:hover:not(.active) {
  background-color: #ddd;
}
</style>
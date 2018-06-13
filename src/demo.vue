<template>
  <div id="app">
    <vue-mescroll @up-callback ='getApiNewsoneList'>
      <div slot="down-html-content">sssefe</div>
      <ul id="data-list">
      	<li></li>
      </ul>
    </vue-mescroll>
  </div>
</template>

<script>
import VueMescroll from '../vue-mescroll'

export default {
  name: 'App',
  components: {
    VueMescroll
  },
  methods:{
  	getApiNewsoneList(mescroll,page) {
        api.getApiNewsoneList(page.num, (res) => {
//      	ajax 请求部分 根据自己的需求定义
            if (res.code == 1000) {
                if (page.num == 1) this.NewsoneList = [];
                if (res.data.length) {
                    this.NewsoneList = [...this.NewsoneList, ...res.data];
                }
                mescroll.endSuccess(res.data.length);  // 根据后台返回格式选取(官网有说明)
            } else {
                mescroll.endErr();	// 根据后台返回格式选取(官网有说明)
            }
        })
      }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

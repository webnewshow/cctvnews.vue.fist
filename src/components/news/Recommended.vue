<template>
  <div class="infinite-list-wrapper" style="overflow:auto">
    <ul class="list"  infinite-scroll-disabled="disabled">
      <li v-for="i in rec" class="list-item">
        <div class="newsMinBox">
          <h2>{{ i.title }}</h2>
          <p>{{i.time}}</p>
          <p class="NewsContent">{{i.content}}</p>
        </div>
      </li>
    </ul>
    <p v-if="loading">加载中...</p>
    <p v-if="noMore">没有更多了</p>
  </div>
</template>

<script>
// 引入 axios 
import axios from 'axios'
export default {
  data() {
    return {
      rec: [
        // {
        //   title: "微纪录片《潮涌东方 海纳百川》",
        //   time: "2019-11-07 08:25:01",
        //   content:
        //     "迎五洲客，计天下利！ 见证中国开放的大门越开越大！ 为上海点赞！为伟大习主席点赞！[赞][赞]"
        // },
        // {
        //   title: "心声、信心在掌声中交汇",
        //   time: "2019-11-07 05:22:21",
        //   content:
        //     "11月5日，上海国家会展中心会议大厅内灯光璀璨，座无虚席，来自世界各地的政商学研各界嘉宾聚集于此。国家主席习近平在这里出席第二届中国国际进口博览会开幕式并发表题为《开放合作命运与共》的主旨演讲。"
        // }
      ],
      loading: false
    };
  },
  mounted() {
    axios({
      method: "get",
      url: "http://127.0.0.1:3000/rec",
    }).then((res) => {
        if(res.status === 200){
             res=res.data;
             this.rec = res.data;
        }   
    })
  },
  computed: {
    noMore () {
        return this.rec.length >= 10
    },
    disabled() {
      return this.loading || this.noMore;
    }
  }
};
</script>

<style>
.newsMinBox {
  padding-left: 20px;
  padding-bottom: 10px;
  border-bottom: 1px solid #999;
}
.newsMinBox h2 {
  margin: 10px 0;
}
.NewsContent {
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 1;
  -webkit-box-orient: vertical;
}
</style>
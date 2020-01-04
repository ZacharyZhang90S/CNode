<template>
  <div id="postlist">
    <div class="loading" v-if="isLoading">
      <img src="../assets/loading.gif" alt="">
    </div>
    <div>
      <div class="bar_wrapper clearfix">
        <ul class="bar">
          <li>全部</li>
          <li>精华</li>
          <li>分享</li>
          <li>问答</li>
          <li>招聘</li>
          <li>客户端测试</li>
        </ul>
      </div>
      <div class="list_wrapper">
        <ul class="list">
          <li v-for="post in posts" :key="post.id">
            <img :src="post.author.avatar_url" alt="">
            <span>
                    <span class="reply_count">{{post.reply_count}}</span>
                    /{{post.visit_count}}
                  </span>
            <span>置顶</span>
            <span>内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容</span>
            <hr>
          </li>
        </ul>
      </div>
      

    
    </div>
    <div>
    
    </div>
  </div>
</template>

<script>
  export default {
    name: 'Postlist',
    data() {
      return {
        isLoading: '',
        posts: [],
      };
    },
    methods: {
      getData() {
        this.$http.get('https://cnodejs.org/api/v1/topics', {
          params: {
            page: 1,
            limit: 20,
          },
        })
          .then((res) => {
            this.isLoading = false;
            this.posts = res.data.data;
            // eslint-disable-next-line no-console
            console.log(this.posts);
          })
          .catch((err) => {
            // eslint-disable-next-line no-console
            console.log(err);
          });
      },
    },
    beforeMount() {
      this.isLoading = true;
      this.getData();
    },
  };
</script>

<style scoped>
  .clearfix::after {
    display: block;
    content: '';
    clear: both;
  }
  ul {
    list-style-type: none;
  }
  #postlist {
    margin-top: 15px;
    margin-left: 75px;
    width: 1065px;
  }
  .loading {
  }
  .bar_wrapper {
  }
  .bar {
    border-radius: 3px 3px 0 0;
    height: 40px;
    width: 100%;
    background: #f6f6f6;
    float: left;
    font-size: 13px;
    color: #8ebb39;
  }
  .bar > li {
    display: inline-block;
    min-width: 36px;
    height: 22px;
    margin-left: 20px;
    margin-top: 9px;
    text-align: center;
    line-height: 22px;
    /*background: #8ebb39;*/
  }
  .bar > li:hover {
    color: #1f557d;
    cursor: pointer;
  }
  .bar > li:first-child {
    color: #ffffff;
    background: #8ebb39;
    border-radius: 3px;
  }
  /*.bar > li.active{*/
  /*  color: #ffffff;*/
  /*  background: #8ebb39;*/
  /*}*/
  .list_wrapper{
  
  }
  .list {
    background: #ffffff;
    height: 600px;
  }
  .list>li>img{
    width: 30px;
    height: 30px;
    border-radius:3px;
    margin: 10px;
  }
  .list>li>span:nth-child(2){
    width: 50px;
  }
  .list>li>span:nth-child(2)>span{
  
  }
  .list>li>span:nth-child(3){
  
  }
  .list>li>span:nth-child(4){
  
  }
  
</style>
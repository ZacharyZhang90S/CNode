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
              /<span class="visit_count">{{post.visit_count}}</span>
             </span>
            <span :class="[{put_good:(post.good  == true),put_top:(post.top  == true),
        'topiclist-tab':(post.good  != true && post.top  != true)}]">{{post|tabFormatter}}</span>
            <span>{{post.title}}</span>
            <span class="comment_wrapper">
              <img :src="post.author.avatar_url" alt="">
              <span>{{post.last_reply_at|dateFormatter}}</span>
            </span>
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
    filters: {
      dateFormatter(str) {
        if (!str) return '';
        let date = new Date(str);
        let time = new Date().getTime() - date.getTime(); //现在的时间-传入的时间 = 相差的时间（单位 = 毫秒）
        if (time < 0) {
          return '';
        } else if ((time / 1000 < 30)) {
          return '刚刚';
        } else if (time / 1000 < 60) {
          return parseInt((time / 1000)) + '秒前';
        } else if ((time / 60000) < 60) {
          return parseInt((time / 60000)) + '分钟前';
        } else if ((time / 3600000) < 24) {
          return parseInt(time / 3600000) + '小时前';
        } else if ((time / 86400000) < 31) {
          return parseInt(time / 86400000) + '天前';
        } else if ((time / 2592000000) < 12) {
          return parseInt(time / 2592000000) + '月前';
        } else {
          return parseInt(time / 31536000000) + '年前';
        }
      },
      tabFormatter(post) {
        if (post.good == true) {
          return '精华';
        } else if (post.top == true) {
          return '置顶';
        } else if (post.tab == 'ask') {
          return '问答';
        } else if (post.tab == 'share') {
          return '分享';
        } else {
          return '招聘';
        }
      },
    },
  }
  ;
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
  .list_wrapper {
  }
  .list {
    background: #ffffff;
  }
  .list > li {
    border-bottom: 1px solid #f0f0f0;
    line-height: 50px;
    width: 100%;
    display: inline-block;
  }
  .list > li > img:first-of-type {
    width: 30px;
    height: 30px;
    border-radius: 3px;
    margin: 10px;
    vertical-align: top;
  }
  .list > li > span:nth-child(2) {
    width: 50px;
    font-size: 8px;
  }
  .list > li > span:nth-child(2) > span:nth-child(1) {
    font-size: 12px;
    color: #987bbc;
    font-weight: bold;
  }
  .list > li > span:nth-child(2) > span:nth-child(2) {
    font-size: 10px;
    color: #b4b4b4;
  }
  .list > li > span:nth-child(3) {
    font-size: 10px;
    margin: 0 10px;
    padding: 3px 4px;
    border-radius: 3px;
    color: #ffffff;
    background: #8ebb39;
  }
  .list > li > span:nth-child(4) {
    font-size: 18px;
  }
  .list > li > .comment_wrapper {
    float: right;
  }
  .list > li > .comment_wrapper > img {
    width: 18px;
    height: 18px;
    vertical-align: -3px;
    border-radius: 3px;
    margin-right: 10px;
  }
  .list > li > .comment_wrapper > span {
    margin-right: 10px;
    display: inline-block;
    width: 70px;
    color: #798086;
    font-size: 12px;
  }
</style>
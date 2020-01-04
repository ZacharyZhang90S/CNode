<template>
  <div class="header">
    <img src="../assets/cnodejs_light.svg" alt="">
    <ul>
      <li><a href="#">首页</a></li>
      <li><a href="#">新手入门</a></li>
      <li><a href="#">API</a></li>
      <li><a href="#">关于</a></li>
      <li><a href="#">注册</a></li>
      <li><a href="#">登录</a></li>
    </ul>
  </div>
</template>

<script>
  export default {
    name: 'Header',
  };
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  
  .header {
    height: 50px;
    background: #444;
  }
  img {
    max-width: 120px;
    margin-left: 50px;
    margin-top: 10px;
  }
  ul {
    list-style-type: none;
    float: right;
  }
  li {
    display: inline-block;
    font-size: 14px;
    padding: 18px 15px;
  }
  
  a{
    text-decoration: none;
    color: #cccccc;
    text-shadow: none;
  }
</style>

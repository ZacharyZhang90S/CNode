<template>
  <div id="app">
    <Header></Header>
    <Postlist></Postlist>
  </div>
</template>

<script>
  import Header from './components/Header';
  import Postlist from './components/Postlist';


  export default {
    name: 'app',
    components: {
      Header,
      Postlist,
    },
  };
</script>

<style>
  * {
    margin: 0;
    padding: 0;
  }
  body {
    background: #e1e1e1;
  }
</style>

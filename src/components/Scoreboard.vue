<template>
    <div class='scoreboard'>
        <div>{{score1}}</div>
        <div class='title'>
            SCOREBOARD - <h4 class='react-link'>See my React version <a href='http://supersmashrobros.surge.sh' target='_blank'  rel='noopener noreferrer'>here</a></h4>
        </div>
        <div>{{score2}}</div>
    </div>
</template>
<!--
---------------------------------
-->
<script>
    export default {
        props: ['score1', 'score2']
    }
</script>
<!--
---------------------------------
-->
<style>
  .scoreboard {
      width: 100%;
      height: 60px;
      margin: 20px 0;
      background: #000a;
      color: white;
      display: flex;
      justify-content: space-between;
      padding: 0 40px;
      align-items: center;
      margin-bottom: 60px;
  }

  .title {
      display: flex;
      flex-direction: column;
      align-items: center;
  }

  .react-link {
      color: #fff;
  }

  a {
      color: #ccc;
  }
</style>
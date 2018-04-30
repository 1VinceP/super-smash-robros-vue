<template>
    <div class='scoreboard'>
        <div>{{score1}}</div>
        <div>SCOREBOARD</div>
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
</style>
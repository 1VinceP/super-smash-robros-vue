<template>
<div class='main' id='app'>
  <header>
    <button @click='displayMonsters = false'>New Robro</button>
    <h1 class='title'>SUPER SMASH ROBROS</h1>
    <button @click='displayMonsters = true'>BATTLE!</button>
  </header>

  <scoreboard :score1='player1Score' :score2='player2Score' />

  <section class='create-monster' v-if='!displayMonsters'>
    <createmonster :addMonster='addMonster' />
  </section>

  <section v-else>
    <div class='player-monsters'>
      <monster class='player-monster' :monster='monster1' :player='1' :damage='damage1' :dead='false' :bonus='bonus1' />
      <button @click='fight' v-show='displayFight'>FIGHT</button>
      <monster class='player-monster' :monster='monster2' :player='2' :damage='damage2' :dead='false' :bonus='bonus2' />
    </div>

    <div class='display'>
      <div class='monsters'>
        <monster v-for='(monster, i) in monsters' :key='i' :monster='monster' :setOne='setOne' :setTwo='setTwo' :dead='monster.dead' />
      </div>
      <!-- <div class='items'></div> -->
    </div>

    <div class='add-super-robro' @click='addSuper' />
  </section>


</div>

</template>
<!--
---------------------------------
-->
<script>
  import CreateMonster from './components/CreateMonster';
  import Monster from './components/Monster.vue';
  import Scoreboard from './components/Scoreboard';
  import robots from './components/robots';

  export default {
    data() {
      return {
        displayMonsters: true,
        displayFight: false,

        player1Score: 0,
        player2Score: 0,

        monsters: robots,

        monster1: '',
        monster2: '',

        damage1: '',
        damage2: '',
        bonus1: '',
        bonus2: ''
      }
    },

    methods: {
      addMonster(name, color) {
        if( !name )
          return

        let tHealth = Math.floor(Math.random() * 30) + 1
        let strength = tHealth > 10 ? Math.floor(Math.random() * 4) + 2 : Math.floor(Math.random() * 5 + 6)
        let image = `http://robohash.org/${name}`

        let newMonster = {
          name,
          tHealth,
          cHealth: tHealth,
          strength,
          color,
          image
        }

        this.monsters.push( newMonster )
      },

      setOne( monster ) {
        if( monster === this.monster2 ) {
          this.monster2 = ''
          this.displayFight = false
        }
        this.monster1 = monster

        if( this.monster2 )
          this.displayFight = true
      },

      setTwo( monster ) {
        console.log( 'hit' )
        if( monster === this.monster1 ) {
          this.monster1 = ''
          this.displayFight = false
        }
        this.monster2 = monster

        if( this.monster1 )
          this.displayFight = true
      },

      fight() {
        console.log( this.monster1, this.monster2, 'hello' )
        const { monster1, monster2 } = this

        this.bonus1 = Math.floor(Math.random() * 4)
        this.bonus2 = Math.floor(Math.random() * 4)

        this.damage1 = monster2.strength + this.bonus2
        this.damage2 = monster1.strength + this.bonus1

        monster1.cHealth -= this.damage1
        monster2.cHealth -= this.damage2

        console.log( `${monster1.name} strength:`, monster1.strength + this.bonus1 )
        console.log( `${monster2.name} strength:`, monster2.strength + this.bonus2 )

        if( monster1.cHealth <= 0 ) {
          console.log( 'hit1' )
          this.displayFight = false
          monster1.dead = 'dead'
          setTimeout(() => {
            this.player2Score++
            this.monster1 = ''
            this.damage1 = ''
            this.damage2 = ''
            this.bonus1 = ''
            this.bonus2 = ''
          }, 3000);

        }
        if( monster2.cHealth <= 0 ) {
          console.log( 'hit2' )
          this.displayFight = false
          monster2.dead = 'dead'
          setTimeout(() => {
            this.player1Score++
            this.monster2 = ''
            this.damage1 = ''
            this.damage2 = ''
            this.bonus1 = ''
            this.bonus2 = ''
          }, 3000);

        }

        console.log( this.monsters )
      },

      addSuper() {
        let newMonster = {
          name: 'Vincent',
          tHealth: 100,
          cHealth: 100,
          strength: 100,
          color: 'background: radial-gradient(white, orange)',
          image: 'http://robohash.org/Vincent?set=set4'
        }

        this.monsters.push( newMonster )
      },

    },

    components: {
      createmonster: CreateMonster,
      monster: Monster,
      scoreboard: Scoreboard
    }
  }
</script>
<!--
---------------------------------
-->
<style>
  header {
    width: 100%;
    height: 30px;
    box-shadow: 0px 8px 12px #000a;
    display: flex;
    justify-content: space-around;
    align-items: center;
  }

  .main {
    width: 100%;
    height: auto;
    min-height: 100vh;
    background: linear-gradient(to bottom, #05abe0 0%,#53cbf1 60%,#87e0fd 100%);
  }

  .create-monster {
    /* height: 98vh; */
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-top: 60px;
  }

  .player-monsters {
    width: 100%;
    display: flex;
    justify-content: space-around;
    align-items: center;
    margin: 40px 0;
    padding: 0 200px;
    position: relative;
  }

  .damages {
    height: 100%;
    width: 100%;
    position: absolute;
    display: flex;
    justify-content: space-between;
    align-items: center;
    font-size: 60px;
    color: red;
  }

  .display {
    display: flex;
    justify-content: space-around;
    padding: 20px;
  }

  .monsters {
    width: 80%;
    display: flex;
    flex-wrap: wrap;
    /* padding: 20px; */
  }

  .items {
    height: 400px;
    width: 20%;
    background: white;
  }

  .add-super-robro {
    height: 100px;
    width: 100px;
    position: relative;
    bottom: 0;
    left: 0;
    background: transparent;
  }
</style>
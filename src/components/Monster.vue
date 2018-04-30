<template>
    <div :class='isDead'>
        {{checkDead()}}
        <div class='monster'>
            <div class='name'>{{monster.name}}</div>
            <div class='picture' :style='monster.color'>
                <img v-if='monster.image' :src='monster.image'/>
                <div v-show='damage' class='damage'>-{{damage}}</div>
                <div class='strength'>{{monster.strength}}</div> 
                <div v-if='bonus' class='strength-bonus'>+{{bonus}}</div>
                <div v-if='monster.cHealth < monster.tHealth' class='hurt'>{{monster.cHealth}}</div>
                <div v-else class='healthy'>{{monster.tHealth}}</div>
            </div>
            <section v-if='!player' class='buttons'>
                {{player}}
                <button class='button1' @click='setOne(monster)' :disabled='dead === "dead"'>1</button>
                <button class='button2' @click='setTwo(monster)' :disabled='dead === "dead"'>2</button>
            </section>
            <section v-else class='not-buttons'>
                Player {{player}}
            </section>
        </div>
    </div>
</template>
<!--
---------------------------------
-->
<script>
    export default {
        props: ['monster', 'setOne', 'setTwo', 'player', 'damage', 'dead', 'bonus'],
        data() {
            return {
                isDead: 'alive'
            }
            
        },
        methods: {
            checkDead() {
                this.isDead = this.dead
            }
        }
    }
</script>
<!--
---------------------------------
-->
<style>
    .dead {
        height: 200px;
        width: 150px;
        margin-right: 20px;
        color: #888 !important;
        margin-bottom: 10px;
    }
    .dead img {
        height: 157px;
        width: 150px;
        position: absolute;
        background: black;
        z-index: 2;
    }

    .monster {
        height: 200px;
        width: 150px;
        box-shadow: 3px 3px 6px rgba( 0, 0, 0, 0.6 );
        margin-right: 20px;
        margin-bottom: 10px;
        background: white;
    }

    .name {
        width: 100%;
        height: 22px;
        background: #ff0;
        display: flex;
        justify-content: center;
        align-items: center;
        box-shadow: 0px 2px 3px -1px rgba( 0, 0, 0, 0.6 );
        text-shadow: 2px 2px 3px #0009;
        position: relative;
        z-index: 3;
    }

    .picture {
        height: 157px;
        width: 150px;
        position: relative;
    }
    .picture > img {
        height: 100%;
        width: 100%;
    }

    .damage {
        position: absolute;
        top: 20px;
        left: 20px;
        font-size: 40px;
        color: red;
    }

    .strength {
        width: 30px;
        height: 32px;
        background: #ca0000;
        color: white;
        border-radius: 50%;
        display: flex;
        justify-content: center;
        align-items: center;
        position: absolute;
        bottom: 1px;
        left: 1px;
        border: 1px solid black;
    }

    .strength-bonus {
        width: 30px;
        height: 32px;
        background: #07ca00;
        color: white;
        border-radius: 50%;
        display: flex;
        justify-content: center;
        align-items: center;
        position: absolute;
        bottom: 1px;
        left: 34px;
        border: 1px solid black;
    }

    .healthy {
        width: 30px;
        height: 32px;
        background: #10108b;
        color: white;
        border-radius: 3px;
        display: flex;
        justify-content: center;
        align-items: center;
        position: absolute;
        bottom: 1px;
        right: 1px;
        border: 1px solid black;
    }

    .hurt {
        width: 30px;
        height: 32px;
        background: #10108b;
        font-weight: 800;
        color: rgb(255, 66, 32);
        border-radius: 3px;
        display: flex;
        justify-content: center;
        align-items: center;
        position: absolute;
        bottom: 1px;
        right: 1px;
        border: 1px solid black;
    }

    .buttons {
        display: flex;
    }

    .button1 {
        width: 50%;
        background: orange;
    }
    .button2 {
        width: 50%;
        background: greenyellow;
    }

    .not-buttons {
        width: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
        background: black;
        color: white;
        height: 21px;
    }
</style>
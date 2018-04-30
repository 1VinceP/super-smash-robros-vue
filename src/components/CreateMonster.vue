<template>
    <div>
        {{selectColor()}}
        <input class='create-name' @keydown.enter='handleAddMonster(name)' v-model='name' placeholder="Enter a name" /> <br>
        <div class='colors'>
            <div class='color' id='green' @click='setColor("green")'></div>
            <div class='color' id='yellow' @click='setColor("yellow")'></div>
            <div class='color' id='red' @click='setColor("red")'></div>
            <div class='color' id='blue' @click='setColor("blue")'></div>
        </div>
        Your robot will be given a random  image and a random amount of health and strength upon creation <br>
        <button class='create-button' @click='handleAddMonster(name)'>Create Robot</button> <br>
    </div>
</template>
<!--
---------------------------------
-->
<script>
    export default {
        props: ['addMonster'],
        data() {
            return {
                name: '',
                color: '',
                selected: ''
            }
        },
        methods: {
            handleAddMonster() {
                this.addMonster(this.name, this.color)
                this.name = ''
            },

            setColor( color ) {
                this.selected = color
                this.color = `background: radial-gradient(white, ${color})`
            },

            selectColor() {
                let classes = document.getElementsByClassName('color')
                
                for( let i = 0; i < classes.length; i++ ) {
                    if( classes[i].id === this.selected )
                        document.getElementById( this.selected ).style.border = '3px solid #0f0'
                    else
                        document.getElementById( classes[i].id ).style.border = 'none'
                }
            }
        }
        
    }
</script>
<!--
---------------------------------
-->
<style>
    .create-name {
        width: 100%;
        height: 40px;
        border-radius: 5px;
        font-size: 30px;
        padding-left: 10px;
    }

    .colors {
        display: flex;
        justify-content: space-between;
    }

    .color {
        height: 157px;
        width: 150px;
        border: 1px solid black;
        box-shadow:  3px 3px 6px rgba( 0, 0, 0, 0.6 );
        margin: 20px 0;
    }

    .create-button {
        width: 100%;
        height: 30px;
        border-color: green;
        border-radius: 5px;
        background: #0f0;
        font-size: 20px;
    }

    #green {
        background: radial-gradient(white, green);
    }

    #yellow {
        background: radial-gradient(white, yellow);
    }

    #red {
        background: radial-gradient(white, red);
    }

    #blue {
        background: radial-gradient(white, blue);
    }
</style>
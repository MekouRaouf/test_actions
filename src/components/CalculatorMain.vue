<template>
    <main>
        <div id="container">
            <div class="row">
                <h1>Raouf Lumiere</h1>
            </div>
            <div class="row clearfix">
                <input type="text" id="screen" :value="screenVal">
                <button id="clear" @click="clearScreen()">AC</button>
            </div>
            <div class="row clearfix">
                <button id="number" @click="pushVal(1)">1</button>
                <button id="number" @click="pushVal(2)">2</button>
                <button id="number" @click="pushVal(3)">3</button>
                <button data-operator="+" class="operator" @click="pushOp('+')">+</button>
            </div>
            <div class="row clearfix">
                <button id="number" @click="pushVal(4)">4</button>
                <button id="number" @click="pushVal(5)">5</button>
                <button id="number" @click="pushVal(6)">6</button>
                <button data-operator="-" class="operator" @click="pushOp('-')">-</button>
            </div>
            <div class="row clearfix">
                <button id="number" @click="pushVal(7)">7</button>
                <button id="number" @click="pushVal(8)">8</button>
                <button id="number" @click="pushVal(9)">9</button>
                <button data-operator="*" class="operator" @click="pushOp('*')">*</button>
            </div>
            <div class="row clearfix">
                <button id="decimal" @click="pushPoint()">.</button>
                <button id="number" @click="pushVal(0)">0</button>
                <button id="equals" @click="equate()">=</button>
                <button data-operator="/" class="operator" @click="pushOp('/')">/</button>
            </div>
        </div>
    </main>
</template>

<script setup>
    import { ref, onMounted } from 'vue';

    var datas = [0]
    var screenVal = ref('')
    var total = 0

    const displayScreen = () => {
        var val = ''

        datas.forEach(elt => {
            val += elt
        })

        return val
    }

    const pushVal = (val) => {
        let len = datas.length - 1

        if(datas[len] == '+' || datas[len] == '-' || datas[len] == '/' || datas[len] == '*'){
            datas.push(val)
        } else {
            datas[len] = parseInt(datas[len] + '' + val)
        }
        screenVal.value = displayScreen()
    }

    const pushOp = (op) => {
        datas.push(op)
        screenVal.value = displayScreen()
    }

    const clearScreen = () => {
        datas = [0]
        screenVal.value = ''
    }

    // const equate = () => {
    //     datas.forEach(elt => {
    //         if(elt == '+'){
    //             val += 
    //         }
    //     })
    // }

    onMounted(() => {
        datas.value = []
    })
</script>

<style lang="css">
*{
    box-sizing: border-box;
    padding: 0;
    margin: 0;
    font-weight: 300;
    font-family: 'Roboto', sans-serif;
}

body{
    background: #222;
}

main{
    background-color: #222;
    display: flex;
    justify-content: center;
    padding: 70px 0;
}

main #container{
    background-color: #333;
    box-shadow: 0 5px 5px black;
    padding: 10px;
}

#container .row h1 {
    -webkit-background-clip: text;
    background-clip: text;
    background-image: linear-gradient(to right bottom, bisque, #777);
    color: transparent;
    font-size: 20px;
    letter-spacing: 2px;
    text-align: right;
}

.clearfix:after {
    clear: both;
    content: " ";
    display: block;
    font-size: 0;
    height: 0;
    visibility: hidden;
}

#container .row:not(:last-child){
    margin-bottom: 10px;
}

#container input,
#container button{
    float: left;
}

#container input:focus,
#container button:focus{
    outline: none;
}

#container input{
    background-color: #222;
    border: 1px solid bisque;
    border-right-width: 0;
    color: #999;
    font-size: 20px;
    font-weight: 300;
    height: 80px;
    padding-right: 14px;
    text-align: right;
    width: 261px;
}

#container button{
    background-color: #222;
    border: none;
    box-shadow: 0 2px 0 #111;
    color: #999;
    font-size: 20px;
    height: 80px;
    width: 80px;
    margin-right: 7px;  
}

#container button:active {
    box-shadow: 0 2px 0 #111;
    transform: translateY(2px);
}

#container #clear,
#container .operator,
#container #equals {
    color: #111;
}

#container #clear,
#container .operator {
    margin-right: 0;
}

#container #clear {
    background-color: #e95a4b;
    border: 1px solid #999;
    border-left-width: 0;
    box-shadow: none;
    cursor: pointer;
}

#container #clear:active {
    box-shadow: none;
    transform: none;
}

#container .operator {
    background-color: #999;
    box-shadow: 0 3px 0 #555;
}

#container .operator:active {
    box-shadow: 0 2px 0 #555;
}

#container #equals {
    background-color: #2ecc71;
    box-shadow: 0 3px 0 #155d34;
}

#container #equals:active {
    box-shadow: 0 2px 0 #155d34;
}
</style>
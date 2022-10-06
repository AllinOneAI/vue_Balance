<script>
    import { ethers } from "./lib/ethers-5.6.esm.min.js"
    let pattern="^0x[a-fA-F0-9]{40}$"
    const provider = new ethers.providers.InfuraProvider("goerli", "dfbf0e548d9d496bae0e3f6fc91cb0a8");
    const reg = new RegExp(pattern);

    export default{
        data() {
            return {
                inputAddress: "0x0000000000000000000000000000000000000000",
                disabled: false,
            }
        },

        methods: {
            async checkBalance() {
                const amount = await provider.getBalance(this.inputAddress)
                alert(`There is ${ethers.utils.formatEther(amount)} GETH\nOn ${this.inputAddress}`)
            }
        },

        watch:{
            inputAddress() {
                if (!reg.test(this.inputAddress)){
                    this.disabled = true;
                } else {
                    this.disabled = false;
                } 
            }
        }
    }

</script>

<template>
    <div class="body">
       <h1 class="headline">Görli Balance</h1>
       <input v-model="inputAddress"><br><br>
       <button class="button-85" role="button" :disabled="disabled" @click="checkBalance">Check</button>
    </div>
</template>

<style>

.button-85 {
  width: 200px;
  height: 50px;
  padding: 0.6em 2em;
  border: none;
  outline: none;
  color: rgb(255, 255, 255);
  background: #111;
  cursor: pointer;
  position: relative;
  z-index: 0;
  border-radius: 10px;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
}

.button-85:before {
  content: "";
  background: linear-gradient(
    45deg,
    #ff0000,
    #ff7300,
    #fffb00,
    #48ff00,
    #00ffd5,
    #002bff,
    #7a00ff,
    #ff00c8,
    #ff0000
  );
  position: absolute;
  top: -2px;
  left: -2px;
  background-size: 400%;
  z-index: -1;
  filter: blur(5px);
  -webkit-filter: blur(5px);
  width: calc(100% + 4px);
  height: calc(100% + 4px);
  animation: glowing-button-85 10s linear infinite;
  transition: opacity 0.3s ease-in-out;
  border-radius: 10px;
}

@keyframes glowing-button-85 {
  0% {
    background-position: 0 0;
  }
  50% {
    background-position: 400% 0;
  }
  100% {
    background-position: 0 0;
  }
}

.button-85:after {
  z-index: -1;
  content: "";
  position: absolute;
  width: 100%;
  height: 100%;
  background: #222;
  left: 0;
  top: 0;
  border-radius: 10px;
}

.button-85:disabled{
    color: black;
    background: black;
}

    input{
        
        width: 50%;
        color: rgb(36, 35, 42);
        font-size: 16px;
        line-height: 20px;
        min-height: 28px;
        border-radius: 4px;
        padding: 8px 16px;
        border: 2px solid transparent;
        background: rgb(251, 251, 251);
        transition: all 0.1s ease 0s;
        box-shadow: rgba(255, 255, 255, 0.449) 0px 0px 50px 10px
    }

    .body{
        margin: auto;
        background-color: black;
    }
    .headline {   
	    animation: color-change 1s infinite alternate;
    }
    @keyframes color-change {
    0% { color: red; }
    50% { color: blue; }
    75% { color: greenyellow; }
    100% { color:blueviolet; }
}
</style>
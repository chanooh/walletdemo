<template>
  <div class="wrapper">
    <h1>Wallet App</h1>
    <div v-if="!address">
      <button @click="createWallet">Create Wallet</button>
    </div>
    <div v-else>
      <p>Account: {{ address }}</p>
      <p>Balance: {{ balance }} ETH</p>
      <button @click="transferETH">Transfer ETH</button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import Web3 from 'web3' 

const web3 = new Web3('https://goerli.infura.io/v3/3574e6df6bb64c9fb8260345c1f53848')
//pk: 0xdf45799c2fe5d1e804d13c092947a2319310ecad64d86204660c4854c346a5a6
//add:0xaa89533F9a84bb11a17570b9701C94dD7A2ddc77
const address = ref('')
if(localStorage.getItem('address')) {
  address.value = ref(localStorage.getItem('address'))
}

const balance = ref(0)
// balance.value = await web3.eth.getBalance(address.value)
web3.eth.getBalance(address.value).then((res) =>{
  balance.value = res;
});
console.log(balance.value);

async function createWallet() {
  console.log(web3)
  const accounts = web3.eth.accounts.create("123")
  console.log(accounts)
  address.value = accounts.address
  localStorage.setItem('address', address.value)
  localStorage.setItem('privateKey', accounts.privateKey)
}
async function transferETH() {

}

</script>

<style scoped>
.wrapper{
  width: 360px;
  height: 600px;
}
</style>

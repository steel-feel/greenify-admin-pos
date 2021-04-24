<script>
	export let balance,sAccountNo;
	import { ethStore } from 'svelte-web3';

	ethStore.setBrowserProvider();
	let iallow;
	var web33 = new window.Web3(Web3.givenProvider);


	const contractAbi = [
		{
			anonymous: false,
			inputs: [
				{
					indexed: true,
					internalType: "address",
					name: "owner",
					type: "address",
				},
				{
					indexed: true,
					internalType: "address",
					name: "spender",
					type: "address",
				},
				{
					indexed: false,
					internalType: "uint256",
					name: "value",
					type: "uint256",
				},
			],
			name: "Approval",
			type: "event",
		},
		{
			anonymous: false,
			inputs: [
				{
					indexed: true,
					internalType: "address",
					name: "from",
					type: "address",
				},
				{
					indexed: true,
					internalType: "address",
					name: "to",
					type: "address",
				},
				{
					indexed: false,
					internalType: "uint256",
					name: "value",
					type: "uint256",
				},
			],
			name: "Transfer",
			type: "event",
		},
		{
			inputs: [
				{
					internalType: "address",
					name: "spender",
					type: "address",
				},
				{
					internalType: "uint256",
					name: "amount",
					type: "uint256",
				},
			],
			name: "approve",
			outputs: [
				{
					internalType: "bool",
					name: "",
					type: "bool",
				},
			],
			stateMutability: "nonpayable",
			type: "function",
		},
		{
			inputs: [
				{
					internalType: "address",
					name: "spender",
					type: "address",
				},
				{
					internalType: "uint256",
					name: "subtractedValue",
					type: "uint256",
				},
			],
			name: "decreaseAllowance",
			outputs: [
				{
					internalType: "bool",
					name: "",
					type: "bool",
				},
			],
			stateMutability: "nonpayable",
			type: "function",
		},
		{
			inputs: [
				{
					internalType: "address",
					name: "spender",
					type: "address",
				},
				{
					internalType: "uint256",
					name: "addedValue",
					type: "uint256",
				},
			],
			name: "increaseAllowance",
			outputs: [
				{
					internalType: "bool",
					name: "",
					type: "bool",
				},
			],
			stateMutability: "nonpayable",
			type: "function",
		},
		{
			inputs: [
				{
					internalType: "address",
					name: "recipient",
					type: "address",
				},
				{
					internalType: "uint256",
					name: "amount",
					type: "uint256",
				},
			],
			name: "transfer",
			outputs: [
				{
					internalType: "bool",
					name: "",
					type: "bool",
				},
			],
			stateMutability: "nonpayable",
			type: "function",
		},
		{
			inputs: [
				{
					internalType: "address",
					name: "sender",
					type: "address",
				},
				{
					internalType: "address",
					name: "recipient",
					type: "address",
				},
				{
					internalType: "uint256",
					name: "amount",
					type: "uint256",
				},
			],
			name: "transferFrom",
			outputs: [
				{
					internalType: "bool",
					name: "",
					type: "bool",
				},
			],
			stateMutability: "nonpayable",
			type: "function",
		},
		{
			inputs: [
				{
					internalType: "string",
					name: "name_",
					type: "string",
				},
				{
					internalType: "string",
					name: "symbol_",
					type: "string",
				},
			],
			stateMutability: "nonpayable",
			type: "constructor",
		},
		{
			inputs: [
				{
					internalType: "address",
					name: "owner",
					type: "address",
				},
				{
					internalType: "address",
					name: "spender",
					type: "address",
				},
			],
			name: "allowance",
			outputs: [
				{
					internalType: "uint256",
					name: "",
					type: "uint256",
				},
			],
			stateMutability: "view",
			type: "function",
		},
		{
			inputs: [
				{
					internalType: "address",
					name: "account",
					type: "address",
				},
			],
			name: "balanceOf",
			outputs: [
				{
					internalType: "uint256",
					name: "",
					type: "uint256",
				},
			],
			stateMutability: "view",
			type: "function",
		},
		{
			inputs: [],
			name: "decimals",
			outputs: [
				{
					internalType: "uint8",
					name: "",
					type: "uint8",
				},
			],
			stateMutability: "view",
			type: "function",
		},
		{
			inputs: [],
			name: "name",
			outputs: [
				{
					internalType: "string",
					name: "",
					type: "string",
				},
			],
			stateMutability: "view",
			type: "function",
		},
		{
			inputs: [],
			name: "symbol",
			outputs: [
				{
					internalType: "string",
					name: "",
					type: "string",
				},
			],
			stateMutability: "view",
			type: "function",
		},
		{
			inputs: [],
			name: "totalSupply",
			outputs: [
				{
					internalType: "uint256",
					name: "",
					type: "uint256",
				},
			],
			stateMutability: "view",
			type: "function",
		},
	];

	var contract = new web33.eth.Contract(contractAbi, "0xb8Fb19A9CD495EDC6Fa3dD6fDB0Fa95ABF10271F");


	web33.eth.getAccounts(function(error, accounts) {
  if (error) throw error;
  // Make the contract call.
  sAccountNo = accounts[0];

  console.log(sAccountNo);
  window.sAccountNo = accounts[0];

  contract.methods.balanceOf(sAccountNo).call(function(error, result) {
  if (error) throw error;

  balance = result;
	


});



contract.methods.allowance( "0xb8Fb19A9CD495EDC6Fa3dD6fDB0Fa95ABF10271F" ,sAccountNo).call(function(error, result) {
  if (error) throw error;

  iallow = result;
});



});











let amount, transferaddress, message;

function onTransfer(){
	//contract.methods.
	console.debug(web33.utils.isAddress(transferaddress), amount,transferaddress);

	contract.methods.approve(window.sAccountNo, +amount).send({from : sAccountNo},function(error, result) {

		if(error) throw error;

		console.log("result1:" + result )

		contract.methods.transferFrom(window.sAccountNo ,transferaddress, +amount).send({from : sAccountNo},function(error, result) {
			if(error) throw error;
			message = result;
			console.log("result2:" + result )
		});

		

});
}

function newTranfer(){
	contract.methods.transfer(transferaddress, +amount).send({from : sAccountNo},function(error, result) {
		if(error) throw error;
			message = result;
		

	})
}


function inAllowace(){

	

	contract.methods.increaseAllowance(sAccountNo, 100).send({from : sAccountNo},function(error, result) {
		if(error) throw error;

				console.log("allowane:" + result )
	});
	

}





</script>

<main>
	<h1>Hello Admin/POS Test</h1>
	<p>TEST POD/ Admin application to check reward system  enter the amount and address of user to check for rewards. </p>
	<p>Need Ropsten to be selected in Metamask</p>

	<p>Use Below account for testing, import this account via PRIVATE KEY in Metmask, At time of config it had <strong>111 GTK</strong></p>
	<p> address: 0xcbF9Df641606fC0F2247869180bdD3181Ae51370

	 </p>
	 <p>private KEY : 35eeb2e4735b14ffcabdcc2687699d74511634218d46a3f278a8b9f9aade88e3 </p>

	<h1> Current Balance {balance}</h1>

	<div>
		Enter Trasfer amount
		<input type="text" bind:value="{amount}" >
	</div>

	<div>
		Enter Address
		<input type="text" bind:value="{transferaddress}" >
	</div>

	<button on:click="{newTranfer}" >Transfer reward to address</button>

	<p>Transaction No.: {message} </p>
	<p>It will take some time to settle the amount as its a testnet. Look out for messages by metamask.</p>

</main>

<style>
	.p1{
		padding: 1em;
	}
	.p5{
		padding: 1em;
	}

	.m5{
		margin: 5em;
	}


	.m2{
		margin: 2em;
	}

	div {
		margin: 2em;
	}

</style>
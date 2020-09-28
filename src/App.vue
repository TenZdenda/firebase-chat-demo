<template>
  <div id="app">
    <div>
			<div class="card" v-for="msg in messages" :key="msg.message">
				<strong>{{ msg.nickname }}</strong>
				<p class="message">{{ msg.text }}</p>
			</div>

			<div class="type">
				<input type="text" name="nickname" v-model="message.nickname" placeholder="Zadej svoje jméno" required>
				<textarea name="area-message" id="textarea-message" cols="30" rows="10" v-model="message.text" required></textarea>
				<button @click="storeMessage">Odeslat</button>
			</div>
	</div>
  </div>
</template>

<script>

import * as firebase from 'firebase'

const firebaseConfig = {
	// Insert firebase config
};

// Initialize Firebase
firebase.initializeApp(firebaseConfig);
const database = firebase.database()

export default {
  name: 'App',
  data() {
		return {
			messages: [],
			message: {
				nickname: '',
				text: '',
			}
		}
	},
	methods: {
		storeMessage() {
			database.ref('messages').push(this.message)
			this.message.text = ''
		}
	},
	created() {
		database.ref('messages').on('child_added', snapshot => this.messages.push(snapshot.val()))
	}
}
</script>
<style>
	.card {
		padding: 15px 30px;
		border: 1px solid gray;
		margin-bottom: 10px;
	}

	.type {
		width: 100%;
	}

	.type input {
		display: block;
		border: none;
		border-bottom: 1px solid black;
		margin: 20px 0px;
		outline: none;
		padding: 3px;
	}

	.type textarea {
		display: block;
		width: 100%;
		margin: 30px 0px;
	}

	.type button {
		background: blue;
		color: white;
		padding: 10px 20px;
		border-radius: 2px;
		border: none;
	}

	.type button:hover {
		background: blueviolet;
	}
</style>

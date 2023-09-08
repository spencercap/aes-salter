<template>
	<p>
		Salter
	</p>

	<hr />
	<h1>encrypt</h1>
	<div>
		<div>
			to encrypt
		</div>
		<input v-model="stuff" type="text" placeholder="stuff">
	</div>
	<div>
		<div>
			salt
		</div>
		<input v-model="salt" type="text" placeholder="salt">
	</div>
	<button @click="doEncrypt">doEncrypt</button>
	<div>
		<div>
			result
		</div>
		<textarea v-model="result" name="" id="" cols="30" rows="10"></textarea>
	</div>


	<hr />
	<h1>decrypt</h1>
	<div>
		<div>
			to decrypt
		</div>
		<input v-model="stuff" type="text" placeholder="stuff">
	</div>
	<div>
		<div>
			salt
		</div>
		<input v-model="salt" type="text" placeholder="salt">
	</div>
	<button @click="doDecrypt">doDecrypt</button>
	<div>
		<div>
			result
		</div>
		<textarea v-model="result" name="" id="" cols="30" rows="10"></textarea>
	</div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

import CryptoJS from 'crypto-js';

export function encrypt(mnemonic: string, passphrase: string): string {
	return CryptoJS.AES.encrypt(mnemonic, passphrase).toString();
}
export function decrypt(encryptedMnemonic: string, passphrase: string): string {
	var bytes = CryptoJS.AES.decrypt(encryptedMnemonic, passphrase);
	return bytes.toString(CryptoJS.enc.Utf8);
}


export default defineComponent({
	data() {
		return {
			stuff: '',
			salt: '',
			result: ''
		}
	},
	methods: {
		doEncrypt() {
			console.log('doEncrypt');
			this.result = encrypt(this.stuff, this.salt);
		},
		doDecrypt() {
			console.log('doDecrypt');
			this.result = decrypt(this.stuff, this.salt);
		}
	}
});
</script>

<style scoped>

</style>

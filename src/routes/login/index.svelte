<script lang="ts">
	let email = '';
	let password = '';
	let isLoggedIn = false;

	import { initializeApp } from 'firebase/app';
	import { getAuth, signInWithEmailAndPassword } from 'firebase/auth';

	const firebaseConfig = {
		apiKey: 'AIzaSyAEQeBDIhVbap3VIhIj3aQ_SCcQ0mqMtaA',
		authDomain: 'fmt1-3cea5.firebaseapp.com',
		projectId: 'fmt1-3cea5',
		storageBucket: 'fmt1-3cea5.appspot.com',
		messagingSenderId: '967645557088',
		appId: '1:967645557088:web:bfe610efa1deca77adee05'
	};
	const app = initializeApp(firebaseConfig);

	const login = () => {
		const auth = getAuth(app);
		signInWithEmailAndPassword(auth, email, password)
			.then((userCredential) => {
				// Signed in
				const user = userCredential.user;
				isLoggedIn = true;
				// ...
			})
			.catch((error) => {
				const errorCode = error.code;
				const errorMessage = error.message;
			});
	};
</script>

<form on:submit|preventDefault={login} method="POST">
	@csrf
	<div class="form-group">
		<label for="email">Email</label>
		<input
			type="email"
			bind:value={email}
			class="form-control"
			id="email"
			name="email"
			placeholder="Enter email"
		/>
	</div>
	<div class="form-group">
		<label for="password">Password</label>
		<input
			type="password"
			class="form-control"
			id="password"
			name="password"
			placeholder="Password"
			bind:value={password}
		/>
	</div>
	<button type="submit" class="btn btn-primary">Submit</button>

	{#if isLoggedIn}
		<p>I am logged in, baby!</p>
	{/if}
</form>

<style>
</style>

<script>
	import { onMount } from 'svelte';
	import { auth } from '../lib/firebase/firebase.client';
	import { browser } from '$app/environment';
	import { authStore } from '../stores/authStore';
	onMount(() => {
		const unsubscribe = auth.onAuthStateChanged((user) => {
			console.log(user);
			authStore.update((curr) => {
				return { ...curr, isLoading: false, currentUser: user };
			});

			if (
				browser &&
				!$authStore?.currentUser &&
				!$authStore.isLoading &&
				window.location.pathname !== '/'
			) {
				window.location.href = '/';
				console.log(authStore.currentUser, authStore.isLoading);
			}
		});
		return unsubscribe;
	});
</script>

<main class="mainContainer">
	<slot />
</main>

<style>
	.mainContainer {
		min-height: 100vh;
		display: flex;
		flex-direction: column;
	}
</style>

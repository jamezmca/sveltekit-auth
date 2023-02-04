<script>
	import { authHandlers, authStore } from '../stores/authStore';

	let action = '';
	let newEmail = '';
	let newPass = '';

	async function handleSubmit() {
		if (!action) {
			return;
		}

		if (action === 'updatePass') {
			return await authHandlers.updatePassword(newPass);
		}

		if (action === 'updateEmail') {
            console.log(newEmail)
			return await authHandlers.updateEmail(newEmail);
		}
	}
</script>

<div class="container">
	<div>
		<button
			on:click={() => {
				action = 'updateEmail';
			}}>Update Email</button
		>
		<button
			on:click={() => {
				action = 'updatePass';
			}}>Update Password</button
		>
	</div>
	{#if action === 'updatePass'}
		<form>
			<label>
				<input bind:value={newPass} type="password" placeholder="New Password" />
			</label>

			<button on:click={handleSubmit}>Submit</button>
		</form>
	{/if}
	{#if action === 'updateEmail'}
		<form>
			<label>
				<input bind:value={newEmail} type="email" placeholder="New Email" />
			</label>
			<button on:click={handleSubmit}>Submit</button>
		</form>
	{/if}
</div>

<style>
	.container {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		flex: 1;
	}

	.container form {
		display: flex;
		flex-direction: column;
	}

	.container div {
		display: grid;
		grid-template-columns: repeat(2, minmax(0, 1fr));
	}
</style>

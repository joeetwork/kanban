<script lang="ts">
	import CreateModal from '$lib/createModal.svelte';
	import Ticket from '$lib/ticket.svelte';

	let tickets: Record<string, unknown>[] = [];

	function handleClick() {
		const newTicket = new Ticket({ target: document.body });
		tickets.push(newTicket);
	}
</script>

<CreateModal {handleClick} />
<div class="ticket-container">
	{#each tickets as ticket (ticket.id)}
		<div>{ticket}</div>
	{/each}
</div>

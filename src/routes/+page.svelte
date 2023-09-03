<script lang="ts">
	import CreateModal from '$lib/createModal.svelte';
	import Ticket from '$lib/ticket.svelte';

	let tickets: Record<string, unknown>[] = [];
	let about: string;

	function handleClick() {
		const newTicket = new Ticket({
			target: document.body,
			props: {
				about
			}
		});
		tickets.push(newTicket);
	}

	function handleChange(
		e: Event & {
			currentTarget: EventTarget & HTMLInputElement;
		}
	) {
		if (e.target instanceof HTMLInputElement) {
			about = e.target.value;
		}
	}
</script>

<CreateModal {handleChange} {handleClick} {about} />
<div class="ticket-container">
	{#each tickets as ticket (ticket.id)}
		<div>{ticket}</div>
	{/each}
</div>

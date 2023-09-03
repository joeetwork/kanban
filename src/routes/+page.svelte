<script lang="ts">
	import CreateModal from '$lib/createModal.svelte';
	import Ticket from '$lib/ticket.svelte';

	let tickets: { id: string; ticket: Ticket }[] = [];
	let about: string;
	let id: string;

	function generateRandomId() {
		id = Math.random().toString(16).slice(2);
	}

	function handleClick() {
		generateRandomId();
		const newTicket = {
			id,
			ticket: new Ticket({
				target: document.body,
				props: {
					about,
					id
				}
			})
		};
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
	{#each tickets as object (object.id)}
		<div>{object.ticket}</div>
	{/each}
</div>

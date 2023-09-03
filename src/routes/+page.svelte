<script lang="ts">
	import CreateModal from '$lib/createModal.svelte';
	import Ticket from '$lib/ticket.svelte';
	import { TipLink } from '@tiplink/api';

	let tickets: { tiplink: { publicKey: string; url: URL }; ticket: Ticket }[] = [];
	let about: string;
	let tiplink: { publicKey: string; url: URL };

	const tipLink: () => Promise<{ publicKey: string; url: URL }> = async () => {
		const tiplink = await TipLink.create();
		return { publicKey: tiplink.keypair.publicKey.toBase58(), url: tiplink.url };
	};

	async function handleClick() {
		tiplink = await tipLink();
		const newTicket = {
			tiplink,
			ticket: new Ticket({
				target: document.body,
				props: {
					about,
					linkAddress: tiplink.url.toString()
				}
			})
		};
		tickets.push(newTicket);
		console.log(tickets);
		
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
	{#each tickets as object (object.tiplink.publicKey)}
		<div>{object.ticket}</div>
	{/each}
</div>

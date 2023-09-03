<script lang="ts">
	export let about: string;
	export let handleClick: () => void;
	export let handleChange: (
		e: Event & {
			currentTarget: EventTarget & HTMLInputElement;
		}
	) => void;
</script>

<input bind:value={about} on:input={(e) => handleChange(e)} type="text" />
<button on:click={handleClick}> Add </button>

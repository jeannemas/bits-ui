<script lang="ts">
	import { melt } from "@melt-ui/svelte";
	import type { NextButtonEvents, NextButtonProps } from "../index.js";
	import { getCtx } from "../ctx.js";
	import { createDispatcher } from "$lib/internal/events.js";

	type $$Props = NextButtonProps;
	type $$Events = NextButtonEvents;

	export let asChild: $$Props["asChild"] = undefined;
	export let el: $$Props["el"] = undefined;

	const {
		elements: { nextButton },
		getAttrs,
	} = getCtx();

	const attrs = getAttrs("next-button");

	$: builder = $nextButton;
	$: Object.assign(builder, attrs);

	const dispatch = createDispatcher();
</script>

{#if asChild}
	<slot {builder} />
{:else}
	<button bind:this={el} use:melt={builder} type="button" {...$$restProps} on:m-click={dispatch}>
		<slot {builder} />
	</button>
{/if}

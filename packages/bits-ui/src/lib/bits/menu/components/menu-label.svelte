<script lang="ts">
	import { melt } from "@melt-ui/svelte";
	import { getGroupLabel } from "../ctx.js";
	import type { LabelProps } from "../index.js";

	type $$Props = LabelProps;

	export let asChild: $$Props["asChild"] = false;
	export let el: $$Props["el"] = undefined;

	const { groupLabel, id, getAttrs } = getGroupLabel();
	const attrs = getAttrs("label");

	$: builder = $groupLabel(id);
	$: Object.assign(builder, attrs);
</script>

{#if asChild}
	<slot {builder} />
{:else}
	<div bind:this={el} use:melt={builder} {...$$restProps}>
		<slot {builder} />
	</div>
{/if}

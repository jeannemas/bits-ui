<script lang="ts">
	import { melt } from "@melt-ui/svelte";
	import { setGroupCtx } from "../ctx.js";
	import type { GroupProps } from "../index.js";
	type $$Props = GroupProps;
	export let asChild: $$Props["asChild"] = false;
	export let el: $$Props["el"] = undefined;

	const { group, id, getAttrs } = setGroupCtx();
	const attrs = getAttrs("group");

	$: builder = $group(id);
	$: Object.assign(builder, attrs);
</script>

{#if asChild}
	<slot {builder} />
{:else}
	<div bind:this={el} use:melt={builder} {...$$restProps}>
		<slot {builder} />
	</div>
{/if}

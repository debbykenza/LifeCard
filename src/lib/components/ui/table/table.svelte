<script lang="ts">
	import type { HTMLTableAttributes } from "svelte/elements";
	import { cn, type WithElementRef } from "$lib/utils.js";

	let {
		ref = $bindable(null),
		class: className,
		children,
		...restProps
	}: WithElementRef<HTMLTableAttributes> = $props();
</script>

<div data-slot="table-container" class="relative w-full overflow-x-auto">
	<table bind:this={ref} data-slot="table" class={cn("w-full caption-bottom text-sm", className)} {...restProps}>
		{@render children?.()}
	</table>
</div>


	<!-- export function Root(Root: any) {
		throw new Error("Function not implemented.");
	}


	export function Header(Header: any) {
		throw new Error("Function not implemented.");
	}


	export function Row(Row: any) {
		throw new Error("Function not implemented.");
	}


	export function Head(Head: any) {
		throw new Error("Function not implemented.");
	}


	export function Body(Body: any) {
		throw new Error("Function not implemented.");
	}


	export function Cell(Cell: any) {
		throw new Error("Function not implemented.");
	}


	export function Root(Root: any) {
		throw new Error("Function not implemented.");
	}


	export function Header(Header: any) {
		throw new Error("Function not implemented.");
	}


	export function Row(Row: any) {
		throw new Error("Function not implemented.");
	}


	export function Head(Head: any) {
		throw new Error("Function not implemented.");
	}


	export function Body(Body: any) {
		throw new Error("Function not implemented.");
	}


	export function Cell(Cell: any) {
		throw new Error("Function not implemented.");
	}


	export function Header(Header: any) {
		throw new Error("Function not implemented.");
	} -->

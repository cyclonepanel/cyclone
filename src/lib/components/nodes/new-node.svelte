<script lang="ts">
	import { Button, buttonVariants } from '$lib/components/ui/button/index.js';
	import * as Dialog from '$lib/components/ui/dialog/index.js';
	import { Input } from '$lib/components/ui/input/index.js';
	import { Label } from '$lib/components/ui/label/index.js';
	import SelectPublicKey from '../misc/select-public-key.svelte';

	let { open = $bindable() } = $props();
	let publicKeyComboboxOpen = $state(false);
</script>

<Dialog.Root bind:open>
	<Dialog.Content class="sm:max-w-[425px]">
		<Dialog.Header>
			<Dialog.Title>Add node</Dialog.Title>
			<Dialog.Description>
				Put in connection details for your new node. Click add when you're done.
			</Dialog.Description>
		</Dialog.Header>
		<div class="grid gap-4 py-4">
			<div class="flex w-full flex-col gap-2.5">
				<Label for="node-name">Node Name</Label>
				<Input type="text" id="node-name" placeholder="e.g. MCServer" />
			</div>
			<div class="flex w-full flex-col gap-2.5">
				<Label for="public-key">Public Key</Label>
				<SelectPublicKey bind:open={publicKeyComboboxOpen} />
			</div>
		</div>
		<Dialog.Footer>
			<Button type="submit">Add node</Button>
		</Dialog.Footer>
	</Dialog.Content>
</Dialog.Root>

<script lang="ts">
	import { tick } from 'svelte';
	import { useId } from 'bits-ui';
	import { cn } from '$lib/utils.js';

	import Key from 'lucide-svelte/icons/key';

	import * as Popover from '$lib/components/ui/popover/index.js';
	import * as Command from '$lib/components/ui/command/index.js';
	import { buttonVariants } from '$lib/components/ui/button/index.js';

	let publicKeys = [
		{
			label: 'Public Key 1',
			id: '1'
		}
	];

	let { open = $bindable() } = $props();
	let id = $state('');

	const selectedKey = $derived(publicKeys.find((s) => s.id === id));

	// We want to refocus the trigger button when the user selects
	// an item from the list so users can continue navigating the
	// rest of the form with the keyboard.
	function closeAndFocusTrigger(triggerId: string) {
		open = false;
		tick().then(() => {
			document.getElementById(triggerId)?.focus();
		});
	}
	const triggerId = useId();
</script>

<Popover.Root bind:open>
	<Popover.Trigger
		id={triggerId}
		class={buttonVariants({
			variant: 'outline',
			size: 'sm',
			class: 'w-[150px] justify-start'
		})}
	>
		{#if selectedKey}
			<Key class="mr-2 size-4 shrink-0" />
			{selectedKey.label}
		{:else}
			Select a public key
		{/if}
	</Popover.Trigger>
	<Popover.Content class="w-[200px] p-0" side="right" align="start">
		<Command.Root>
			<Command.Input placeholder="Search public keys..." class="h-9 border-none" />
			<Command.List>
				<Command.Empty>No results found.</Command.Empty>
				<Command.Group>
					{#each publicKeys as key}
						<Command.Item
							value={key.id}
							onSelect={() => {
								id = key.id;
								closeAndFocusTrigger(triggerId);
							}}
						>
							<Key class={cn('mr-2 size-4', key.id !== selectedKey?.id && 'text-foreground/40')} />

							<span>
								{key.label}
							</span>
						</Command.Item>
					{/each}
				</Command.Group>
			</Command.List>
		</Command.Root>
	</Popover.Content>
</Popover.Root>

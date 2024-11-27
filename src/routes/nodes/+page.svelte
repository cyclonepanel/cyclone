<script>
	import NewNode from '$lib/components/nodes/new-node.svelte';
	import NodeCard from '$lib/components/nodes/node-card.svelte';
	import { Button } from '$lib/components/ui/button';

	import Plus from 'lucide-svelte/icons/plus';

	const PLACEHOLDER_NODE_DATA = { name: 'Node 1', hostname: 'node1.skyfall.net', id: '1' };

	let isOpen = $state(false);
</script>

<div class="flex w-full flex-col gap-2">
	<div class="flex">
		<h1 class="text-3xl font-bold">Nodes</h1>
		<Button variant="secondary" class="ml-auto flex items-center" onclick={() => (isOpen = true)}>
			<Plus />
			Create Node
		</Button>
		<NewNode bind:open={isOpen} />
	</div>

	<div class="mt-4 grid grid-cols-1 gap-4 sm:grid-cols-2 lg:grid-cols-3">
		<NodeCard data={PLACEHOLDER_NODE_DATA} />
	</div>
</div>

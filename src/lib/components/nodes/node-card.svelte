<script lang="ts">
	import * as Card from '$lib/components/ui/card/index.js';

	interface Data {
		name: string;
		hostname: string;
		id: string;
	}
	let { data }: { data: Data } = $props();
</script>

<a href="/nodes/{data.id}">
	<Card.Root>
		<Card.Header>
			<Card.Title class="text-md">{data.name}</Card.Title>
			<Card.Description>{data.hostname}</Card.Description>
		</Card.Header>
		<Card.Footer />
	</Card.Root>
</a>

<script lang="ts">
	import '../app.css';
	import * as Sidebar from '$lib/components/ui/sidebar/index.js';
	import AppSidebar from '$lib/components/layout/app-sidebar.svelte';
	import { ModeWatcher } from 'mode-watcher';

	let { children } = $props();
</script>

<ModeWatcher />
<Sidebar.Provider class="w-screen">
	<AppSidebar />
	<main class="w-full">
		<Sidebar.Trigger />
		<div class="flex-1 px-8 py-4">
			{@render children?.()}
		</div>
	</main>
</Sidebar.Provider>

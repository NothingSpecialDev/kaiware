<script lang="ts">
	import Console from '$/routes/Console.svelte';
	import { device } from '$lib/stores/device';
	import View from '$lib/ui-components/view/View.svelte';
	import ViewContent from '$lib/ui-components/view/ViewContent.svelte';
	import ViewHeader from '$lib/ui-components/view/ViewHeader.svelte';
	import Router, { link, location, replace } from 'svelte-spa-router';
	import Elements from './Elements.svelte';
	import Logs from './Logs.svelte';
	import Network from './Network.svelte';
	import Storage from './Storage.svelte';

	if ($location === '/dev-tools') {
		replace('/dev-tools/elements');
	}

	const prefix = '/dev-tools';
	const routes = {
		'/elements': Elements,
		'/logs': Logs,
		'/network': Network,
		'/storage': Storage,
		'/console': Console
	};
</script>

<View>
	<ViewHeader title="Dev Tools">
		<a
			href="/dev-tools/logs"
			use:link
			class="nav-link"
			class:active={$location === '/dev-tools/logs'}
		>
			Logs
		</a>
		<a
			href="/dev-tools/elements"
			use:link
			class="nav-link"
			class:active={$location === '/dev-tools/elements'}
			class:disabled={$device === null}
		>
			Elements
		</a>
		<a
			href="/dev-tools/network"
			use:link
			class="nav-link"
			class:active={$location === '/dev-tools/network'}
		>
			Network
		</a>
		<a
			href="/dev-tools/storage"
			use:link
			class="nav-link"
			class:active={$location === '/dev-tools/storage'}
			class:disabled={$device === null}
		>
			Storage
		</a>
		<a
			href="/dev-tools/console"
			use:link
			class="nav-link"
			class:active={$location === '/dev-tools/console'}
			class:disabled={$device === null}
		>
			Console
		</a>
	</ViewHeader>
	<ViewContent>
		<Router {routes} {prefix} />
	</ViewContent>
</View>

<style>
	.nav-link {
		font-size: 1.6rem;
		margin-right: 15px;
		margin-bottom: -2px;
		border-bottom: 3px solid transparent;
		text-decoration: none;
	}
	.nav-link.active,
	.nav-link:hover {
		border-color: var(--accent-color);
	}
	.nav-link.disabled {
		opacity: 0.4;
		pointer-events: none;
	}
</style>

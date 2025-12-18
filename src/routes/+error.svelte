<script>
	import { page } from '$app/stores';
	import { Button } from '$lib/components/ui/button';

// Server status (mocked, replace with real API if needed)
let serverStatus = $state('Online');
</script>

<svelte:head>
	<title>{$page.status} - LatinCraft</title>
	<style>
		body {
			background-color: #0c0a09;
		}
	</style>
</svelte:head>

<div class="min-h-screen bg-stone-950">

	<div class="absolute top-5 right-5 flex items-center gap-2 z-10">
		<Button
			size="sm"
			variant="ghost"
			class="flex items-center gap-2 text-green-400  hover:text-green-400  dark px-3 py-1"
			onclick={() => location.href = '/status'}
			aria-label="View server status"
		>
			<span class="inline-block w-2 h-2 rounded-full bg-green-500"></span>
			Online
		</Button>
	</div>
    
	<!-- Logo -->
	<div class="absolute top-5 left-5">
		<a href="/">
			<h1 class="text-2xl font-bold">
				<span class="text-red-400">Latin</span><span class="text-stone-200">Craft</span>
			</h1>
		</a>
	</div>

	<!-- error section -->
	<div class="min-h-screen flex items-center justify-center px-4">
		<div class="text-center">
			<h1 class="text-[7rem] md:text-[10rem] font-bold text-white mb-4 tracking-tight leading-none">{$page.status}</h1>
			<p class="text-xl text-stone-300 mb-6">
				{#if $page.status === 404}
					Page not found
				{:else if $page.status === 500}
					Server error
				{:else}
					Something went wrong
				{/if}
			</p>
			<Button 
				size="lg"
				class="bg-white text-stone-900 hover:bg-stone-100 cursor-pointer px-8 font-medium"
				onclick={() => location.href = '/'}
			>
				Go Home
			</Button>
		</div>
	</div>
</div>

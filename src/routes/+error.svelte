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
			background-color: #000000;
		}
	</style>
</svelte:head>

<div class="min-h-screen bg-black text-white font-sans selection:bg-white/20">

	<div class="absolute top-5 right-5 flex items-center gap-2 z-10">
		<Button
			size="sm"
			variant="ghost"
			class="flex items-center gap-2 text-green-400 hover:text-green-300 hover:bg-white/5 px-3 py-1"
			onclick={() => location.href = '/status'}
			aria-label="View server status"
		>
			<span class="inline-block w-2 h-2 rounded-full bg-green-500 animate-pulse"></span>
			Online
		</Button>
	</div>
    
	<!-- Logo -->
	<div class="absolute top-5 left-5">
		<a href="/" class="hover:opacity-80 transition-opacity">
			<h1 class="text-xl font-bold tracking-tight">
				<span class="text-white">Latin</span><span class="text-zinc-400">Craft</span>
			</h1>
		</a>
	</div>

	<!-- error section -->
	<div class="min-h-screen flex items-center justify-center px-4">
		<div class="text-center">
			<h1 class="text-[8rem] md:text-[12rem] font-bold text-white mb-4 tracking-tighter leading-none select-none">{$page.status}</h1>
			<p class="text-2xl text-zinc-400 mb-10 font-light">
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
				class="bg-white text-black hover:bg-zinc-200 cursor-pointer px-8 h-12 rounded-full font-medium text-base transition-all hover:scale-105"
				onclick={() => location.href = '/'}
			>
				Go Home
			</Button>
		</div>
	</div>
</div>

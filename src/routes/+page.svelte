<script>
	import { Button } from '$lib/components/ui/button';
	import * as Card from '$lib/components/ui/card';
	import { Badge } from '$lib/components/ui/badge';
	import Header from '$lib/components/Header.svelte';

	let copied = $state(false);

	function copyToClipboard(text) {
		navigator.clipboard.writeText(text);
		copied = true;
		setTimeout(() => {
			copied = false;
		}, 2000);
	}
</script>

<svelte:head>
	<style>
		body {
			background-color: #0c0a09;
		}
	</style>
</svelte:head>

<div class="min-h-screen bg-stone-950">
	<Header logoColor="red" currentPage="home" />

	<!-- Hero Section -->
	<div class="container mx-auto px-4 py-16 min-h-[calc(100vh-73px)]">
		<div class="text-center mb-20">
			<h1 class="text-7xl font-bold text-white mb-6 tracking-tight">
				<span class="text-red-400">Latin</span><span class="text-white">Craft</span>
			</h1>
			<p class="text-xl text-stone-300 mb-8 font-normal">The semi-official Minecraft Server of <a href="https://www.roxburylatin.org/" class=" hover:underline cursor-pointer ">The Roxbury Latin School</a></p>
			<div class="flex gap-4 justify-center flex-wrap">
				<Button size="lg" class="bg-white text-stone-900 hover:bg-stone-100 cursor-pointer px-8 font-medium" onclick={() => (location.href = '/discord')}>
					Join Discord
				</Button>
                <Button
                    size="lg"
                    class="bg-stone-900 border border-stone-700 cursor-pointer text-white hover:bg-stone-800 font-medium"
                    onclick={() => (location.href = '/status')}
                >
                    Server Status
                </Button>
			</div>
		</div>

		<!-- Servers Section -->
		<div class="max-w-5xl mx-auto">
			<h2 class="text-4xl font-bold text-white text-center mb-12 tracking-tight">Servers</h2>
			
			<div class="grid md:grid-cols-2 gap-6">
				<!-- Creative Server -->
				<Card.Root class="relative bg-stone-900 border-stone-800 hover:border-stone-700 transition-all overflow-hidden group">
					<Card.Header>
						<div class="flex justify-between items-start">
							<Card.Title class="text-2xl text-white font-semibold">LatinCraft Creative</Card.Title>
							<a href="/status">
								<Badge class="bg-green-500/10 text-green-400 border border-green-500/20 cursor-pointer hover:bg-green-500/20 transition-colors">ONLINE</Badge>
							</a>
						</div>
						<Card.Description class="text-stone-400">
							Unleash your creativity in the full creative world
						</Card.Description>
					</Card.Header>
					<Card.Content class="text-stone-300">
						<div class="space-y-3">
							<div class="flex items-center gap-3">
								<div class="w-1.5 h-1.5 rounded-full bg-green-400"></div>
								<span class="text-sm">Build anything you imagine</span>
							</div>
							<div class="flex items-center gap-3">
								<div class="w-1.5 h-1.5 rounded-full bg-green-400"></div>
								<span class="text-sm">WorldEdit & other plugins</span>
							</div>
							<div class="flex items-center gap-3">
								<div class="w-1.5 h-1.5 rounded-full bg-green-400"></div>
								<span class="text-sm">Collaborative building</span>
							</div>
							<div class="mt-6 p-4 bg-stone-950 rounded-lg border border-stone-800">
								<p class="text-xs text-stone-500 mb-2 uppercase tracking-wider">Server IP</p>
								<code class="text-green-400 font-mono text-sm">build.latincraft.net</code>
							</div>
						</div>
					</Card.Content>
					<Card.Footer>
						<Button 
							class="w-full bg-stone-800 hover:bg-stone-700 text-white border-0 relative cursor-pointer overflow-hidden"
							onclick={() => copyToClipboard('build.latincraft.net')}
						>
							<span class="transition-all duration-300 ease-out" class:opacity-0={copied} class:scale-95={copied}>
								Copy IP Address
							</span>
							{#if copied}
								<span class="absolute inset-0 flex items-center justify-center animate-in fade-in zoom-in-95 duration-300">
									✓ Copied!
								</span>
							{/if}
						</Button>
					</Card.Footer>
				</Card.Root>

				<!-- Season 2 Server -->
				<Card.Root class="relative bg-stone-900 border-stone-800 hover:border-stone-700 transition-all overflow-hidden group">
					<Card.Header>
						<div class="flex justify-between items-start">
							<Card.Title class="text-2xl text-white font-semibold">LatinCraft Season 2</Card.Title>
							<a href="/status">
								<Badge class="bg-amber-500/10 text-amber-400 border border-amber-500/20 cursor-pointer hover:bg-amber-500/20 transition-colors">COMING SOON</Badge>
							</a>
						</div>
						<Card.Description class="text-stone-400">
							A brand new season begins
						</Card.Description>
					</Card.Header>
					<Card.Content class="text-stone-300">
						<div class="space-y-3">
							<div class="flex items-center gap-3">
								<div class="w-1.5 h-1.5 rounded-full bg-amber-400"></div>
								<span class="text-sm">Fresh survival world</span>
							</div>
							<div class="flex items-center gap-3">
								<div class="w-1.5 h-1.5 rounded-full bg-amber-400"></div>
								<span class="text-sm">New challenges & events</span>
							</div>
							<div class="flex items-center gap-3">
								<div class="w-1.5 h-1.5 rounded-full bg-amber-400"></div>
								<span class="text-sm">Runs throughout winter break</span>
							</div>
							<div class="mt-6 p-4 bg-stone-950 rounded-lg border border-stone-800">
								<p class="text-xs text-stone-500 mb-2 uppercase tracking-wider">Launches</p>
								<code class="text-amber-400 font-mono text-sm">December 19th, 2025</code>
							</div>
						</div>
					</Card.Content>
					<Card.Footer>
						<Button 
							class="w-full bg-stone-800 hover:bg-stone-700 text-white border-0"
							disabled
						>
							Coming Soon...
						</Button>
					</Card.Footer>
				</Card.Root>
			</div>
		</div>

	</div>

	<!-- Footer -->
	<footer class="bg-stone-950 py-8 border-t border-stone-900">
		<div class="container mx-auto px-4 text-center text-stone-400">
			<p>&copy; 2025 LatinCraft. All rights reserved.</p>
			<p class="text-sm mt-2">Not affiliated with Mojang or Microsoft | View source on <a class=" hover:underline" href="https://github.com/Static-o2/Latincraft">GitHub</a> </p>
		</div>
	</footer>
</div>

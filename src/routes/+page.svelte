<script>
	import { Button } from '$lib/components/ui/button';
	import * as Card from '$lib/components/ui/card';
	import { Badge } from '$lib/components/ui/badge';
	import Header from '$lib/components/Header.svelte';
	import { onMount } from 'svelte';

	let copied = $state(false);
	let countdown = $state({ days: 0, hours: 0, minutes: 0, seconds: 0 });

	function copyToClipboard(text) {
		navigator.clipboard.writeText(text);
		copied = true;
		setTimeout(() => {
			copied = false;
		}, 2000);
	}

	function updateCountdown() {
		// January 23rd, 2026 at 7:30 PM EST (UTC-5)
		const launchDate = new Date('2026-01-24T00:30:00Z'); // 7:30 PM EST = 00:30 UTC next day
		const now = new Date();
		const diff = launchDate - now;

		if (diff > 0) {
			countdown = {
				days: Math.floor(diff / (1000 * 60 * 60 * 24)),
				hours: Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60)),
				minutes: Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60)),
				seconds: Math.floor((diff % (1000 * 60)) / 1000)
			};
		} else {
			countdown = { days: 0, hours: 0, minutes: 0, seconds: 0 };
		}
	}

	onMount(() => {
		updateCountdown();
		const interval = setInterval(updateCountdown, 1000);
		return () => clearInterval(interval);
	});
</script>

<svelte:head>
	<style>
		body {
			background-color: rgb(10, 10, 10);
		}
	</style>
</svelte:head>

<div class="min-h-screen bg-[rgb(10,10,10)] text-white selection:bg-white/20">
	<Header logoColor="red" currentPage="home" />

	<!-- Hero Section -->
	<div class="container mx-auto px-4 pt-32 pb-16 min-h-[calc(100vh-73px)] flex flex-col justify-center">
		<div class="text-center mb-24 mx-auto">
			<h1 class="text-6xl md:text-8xl font-bold text-white mb-8">
				LatinCraft
			</h1>
			<p class="text-xl md:text-2xl text-zinc-400 mb-10 leading-relaxed">
				The semi-official Minecraft Server of 
				<a href="https://www.roxburylatin.org/" class="text-white hover:text-zinc-300 transition-colors border-b border-white/20 hover:border-white pb-0.5">The Roxbury Latin School</a>
			</p>
			<div class="flex gap-4 justify-center flex-wrap">
				<Button size="lg" class="bg-white text-black hover:bg-zinc-200 cursor-pointer px-8 h-12 rounded-full font-medium text-base transition-all hover:scale-105" onclick={() => (location.href = '/discord')}>
					Join Discord
				</Button>
                <Button
                    size="lg"
                    class="bg-zinc-900 border border-zinc-800 cursor-pointer text-white hover:bg-zinc-800 h-12 px-8 rounded-full font-medium text-base transition-all hover:scale-105"
                    onclick={() => (location.href = '/status')}
                >
                    Server Status
                </Button>
			</div>
		</div>

		<!-- Servers Section -->
		<div class="w-full max-w-[1062px] mx-auto">
			<h2 class="text-4xl font-bold text-white text-center mb-12 tracking-tight">Servers</h2>
			
			<div class="grid md:grid-cols-2 gap-8">
				<!-- Creative Server -->
				<Card.Root class="relative bg-zinc-900/30 border-zinc-700 transition-all overflow-hidden group backdrop-blur-sm">
					<Card.Header>
						<div class="flex justify-between items-start">
							<Card.Title class="text-2xl text-white font-semibold">LatinCraft Creative</Card.Title>
							<a href="/status">
								<Badge class="bg-green-500/10 text-green-400 border border-green-500/20 cursor-pointer hover:bg-green-500/20 transition-colors">ONLINE</Badge>
							</a>
						</div>
						<Card.Description class="text-zinc-400">
							Unleash your creativity in the full creative world
						</Card.Description>
					</Card.Header>
					<Card.Content class="text-zinc-300">
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
							<div class="mt-6 p-4 bg-black/40 rounded-lg border border-zinc-800">
								<p class="text-xs text-zinc-500 mb-2 uppercase tracking-wider">Server IP</p>
								<code class="text-green-400 font-mono text-sm">build.latincraft.net</code>
							</div>
						</div>
					</Card.Content>
					<Card.Footer>
						<Button 
							class="w-full bg-zinc-800 hover:bg-zinc-700 text-white border-0 relative cursor-pointer overflow-hidden"
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

				<!-- Season 3 Server -->
				<Card.Root class="relative bg-zinc-900/30 border-zinc-700 transition-all overflow-hidden group backdrop-blur-sm">
					<Card.Header>
						<div class="flex justify-between items-start">
							<Card.Title class="text-2xl text-white font-semibold">LatinCraft Season 3</Card.Title>
							<a href="/status">
								<Badge class="bg-amber-500/10 text-amber-400 border border-amber-500/20 cursor-pointer hover:bg-amber-500/20 transition-colors">COMING SOON</Badge>
							</a>
						</div>
						<Card.Description class="text-zinc-400">
							A brand new season begins
						</Card.Description>
					</Card.Header>
					<Card.Content class="text-zinc-300">
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
							<span class="text-sm">idk what to put for the 3rd point</span>
						</div>
						<div class="mt-6 p-4 bg-black/40 rounded-lg border border-zinc-800">							<div class="flex gap-3 justify-center items-center">
								<div class="text-center">
									<div class="text-2xl font-bold text-amber-400 font-mono">{countdown.days}</div>
									<div class="text-xs text-zinc-500 uppercase">Days</div>
								</div>
								<span class="text-amber-400 text-xl">:</span>
								<div class="text-center">
									<div class="text-2xl font-bold text-amber-400 font-mono">{countdown.hours.toString().padStart(2, '0')}</div>
									<div class="text-xs text-zinc-500 uppercase">Hours</div>
								</div>
								<span class="text-amber-400 text-xl">:</span>
								<div class="text-center">
									<div class="text-2xl font-bold text-amber-400 font-mono">{countdown.minutes.toString().padStart(2, '0')}</div>
									<div class="text-xs text-zinc-500 uppercase">Mins</div>
								</div>
								<span class="text-amber-400 text-xl">:</span>
								<div class="text-center">
									<div class="text-2xl font-bold text-amber-400 font-mono">{countdown.seconds.toString().padStart(2, '0')}</div>
									<div class="text-xs text-zinc-500 uppercase">Secs</div>
								</div>
							</div>
						</div>
					</div>
				</Card.Content>
				<Card.Footer>
					<Button 
						class="w-full bg-zinc-800 hover:bg-zinc-700 text-white border-0"
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
	<footer class="py-6 border-t border-white/5">
		<div class="container mx-auto px-4 flex flex-col md:flex-row justify-between items-center gap-4 text-zinc-600 text-sm">
			<p>&copy; 2025 LatinCraft</p>
			<div class="flex items-center gap-6">
				<span class="hidden md:inline">Not affiliated with Mojang or Microsoft</span>
				<a class="hover:text-zinc-400 transition-colors" href="https://github.com/Static-o2/Latincraft">GitHub</a>
			</div>
		</div>
	</footer>
</div>

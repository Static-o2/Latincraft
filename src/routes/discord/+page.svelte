<script>
	import { Button } from '$lib/components/ui/button';
	import * as Card from '$lib/components/ui/card';
	import { onMount } from 'svelte';
	import Header from '$lib/components/Header.svelte';

	let countdown = $state(20);

	onMount(() => {
		// Countdown timer
		const countdownInterval = setInterval(() => {
			countdown--;
			if (countdown <= 0) {
				clearInterval(countdownInterval);
			}
		}, 1000);

		// Redirect to Discord after delay
		const redirectTimer = setTimeout(() => {
			window.location.href = 'https://discord.gg/UXpd2YnQwH';
		}, 20000);

		return () => {
			clearInterval(countdownInterval);
			clearTimeout(redirectTimer);
		};
	});
</script>

<svelte:head>
	<title>Join Discord - LatinCraft</title>
	<style>
		body {
			background-color: #000000;
		}
	</style>
</svelte:head>

<div class="min-h-screen bg-black text-white selection:bg-indigo-500/30">
	<Header currentPage="discord" />

	<!-- Main Content -->
	<div class="container mx-auto px-4 pt-17 pb-16 min-h-[calc(100vh-73px)] flex flex-col justify-center">
		<div class="max-w-xl mx-auto w-full">
			<div class="text-center mb-16">
				<h1 class="text-5xl md:text-6xl font-bold text-white mb-6">Join The Discord</h1>
				<p class="text-xl text-zinc-400">Connect with the Roxbury Latin community</p>
			</div>

			<Card.Root class="bg-zinc-900/30 border-zinc-700 backdrop-blur-sm">
				<Card.Header class="pb-2">
					<Card.Title class="text-2xl text-white font-semibold text-center">RL Foxes Discord Server</Card.Title>
					<Card.Description class="text-zinc-400 text-center text-base">
						Chat with friends, get updates, and join events
					</Card.Description>
				</Card.Header>
				<Card.Content class="text-zinc-300 pt-2">
					<div class="space-y-4">
						<div class="flex items-center gap-3">
							<div class="w-1.5 h-1.5 rounded-full bg-indigo-400"></div>
							<span class="text-sm text-zinc-300">Stay updated about cool stuff</span>
						</div>
						<div class="flex items-center gap-3">
							<div class="w-1.5 h-1.5 rounded-full bg-indigo-400"></div>
							<span class="text-sm text-zinc-300">Connect with other players</span>
						</div>
						<div class="flex items-center gap-3">
							<div class="w-1.5 h-1.5 rounded-full bg-indigo-400"></div>
							<span class="text-sm text-zinc-300">Hang Out with friends</span>
						</div>
						<div class="flex items-center gap-3">
							<div class="w-1.5 h-1.5 rounded-full bg-indigo-400"></div>
							<span class="text-sm text-zinc-300">Participate in friday game nights</span>
						</div>
						
						<div class="mt-8 p-4 bg-black/40 rounded-lg border border-zinc-800 text-center">
							<p class="text-xs text-zinc-500 mb-2 uppercase tracking-wider font-medium">Redirecting in {countdown} second{countdown !== 1 ? 's' : ''}...</p>
							<code class="text-indigo-400 font-mono text-sm">discord.gg/UXpd2YnQwH</code>
						</div>
					</div>
				</Card.Content>
				<Card.Footer class="pt-2">
					<Button 
						class="w-full cursor-pointer bg-white text-black hover:bg-zinc-200 border-0 h-10 font-medium transition-all"
						onclick={() => window.open('https://discord.gg/UXpd2YnQwH', '_blank')}
					>
						Apply to join
					</Button>
				</Card.Footer>
			</Card.Root>

			<div class="text-center mt-12">
				<a href="/" class="text-zinc-500 hover:text-white transition-colors text-sm font-medium">
					← Back to Home
				</a>
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

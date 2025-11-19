<script>
	import { Button } from '$lib/components/ui/button';
	import * as Card from '$lib/components/ui/card';
	import { onMount } from 'svelte';

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
			background-color: #0c0a09;
		}
	</style>
</svelte:head>

<div class="min-h-screen bg-stone-950">
	<!-- Header -->
	<header class="bg-stone-900 border-b border-stone-800">
		<div class="container mx-auto px-4 py-4">
			<div class="flex justify-between items-center">
				<a href="/">
					<h1 class="text-2xl font-bold">
						<span class="text-indigo-400">Latin</span><span class="text-stone-200">Craft</span>
					</h1>
				</a>
				<nav class="flex gap-4 items-center">
					<a href="/status" class="text-stone-300 hover:text-green-500 transition-colors">Server Status</a>
					<a href="https://discord.gg/UXpd2YnQwH" target="_blank" rel="noopener noreferrer" class="text-green-500 transition-colors font-medium">Discord</a>
					<button class="text-stone-300 hover:text-green-500 transition-colors">Rules</button>
				</nav>
			</div>
		</div>
	</header>

	<!-- Main Content -->
	<div class="container mx-auto px-4 py-16">
		<div class="max-w-xl mx-auto">
			<div class="text-center mb-12">
				<h1 class="text-5xl font-bold text-white mb-4 tracking-tight">Join The Discord</h1>
				<p class="text-xl text-stone-400">Connect with the Roxbury Latin community</p>
			</div>

			<Card.Root class="bg-stone-900 border-stone-800">
				<Card.Header>
					<Card.Title class="text-2xl text-white font-semibold text-center">RL Foxes Discord Server</Card.Title>
					<Card.Description class="text-stone-400 text-center">
						Chat with friends, get updates, and join events
					</Card.Description>
				</Card.Header>
				<Card.Content class="text-stone-300">
					<div class="space-y-4">
						<div class="flex items-center gap-3">
							<div class="w-1.5 h-1.5 rounded-full bg-indigo-400"></div>
							<span class="text-sm">Stay updated about cool stuff</span>
						</div>
						<div class="flex items-center gap-3">
							<div class="w-1.5 h-1.5 rounded-full bg-indigo-400"></div>
							<span class="text-sm">Connect with other players</span>
						</div>
						<div class="flex items-center gap-3">
							<div class="w-1.5 h-1.5 rounded-full bg-indigo-400"></div>
							<span class="text-sm">Hang Out with friends</span>
						</div>
						<div class="flex items-center gap-3">
							<div class="w-1.5 h-1.5 rounded-full bg-indigo-400"></div>
							<span class="text-sm">Participate in friday game nights</span>
						</div>
						
						<div class="mt-6 p-4 bg-stone-950 rounded-lg border border-stone-800 text-center">
							<p class="text-xs text-stone-500 mb-2 uppercase tracking-wider">Redirecting in {countdown} second{countdown !== 1 ? 's' : ''}...</p>
							<code class="text-indigo-400 font-mono text-sm">discord.gg/UXpd2YnQwH</code>
						</div>
					</div>
				</Card.Content>
				<Card.Footer>
					<Button 
						class="w-full bg-stone-800 hover:bg-stone-700 text-white border-0"
						onclick={() => window.open('https://discord.gg/UXpd2YnQwH', '_blank')}
					>
						Apply to join
					</Button>
				</Card.Footer>
			</Card.Root>

			<div class="text-center mt-8">
				<a href="/" class="text-stone-400 hover:text-green-500 transition-colors text-sm">
					← Back to Home
				</a>
			</div>
		</div>
	</div>

	<!-- Footer -->
	<footer class="bg-stone-950 py-8 border-t border-stone-900">
		<div class="container mx-auto px-4 text-center text-stone-400">
			<p>&copy; 2025 LatinCraft. All rights reserved.</p>
			<p class="text-sm mt-2">Not affiliated with Mojang or Microsoft</p>
		</div>
	</footer>
</div>

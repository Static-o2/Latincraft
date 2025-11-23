<script>
	import { Badge } from '$lib/components/ui/badge';
	import * as Card from '$lib/components/ui/card';
	import { onMount } from 'svelte';
	
	let servers = $state([
		{
			name: 'LatinCraft Creative',
			status: 'checking',
			players: 0,
			maxPlayers: 0,
			onlinePlayers: [],
			ip: 'build.latincraft.net',
			version: 'Unknown',
			displayIp: 'build.latincraft.net'
		},
		{
			name: 'LatinCraft Season 2',
			status: 'coming-soon',
			players: 0,
			maxPlayers: 100,
			onlinePlayers: [],
			ip: null,
			version: '1.21.10',
			launchDate: 'December 19th, 2025',
			displayIp: 'TBA'
		}
	]);

	async function checkServerStatus(server, index) {
		if (!server.ip) return;
		
		try {
			const response = await fetch(`https://api.mcstatus.io/v2/status/java/${server.ip}`);
			const data = await response.json();
			
			if (data.online) {
				// Extract player names from the list array
				const playerList = data.players?.list?.map(p => p.name_clean || p.name_raw || p) || [];
				
				servers[index] = {
					...server,
					status: 'online',
					players: data.players?.online || 0,
					maxPlayers: data.players?.max || 0,
					onlinePlayers: playerList,
					version: data.version?.name_clean || data.version?.name_raw || 'Unknown'
				};
			} else {
				servers[index] = {
					...server,
					status: 'offline'
				};
			}
		} catch (error) {
			console.error('Error checking server status:', error);
			servers[index] = {
				...server,
				status: 'offline'
			};
		}
	}

	onMount(() => {
		// Check status for servers that have an IP
		servers.forEach((server, index) => {
			if (server.ip) {
				checkServerStatus(server, index);
			}
		});

		// Refresh every 30 seconds
		const interval = setInterval(() => {
			servers.forEach((server, index) => {
				if (server.ip) {
					checkServerStatus(server, index);
				}
			});
		}, 30000);

		return () => clearInterval(interval);
	});
</script>

<svelte:head>
	<title>Server Status - LatinCraft</title>
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
						<span class="text-green-500">Latin</span><span class="text-stone-200">Craft</span>
					</h1>
				</a>
				<nav class="flex gap-4 items-center">
					<a href="/status" class="text-green-500 transition-colors font-medium">Server Status</a>
					<a href="/discord" class="text-stone-300 hover:text-green-500 transition-colors">Discord</a>
					<button class="text-stone-300 hover:text-green-500 transition-colors">Rules</button>
				</nav>
			</div>
		</div>
	</header>

	<!-- Main Content -->
	<div class="container mx-auto px-4 py-16 min-h-[calc(100vh-73px)]">
		<div class="max-w-4xl mx-auto">
			<h1 class="text-4xl font-bold text-white mb-2 tracking-tight">Server Status</h1>
			<p class="text-stone-400 mb-12">Real-time server info and online players</p>

			<div class="space-y-8">
				{#each servers as server}
					<Card.Root class="bg-stone-900 border-stone-800">
						<Card.Header>
							<div class="flex justify-between items-start">
								<div>
									<Card.Title class="text-2xl text-white font-semibold">{server.name}</Card.Title>
									<Card.Description class="text-stone-400 mt-1">
										{server.displayIp} • {server.version}
									</Card.Description>
								</div>
								{#if server.status === 'online'}
									<Badge class="bg-green-500/10 text-green-400 border border-green-500/20">
										ONLINE
									</Badge>
								{:else if server.status === 'offline'}
									<Badge class="bg-red-500/10 text-red-400 border border-red-500/20">
										OFFLINE
									</Badge>
								{:else if server.status === 'checking'}
									<Badge class="bg-stone-500/10 text-stone-400 border border-stone-500/20">
										CHECKING...
									</Badge>
								{:else}
									<Badge class="bg-amber-500/10 text-amber-400 border border-amber-500/20">
										COMING SOON
									</Badge>
								{/if}
							</div>
						</Card.Header>
						
						<Card.Content>
							{#if server.status === 'online'}
								<!-- Player Count -->
								<div class="mb-6">
									<div class="flex justify-between items-center mb-2">
										<span class="text-sm text-stone-400 uppercase tracking-wider">Players Online</span>
										<span class="text-white font-semibold">{server.players}/{server.maxPlayers}</span>
									</div>
									<div class="w-full bg-stone-800 rounded-full h-2">
										<div 
											class="bg-green-500 h-2 rounded-full transition-all duration-500"
											style="width: {(server.players / server.maxPlayers) * 100}%"
										></div>
									</div>
								</div>

								<!-- Online Players List -->
								{#if server.onlinePlayers.length > 0}
									<div>
										<h3 class="text-sm text-stone-400 uppercase tracking-wider mb-3">Currently Playing</h3>
										<div class="flex flex-wrap gap-2">
											{#each server.onlinePlayers as player}
												<div class="px-3 py-1.5 bg-stone-800 rounded-md text-stone-300 text-sm border border-stone-700">
													{player}
												</div>
											{/each}
										</div>
									</div>
								{:else}
									<div class="text-center py-4">
										<p class="text-stone-500 text-sm">No players online right now</p>
									</div>
								{/if}
							{:else if server.status === 'offline'}
								<div class="text-center py-8">
									<p class="text-red-400 text-lg">Server is currently offline</p>
									<p class="text-stone-500 text-sm mt-2">Please check back later</p>
								</div>
							{:else if server.status === 'checking'}
								<div class="text-center py-8">
									<p class="text-stone-400">Checking server status...</p>
								</div>
							{:else if server.launchDate}
								<!-- Coming Soon Info -->
								<div class="text-center py-8">
									<p class="text-stone-400 mb-2">Launches on</p>
									<p class="text-2xl font-semibold text-amber-400">{server.launchDate}</p>
								</div>
							{/if}
						</Card.Content>
					</Card.Root>
				{/each}
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

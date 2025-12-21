<script>
	import * as Card from '$lib/components/ui/card';
	import { Badge } from '$lib/components/ui/badge';
	import { onMount } from 'svelte';
	import Header from '$lib/components/Header.svelte';
	
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
			status: 'checking',
			players: 0,
			maxPlayers: 100,
			onlinePlayers: [],
			ip: 'play.latincraft.net',
			version: '1.21.10',
			displayIp: 'play.latincraft.net'
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
			background-color: #000000;
		}
	</style>
</svelte:head>

<div class="min-h-screen bg-[rgb(10,10,10)] text-white selection:bg-green-500/30">
	<Header currentPage="status" />

	<!-- Main Content -->
	<div class="container mx-auto px-4 pt-12 pb-16 min-h-[calc(100vh-73px)]">
		<div class="max-w-4xl mx-auto">
			<h1 class="text-5xl font-bold text-white mb-3">Server Status</h1>
			<p class="text-zinc-400 mb-12 text-lg">Real-time server info + online players</p>

			<div class="space-y-8">
				{#each servers as server}
					<Card.Root class="bg-zinc-900/30 border-zinc-700/90 backdrop-blur-sm">
						<Card.Header>
							<div class="flex justify-between items-start">
								<div>
									<Card.Title class="text-2xl text-white font-semibold">{server.name}</Card.Title>
									<Card.Description class="text-zinc-400 mt-1 font-mono text-sm">
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
								{/if}
							</div>
						</Card.Header>
						
						<Card.Content>
							{#if server.status === 'online'}
								<!-- Player Count -->
								<div class="mb-8">
									<div class="flex justify-between items-center mb-3">
										<span class="text-xs text-zinc-500 uppercase tracking-wider font-medium">Players Online</span>
										<span class="text-white font-mono">{server.players}/{server.maxPlayers}</span>
									</div>
									<div class="w-full bg-zinc-800/50 rounded-full h-1.5 overflow-hidden">
										<div 
											class="bg-white h-full rounded-full transition-all duration-500"
											style="width: {(server.players / server.maxPlayers) * 100}%"
										></div>
									</div>
								</div>

								<!-- Online Players List -->
								{#if server.onlinePlayers.length > 0}
									<div>
										<h3 class="text-xs text-zinc-500 uppercase tracking-wider mb-4 font-medium">Currently Playing</h3>
										<div class="flex flex-wrap gap-2">
											{#each server.onlinePlayers as player}
												<div class="px-3 py-1.5 bg-zinc-800/50 rounded-md text-zinc-300 text-sm border border-white/5">
													{player}
												</div>
											{/each}
										</div>
									</div>
								{:else}
									<div class="text-center py-4 border border-dashed border-zinc-800 rounded-lg">
										<p class="text-zinc-500 text-sm">No players online right now</p>
									</div>
								{/if}
							{:else if server.status === 'offline'}
								<div class="text-center py-12 border border-dashed border-zinc-800 rounded-lg">
									<p class="text-red-400 text-lg font-medium">Server is currently offline</p>
									<p class="text-zinc-500 text-sm mt-2">Please check back later</p>
								</div>
							{:else if server.status === 'checking'}
								<div class="text-center py-12">
									<p class="text-zinc-400 animate-pulse">Checking server status...</p>
								</div>
							{/if}
						</Card.Content>
					</Card.Root>
				{/each}
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

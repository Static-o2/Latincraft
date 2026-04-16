<script>
	import { Button } from '$lib/components/ui/button';
	import * as Card from '$lib/components/ui/card';
	import { Badge } from '$lib/components/ui/badge';
	import Header from '$lib/components/Header.svelte';
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

		<!-- Season 4 Section -->
		<div class="w-full max-w-4xl mx-auto">

			<Card.Root class="relative bg-zinc-900/40 border-zinc-700 overflow-hidden backdrop-blur-sm">
				<div class="pointer-events-none absolute  inset-1 rounded-lg bg-[radial-gradient(circle_at_20%_15%,rgba(255,80,80,0.12),transparent_42%)]"></div>
				<Card.Header class="relative">
					<div class="flex justify-between items-start gap-4 flex-wrap">
						<div>
							<Card.Title class="text-3xl md:text-4xl text-white font-semibold">LatinCraft Season 4: Divided</Card.Title>
							<Card.Description class="text-zinc-300 mt-4 text-base md:text-md max-w-2xl">
								The world is split into four quadrants, separated by a giant wall. Each team is placed into their own quadrant.
							</Card.Description>
						</div>
						<Badge class="bg-red-500/10 text-red-300 border border-red-400/30">SEASON EVENT</Badge>
					</div>
				</Card.Header>

				<Card.Content class=" text-zinc-200 space-y-4">
					<p class="text-base md:text-md leading-relaxed">
						When the season begins, you will have 2 whole weeks to prepare for when the wall drops. Go on defense and build fortified bases and strongholds, go on offense and build TNT cannons, flying machines and build up vaults of pvp gear, or maybe go with a mix of both.
					</p>
					<p class="text-base md:text-md leading-relaxed">
						On Anarchy Day, the wall drops and players can move freely between the quadrants. Last team standing wins. To keep things interesting if there's a stalemate, bonus chests filled with OP loot will start to spawn randomly and the world border will shrink until only one team remains.
					</p>


				</Card.Content>

				<Card.Footer class="relative flex flex-col sm:flex-row gap-3 mt-8">
					<Button
						class="w-full sm:w-auto bg-white text-black hover:bg-zinc-200 cursor-pointer"
						onclick={() => (location.href = '/discord')}
					>
						Join Discord for Team Selection
					</Button>
					<Button
						class="w-full sm:w-auto bg-zinc-800 hover:bg-zinc-700 text-white border-0"
						disabled
					>
						IP Drops Soon
					</Button>

				</Card.Footer>
			</Card.Root>
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

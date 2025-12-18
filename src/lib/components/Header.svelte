<script>
	import * as DropdownMenu from '$lib/components/ui/dropdown-menu';
	
	let { logoColor = 'red', currentPage = 'home' } = $props();
</script>

<header class="">
	<div class="container mx-auto px-4 py-4">
		<div class="flex justify-between items-center">
			<a href="/">
				<h1 class="text-2xl font-bold">
					<span class="text-{logoColor}-400">Latin</span><span class="text-stone-200">Craft</span>
				</h1>
			</a>
			
			<!-- Desktop -->
			<nav class="hidden sm:flex gap-4 items-center">
				<a 
					href="/status" 
					class="{currentPage === 'status' ? 'text-green-400 font-medium' : 'text-stone-300 hover:text-green-300'} transition-colors"
				>
					Server Status
				</a>
				<a 
					href="/discord" 
					class="{currentPage === 'discord' ? 'text-indigo-400 font-medium' : 'text-stone-300 hover:text-indigo-300'} transition-colors"
				>
					Discord
				</a>
				<button class="text-stone-300 hover:text-orange-300 transition-colors">Rules</button>
			</nav>

			<!-- Mobile -->
			<DropdownMenu.Root>
				<DropdownMenu.Trigger class="sm:hidden text-stone-300 hover:text-stone-400 transition-colors p-2">
					<svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
						<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"></path>
					</svg>
				</DropdownMenu.Trigger>
				<DropdownMenu.Content class="bg-stone-900 border-stone-800 w-48">
					<DropdownMenu.Item class="text-stone-300 hover:text-green-500 focus:text-green-500 focus:bg-stone-800">
						<a href="/status" class="w-full {currentPage === 'status' ? 'text-green-500 font-medium' : ''}">
							Server Status
						</a>
					</DropdownMenu.Item>
					<DropdownMenu.Item class="text-stone-300 hover:text-green-500 focus:text-green-500 focus:bg-stone-800">
						<a href="/discord" class="w-full {currentPage === 'discord' ? 'text-indigo-400 font-medium' : ''}">
							Discord
						</a>
					</DropdownMenu.Item>
					<DropdownMenu.Item class="text-stone-300 hover:text-green-500 focus:text-green-500 focus:bg-stone-800">
						Rules
					</DropdownMenu.Item>
				</DropdownMenu.Content>
			</DropdownMenu.Root>
		</div>
	</div>
</header>

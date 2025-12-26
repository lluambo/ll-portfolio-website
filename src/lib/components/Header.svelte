<script lang="ts">
    let { links = [] }: { links: { name: string; href: string }[] } = $props();
</script>

<div class="fixed top-4 left-0 right-0 z-50 flex justify-center w-full px-4">
    <div
        class="navbar bg-black/30 backdrop-blur-xl border border-white/10 rounded-full shadow-lg max-w-3xl w-full text-white"
    >
        <div class="navbar-start">
            <a
                href="/"
                class="btn btn-ghost btn-sm text-xl font-bold tracking-tighter hover:bg-white/10"
            >
                lluambo<span class="text-cyan-400 animate-cursor font-black"
                    >_</span
                >
            </a>
        </div>
        <div class="navbar-center hidden sm:flex">
            <ul class="menu menu-horizontal px-1 gap-1">
                {#each links as link}
                    <li>
                        <a
                            href={link.href}
                            class="rounded-full font-medium text-gray-200 hover:bg-white/10 hover:text-white transition-all"
                            >{link.name}</a
                        >
                    </li>
                {/each}
            </ul>
        </div>
        <div class="navbar-end sm:hidden">
            <div class="dropdown dropdown-end">
                <div
                    tabindex="0"
                    role="button"
                    class="btn btn-ghost btn-circle text-white"
                >
                    <svg
                        xmlns="http://www.w3.org/2000/svg"
                        class="h-5 w-5"
                        fill="none"
                        viewBox="0 0 24 24"
                        stroke="currentColor"
                        ><path
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            stroke-width="2"
                            d="M4 6h16M4 12h16M4 18h7"
                        /></svg
                    >
                </div>
                <ul
                    tabindex="-1"
                    class="menu menu-sm dropdown-content mt-3 z-[1] p-2 shadow-lg bg-gray-900 border border-white/10 rounded-box w-52 text-white"
                >
                    {#each links as link}
                        <li><a href={link.href}>{link.name}</a></li>
                    {/each}
                </ul>
            </div>
        </div>
    </div>
</div>

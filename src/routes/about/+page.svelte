<script lang="ts">
    import Header from "$lib/components/Header.svelte";
    import Footer from "$lib/components/Footer.svelte";
    import Experience from "$lib/components/Experience.svelte";
    import Certificates from "$lib/components/Certificates.svelte";

    const navLinks = [
        { name: "Home", href: "/" },
        { name: "About", href: "/about" },
        { name: "Projects", href: "/#projects" },
        { name: "Contact", href: "/contact" },
    ];

    const skills = [
        "Svelte 5",
        "SvelteKit",
        "Tailwind CSS",
        "TypeScript",
        "Node.js",
        "Vanta.js",
        "Blender",
        "Git",
        "Python",
        "Three.js",
        "DaisyUI",
        "WebGL",
    ];
</script>

<div
    class="min-h-screen font-sans selection:bg-cyan-500 selection:text-white text-white"
>
    <Header links={navLinks} />

    <main class="container mx-auto px-4 pt-32 pb-20">
        <div class="max-w-6xl mx-auto">
            <div class="mb-12 text-center md:text-left">
                <h1 class="text-5xl md:text-7xl font-black mb-6 text-white">
                    About <span
                        class="text-transparent bg-clip-text bg-linear-to-r from-cyan-300 to-purple-400"
                        >Me</span
                    >
                </h1>
                <div
                    class="h-1 w-24 bg-cyan-500 rounded-full mx-auto md:mx-0 shadow-[0_0_10px_#22d3ee]"
                ></div>
            </div>

            <div
                class="card bg-black/40 backdrop-blur-xl border border-white/10 p-8 md:p-12 shadow-2xl mb-24"
            >
                <div class="grid md:grid-cols-3 gap-12">
                    <div class="md:col-span-2 space-y-6">
                        <h2 class="text-2xl font-bold text-white mb-4">
                            A bit about Journey
                        </h2>
                        <div
                            class="prose prose-lg prose-p:text-gray-300 prose-strong:text-cyan-300 max-w-none"
                        >
                            <p>
                                I have always been a person who like to solve
                                problems, at first that was with simple python
                                scripts, but as I continued working more and
                                more on simple projects, I though why not try
                                make them available to the world, and the
                                simplest way was through the web. To be honest
                                back in the day I learnt php and html to make
                                simple websites but I hated the experience, so I
                                ditched web development for a while, until in
                                2025 when I decided to give it another chance
                                cause of a random idea I had for a
                                project(coming soon) and that's when I
                                discovered Svelte and SvelteKit as i was
                                learning javaScript and TypeScript, and from
                                there I was hooked.
                            </p>
                            <p>
                                For me the most important thing about a language
                                or framework is that it makes sense to me and
                                Svelte does just that. Does a lot of the things
                                behind the scenes making development a breeze
                                and fun. Big shoutout to one of my friends
                                Benin,you can check out his work <a
                                    href="https://frstudios.co.ke/BeninMukabanah"
                                    class="text-cyan-400 underline hover:text-cyan-300"
                                    >here</a
                                > who introduced me to SvelteKit.
                            </p>
                            <p>
                                Currently, I am focusing deeply on the <strong
                                    >Svelte 5</strong
                                > making things that fix problems and look amazing
                                as they fix them.
                            </p>
                        </div>
                        <div class="md:col-span-2 space-y-6">
                            <h2 class="text-2xl font-bold text-white mb-4">
                                What am I working on <span
                                    class="text-transparent bg-clip-text bg-linear-to-r from-cyan-300 to-purple-400"
                                    >Now</span
                                >
                            </h2>

                            <div
                                class="prose prose-lg prose-p:text-gray-300 prose-strong:text-cyan-300 max-w-none"
                            >
                                <p>
                                    Next steps is what I can do to make websites
                                    look even better with <strong
                                        >Svelte 5</strong
                                    > so stay tuned and come visit the webstie from
                                    time to time to see what im upto. I also have
                                    my resume downloadable below if you want to see
                                    my experience and skills in detail. Always happy
                                    to connect so feel free to reach out, my linkedin
                                    and github are linked in the footer.
                                </p>
                            </div>

                            <div class="pt-4">
                                <a
                                    href="/Lucas_Luambo_Resume.pdf"
                                    download="Lucas_Luambo_Resume.pdf"
                                    class="btn btn-outline border-cyan-500 text-cyan-400 hover:bg-cyan-500 hover:text-black hover:border-cyan-500 gap-3 group"
                                >
                                    <svg
                                        xmlns="http://www.w3.org/2000/svg"
                                        class="h-5 w-5 transition-transform group-hover:translate-y-1"
                                        fill="none"
                                        viewBox="0 0 24 24"
                                        stroke="currentColor"
                                    >
                                        <path
                                            stroke-linecap="round"
                                            stroke-linejoin="round"
                                            stroke-width="2"
                                            d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4"
                                        />
                                    </svg>
                                    Download Resume
                                </a>
                            </div>
                        </div>
                    </div>

                    <div class="space-y-8">
                        <div
                            class="bg-white/5 rounded-xl p-6 border border-white/5"
                        >
                            <h3
                                class="text-xl font-bold mb-4 text-white border-b border-white/10 pb-2"
                            >
                                Tech Stack
                            </h3>
                            <div class="flex flex-wrap gap-2">
                                {#each skills as skill}
                                    <span
                                        class="badge badge-lg badge-outline border-purple-500/50 text-purple-200 hover:bg-purple-500/20 transition-colors py-4"
                                    >
                                        {skill}
                                    </span>
                                {/each}
                            </div>
                        </div>

                        <div
                            class="bg-linear-to-br from-cyan-900/20 to-purple-900/20 rounded-xl p-6 border border-cyan-500/20"
                        >
                            <h3
                                class="text-lg font-bold text-cyan-200 mb-2 flex items-center gap-2"
                            >
                                <span
                                    class="w-2 h-2 rounded-full bg-cyan-400 animate-pulse"
                                ></span> Open to connect
                            </h3>
                            <p class="text-sm text-gray-400 mb-4">
                                I'm currently available for freelance projects
                                and full-time roles.
                            </p>
                            <a
                                href="/contact"
                                class="btn btn-sm btn-primary w-full shadow-lg shadow-cyan-500/20"
                                >Contact me</a
                            >
                        </div>
                    </div>
                </div>
            </div>

            <Experience />
            <Certificates />
        </div>
    </main>

    <Footer />
</div>

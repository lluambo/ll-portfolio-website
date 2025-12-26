<script lang="ts">
    import Header from "$lib/components/Header.svelte";
    import Footer from "$lib/components/Footer.svelte";
    import Experience from "$lib/components/Experience.svelte";
    import Certificates from "$lib/components/Certificates.svelte";

    const navLinks = [
        { name: "Home", href: "/" },
        { name: "About", href: "/about" },
        { name: "Projects", href: "/#projects" },
        { name: "Contact", href: "/#contact" },
    ];

    const skills = [
        "Svelte 5",
        "SvelteKit",
        "Tailwind CSS",
        "TypeScript",
        "Node.js",
        "Vanta.js",
        "Figma",
        "Git",
        "PostgreSQL",
        "Three.js",
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
                        class="text-transparent bg-clip-text bg-gradient-to-r from-cyan-300 to-purple-400"
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
                            My Journey
                        </h2>
                        <div
                            class="prose prose-lg prose-p:text-gray-300 prose-strong:text-cyan-300 max-w-none"
                        >
                            <p>
                                I specialize in building accessible, inclusive
                                products and digital experiences. I enjoy
                                turning complex problems into simple, beautiful,
                                and intuitive designs.
                            </p>
                            <p>
                                My journey began with a curiosity for how things
                                work on the web, which quickly turned into a
                                passion for full-stack development. When I'm not
                                pushing pixels, you'll find me exploring new
                                technologies, contributing to open source, or
                                optimizing performance metrics.
                            </p>
                            <p>
                                Currently, I am focusing deeply on the <strong
                                    >Svelte 5</strong
                                > ecosystem and creating interactive 3D web experiences
                                using WebGL.
                            </p>
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
                            class="bg-gradient-to-br from-cyan-900/20 to-purple-900/20 rounded-xl p-6 border border-cyan-500/20"
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
                                href="/#contact"
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

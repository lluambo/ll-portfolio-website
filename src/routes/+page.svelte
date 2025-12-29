<script lang="ts">
    import Header from "$lib/components/Header.svelte";
    import Footer from "$lib/components/Footer.svelte";
    import Pic from "$lib/assets/landingPictures/landing_pic.png";
    import PersonalPortfolio from "$lib/assets/projects/personal-portfolio.png";

    //Navigation Links
    const navLinks = [
        { name: "Home", href: "/" },
        { name: "About", href: "/about" },
        { name: "Projects", href: "/#projects" },
        { name: "Contact", href: "/contact" },
    ];

    // Projects Data
    const projects = [
        {
            slug: "Personal-Portfolio",
            name: "Personal Portfolio",
            tag: "SvelteKit",
            img: PersonalPortfolio,
            desc: "A personal portfolio website built with SvelteKit and Tailwind CSS.",
        },
        /*  {
            slug: "beta-app",
            name: "Beta App",
            tag: "Mobile",
            img: "https://picsum.photos/400/250?random=2",
            desc: "test description for beta app.",
        },
        {
            slug: "gamma-dash",
            name: "Gamma Dash",
            tag: "Dashboard",
            img: "https://picsum.photos/400/250?random=3",
            desc: "test description for gamma dash.",
            },*/
        //uncomment above projects when adding more projects
    ];
</script>

<div
    class="min-h-screen font-sans selection:bg-cyan-500 selection:text-white text-white"
>
    <Header links={navLinks} />

    <section
        class="min-h-screen flex items-center justify-center pt-24 pb-10 relative overflow-hidden"
    >
        <div
            class="container mx-auto px-4 z-10 grid lg:grid-cols-2 gap-12 items-center"
        >
            <div class="text-center lg:text-left order-2 lg:order-1">
                <div
                    class="text-center lg:text-left order-2 lg:order-1
                                       bg-black/60 md:bg-transparent
                                       backdrop-blur-md md:backdrop-blur-none
                                       p-6 md:p-0
                                       rounded-2xl md:rounded-none
                                       border border-white/10 md:border-none
                                       shadow-2xl md:shadow-none"
                >
                    <div class="inline-block mb-6">
                        <div
                            class="badge badge-lg border-cyan-500/50 bg-cyan-900/30 text-cyan-100 p-4 gap-2 backdrop-blur-sm shadow-[0_0_15px_rgba(34,211,238,0.2)]"
                        >
                            <span
                                class="w-2 h-2 rounded-full bg-cyan-400 animate-pulse"
                            ></span>
                            Available for work
                        </div>
                    </div>

                    <h1
                        class="text-5xl md:text-7xl font-black mb-6 tracking-tight leading-tight drop-shadow-2xl"
                    >
                        Yoh, I'm <span
                            class="text-transparent bg-clip-text bg-linear-to-r from-cyan-300 to-purple-400"
                            >Lucas Luambo</span
                        >
                    </h1>

                    <p
                        class="text-lg md:text-xl text-gray-300 max-w-xl mx-auto lg:mx-0 mb-10 leading-relaxed font-light prose-strong:text-cyan-300"
                    >
                        Im a passionate developer who loves building amazing
                        digital experiences. Currently, I'm focused on making
                        responsive web applications using <strong>Svelte</strong
                        >
                        as my frontend and
                        <strong>SvelteKit</strong> as my backend.
                    </p>

                    <div
                        class="flex flex-wrap gap-4 justify-center lg:justify-start"
                    >
                        <a
                            href="/about"
                            class="btn bg-cyan-500 hover:bg-cyan-400 text-black border-none btn-lg rounded-full px-8 shadow-[0_0_20px_rgba(34,211,238,0.4)]"
                        >
                            More About Me
                        </a>
                        <a
                            href="#projects"
                            class="btn btn-outline btn-lg rounded-full px-8 backdrop-blur-md bg-white/5 border-white/20 text-white hover:bg-white hover:text-black hover:border-white"
                        >
                            View Projects
                        </a>
                    </div>
                </div>
            </div>

            <div class="relative order-1 lg:order-2 flex justify-center">
                <div
                    class="absolute inset-0 bg-linear-to-tr from-cyan-500/30 to-purple-500/30 blur-[80px] rounded-full w-3/4 h-3/4 m-auto -z-10"
                ></div>
                <img
                    src={Pic}
                    alt="Developer Portrait"
                    class="relative z-10 w-full max-w-md object-contain drop-shadow-[0_0_15px_rgba(255,255,255,0.15)] hover:scale-105 transition-transform duration-500 rounded-2xl"
                />
            </div>
        </div>
    </section>

    <section id="projects" class="py-20 px-4">
        <div class="container mx-auto max-w-5xl">
            <div
                class="flex flex-col md:flex-row justify-between items-center md:items-end mb-12 gap-4 bg-black/60 backdrop-blur-md p-6 rounded-2xl border border-white/10 shadow-lg"
            >
                <h2
                    class="text-3xl font-bold text-white flex items-center gap-3"
                >
                    Some of my<span
                        class="text-transparent bg-clip-text bg-linear-to-r from-cyan-300 to-purple-400"
                        >Projects</span
                    >
                </h2>
                <a
                    href="https://github.com/lluambo"
                    class="btn btn-sm btn-ghost text-cyan-300 hover:text-cyan-200 hover:bg-white/10"
                    >View Github -></a
                >
            </div>

            <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
                {#each projects as project}
                    <a
                        href="/projects/{project.slug}"
                        class="group card bg-black/40 backdrop-blur-xl border border-white/10 overflow-hidden hover:shadow-[0_0_30px_rgba(34,211,238,0.15)] hover:border-cyan-500/30 transition-all duration-500 block text-left"
                    >
                        <figure class="relative h-48 overflow-hidden">
                            <img
                                src={project.img}
                                alt={project.name}
                                class="w-full h-full object-cover transition-transform duration-700 group-hover:scale-110"
                            />
                            <div
                                class="absolute inset-0 bg-black/50 group-hover:bg-transparent transition-colors duration-300"
                            ></div>
                        </figure>
                        <div class="card-body p-6">
                            <div class="flex justify-between items-start">
                                <h3
                                    class="card-title text-xl text-white group-hover:text-cyan-300 transition-colors"
                                >
                                    {project.name}
                                </h3>
                                <div
                                    class="badge badge-xs badge-primary badge-outline mt-1"
                                >
                                    {project.tag}
                                </div>
                            </div>
                            <p class="text-gray-400 text-sm mt-2">
                                {project.desc}
                            </p>
                        </div>
                    </a>
                {/each}
            </div>
        </div>
    </section>

    <Footer />
</div>

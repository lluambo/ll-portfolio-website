<script lang="ts">
    import Header from "$lib/components/Header.svelte";
    import Footer from "$lib/components/Footer.svelte";
    import PersonalPortfolio from "$lib/assets/projects/personal-portfolio.png";
    import { page } from "$app/state";

    // Helper to get slug from URL
    const slug = $derived(page.params.slug);

    const allProjects = {
        "Personal-Portfolio": {
            name: "Personal Portfolio",
            tag: "Svelte, SvelteKit and Tailwind CSS",
            img: PersonalPortfolio,
            desc: "A personal portfolio website built with SvelteKit and Tailwind CSS.",
            content: `
                <p class="mb-6 leading-relaxed">
                    I built this site to be more than just a digital resume—it's a playground where I can experiment with Svelte.
                    My goal was to create something that <strong>works</strong> and has my own personal touch, rather than just a static list of skills.
                    It was also the perfect excuse to start learning <strong>Svelte 5</strong> and its ecosystem.
                </p>

                <h3 class="text-2xl font-bold text-white mb-4 mt-8">What makes it special?</h3>
                <ul class="list-disc list-inside space-y-4 text-gray-300 mb-8">
                    <li>
                        <strong class="text-cyan-400">A Background that Moves with You:</strong>
                        I didn't want a simple background. Because of this I spent a long while getting <span class="text-white">Vanta.js</span> and <span class="text-white">Three.js</span> to create a 3D net effect that actually reacts to your mouse movement. It gives the site a personal touch and is something to look forward to in my next projects.
                    </li>
                    <li>
                        <strong class="text-cyan-400">New and Improved Svelte5</strong>
                        Svelte 5 just recently released so I decided to build this entirely on <span class="text-white">Svelte 5</span> after a recomendation from a friend and to get into the new tech running. At first I was going to use react or simple javascipt but Svelte just felt right. It was a learning curve coming, but the result is a website that feels incredibly snappy and lightweight.
                    </li>
                    <li>
                        <strong class="text-cyan-400">Creative Problem Solving:</strong>
                        I needed a contact form but didn't want to pay for a backend server. My solution? I found a way to use Google Forms to act as my API. This was my first deep dive into Svlete and I wanted somtehing simple. Now, messages are sent directly to my personal Google Sheets for free.
                    </li>
                </ul>

                <h3 class="text-2xl font-bold text-white mb-4">Why <strong>Svelte?</strong></h3>
                <p class="leading-relaxed">
                    I chose Svelte 5 because I wanted something that works and is fun to work with. The code is cleaner, the bundle size is smaller, and honestly, it’s just really fun to write compared to other frameworks.
                </p>
            `,
        },
        /* , // Note: When you add more projects, put a comma after the closing bracket above: },
        "beta-app": {
            name: "Beta App",
            tag: "Mobile",
            img: "https://picsum.photos/800/400?random=2",
            desc: "React Native fitness tracking application.",
            content: `<p>A cross-platform mobile app designed to help users track their fitness goals using device sensors.</p>`,
        },
        "gamma-dash": {
            name: "Gamma Dash",
            tag: "Dashboard",
            img: "https://picsum.photos/800/400?random=3",
            desc: "Real-time crypto analytics platform.",
            content: `<p>High-frequency data visualization using D3.js and WebSockets to track market movements in real-time.</p>`,
        }
        */
    };

    // Fallback if project isn't found
    let project = $derived(
        allProjects[slug as keyof typeof allProjects] || {
            name: "Project Not Found",
            tag: "Error",
            img: "",
            desc: "This project does not exist.",
            content: "<p>Please go back and select a valid project.</p>",
        },
    );

    const navLinks = [
        { name: "Home", href: "/" },
        { name: "About", href: "/about" },
        { name: "Projects", href: "/#projects" },
        { name: "Contact", href: "/contact" },
    ];
</script>

<div
    class="min-h-screen font-sans selection:bg-cyan-500 selection:text-white text-white"
>
    <Header links={navLinks} />

    <main class="container mx-auto px-4 pt-32 pb-20">
        <article class="max-w-4xl mx-auto">
            <a
                href="/#projects"
                class="btn btn-ghost btn-sm mb-8 pl-0 text-gray-300 hover:bg-white/10 hover:text-white transition-all"
            >
                ← Back to Projects
            </a>

            <div class="mb-10">
                <div
                    class="badge badge-lg badge-outline text-cyan-300 border-cyan-500/50 mb-4 shadow-[0_0_10px_rgba(34,211,238,0.3)]"
                >
                    {project.tag}
                </div>
                <h1
                    class="text-4xl md:text-6xl font-black text-white mb-6 leading-tight drop-shadow-lg"
                >
                    {project.name}
                </h1>
                <p
                    class="text-xl text-gray-200 leading-relaxed max-w-2xl font-light"
                >
                    {project.desc}
                </p>
            </div>

            <figure
                class="w-full h-64 md:h-96 rounded-2xl overflow-hidden mb-12 shadow-[0_0_40px_rgba(0,0,0,0.5)] border border-white/10 relative group"
            >
                {#if project.img}
                    <img
                        src={project.img}
                        alt={project.name}
                        class="w-full h-full object-cover transition-transform duration-700 group-hover:scale-105"
                    />
                {:else}
                    <div
                        class="w-full h-full bg-white/5 flex items-center justify-center text-gray-500"
                    >
                        No Image Available
                    </div>
                {/if}
                <div
                    class="absolute inset-0 bg-linear-to-t from-black/60 to-transparent"
                ></div>
            </figure>

            <div
                class="card bg-black/60 backdrop-blur-xl border border-white/10 p-8 md:p-12 shadow-2xl"
            >
                <div
                    class="prose prose-lg max-w-none
                    prose-headings:text-white prose-headings:font-bold
                    prose-p:text-gray-300 prose-p:leading-relaxed
                    prose-li:text-gray-300
                    prose-strong:text-cyan-300
                    prose-a:text-cyan-400 hover:prose-a:text-cyan-300
                    prose-blockquote:text-gray-400 prose-blockquote:border-l-cyan-500"
                >
                    {@html project.content}
                </div>
            </div>
        </article>
    </main>

    <Footer />
</div>

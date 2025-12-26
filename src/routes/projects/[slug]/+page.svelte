<script lang="ts">
    import Header from "$lib/components/Header.svelte";
    import Footer from "$lib/components/Footer.svelte";
    import { page } from "$app/state";

    // Helper to get slug from URL
    const slug = $derived(page.params.slug);

    const allProjects = {
        "project-alpha": {
            name: "Project Alpha",
            tag: "SvelteKit",
            img: "https://picsum.photos/800/400?random=1",
            desc: "A full-stack e-commerce dashboard built with SvelteKit and Supabase.",
            content: `
				<p>This project was built to solve the issue of complex state management in e-commerce dashboards.</p>
				<h3>Key Features</h3>
				<ul>
					<li>Real-time inventory tracking via WebSockets</li>
					<li>User role management with Row Level Security</li>
					<li>Automated sales reporting emails</li>
				</ul>
				<h3>Technology</h3>
				<p>We utilized <strong>Svelte 5's runes</strong> for granular reactivity, resulting in a 40% performance boost over the previous React version.</p>
			`,
        },
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
        },
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
        { name: "Contact", href: "/#contact" },
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
                    class="absolute inset-0 bg-gradient-to-t from-black/60 to-transparent"
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

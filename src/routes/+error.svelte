<script lang="ts">
    import { page } from "$app/stores";
    import Header from "$lib/components/Header.svelte";
    import Footer from "$lib/components/Footer.svelte";

    const navLinks = [
        { name: "Home", href: "/" },
        { name: "About", href: "/about" },
        { name: "Projects", href: "/#projects" },
        { name: "Contact", href: "/contact" },
    ];
</script>

<div
    class="min-h-screen font-sans selection:bg-cyan-500 selection:text-white text-white flex flex-col"
>
    <Header links={navLinks} />

    <main
        class="grow flex flex-col items-center justify-center text-center px-4 relative overflow-hidden"
    >
        <div
            class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-96 h-96 bg-purple-600/20 rounded-full blur-[120px] -z-10"
        ></div>

        <h1
            class="text-9xl font-black text-transparent bg-clip-text bg-linear-to-r from-cyan-400 to-purple-600 mb-4 drop-shadow-[0_0_30px_rgba(168,85,247,0.5)]"
        >
            404
        </h1>

        <h2 class="text-2xl md:text-4xl font-bold text-white mb-6">
            Page Not Found
        </h2>

        <p class="text-gray-400 max-w-md mb-8 text-lg">
            It looks like you've ventured into the void. The page you are
            looking for doesn't exist or has been moved.
        </p>

        <a
            href="/"
            class="btn btn-outline border-cyan-500 text-cyan-400 hover:bg-cyan-500 hover:text-black hover:border-cyan-500 gap-2 group px-8"
        >
            <svg
                xmlns="http://www.w3.org/2000/svg"
                class="h-5 w-5 transition-transform group-hover:-translate-x-1"
                fill="none"
                viewBox="0 0 24 24"
                stroke="currentColor"
                ><path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M10 19l-7-7m0 0l7-7m-7 7h18"
                /></svg
            >
            Return Home
        </a>
    </main>

    <Footer />
</div>

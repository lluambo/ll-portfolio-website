<script>
    import "./layout.css";
    import favicon from "$lib/assets/favicon.svg";
    import Background from "$lib/components/Background.svelte";

    let { children } = $props();
</script>

<svelte:head>
    <link rel="icon" type="image/svg+xml" href={favicon} />
    <title>Lucas Luambo | Fullstack Developer</title>
    <meta
        name="description"
        content="Portfolio of Lucas Luambo, a Fullstack Developer specializing in SvelteKit and WebGL."
    />

    <meta property="og:title" content="Lucas Luambo | Fullstack Developer" />
    <meta
        property="og:description"
        content="Check out my interactive 3D portfolio."
    />
    <meta
        property="og:image"
        content="https://ll-portfolio-website.vercel.app/og-image.jpg"
    />
    <meta
        property="og:url"
        content="https://ll-portfolio-website.vercel.app/"
    />
</svelte:head>

<Background />

<div class="relative z-10">
    {@render children()}
</div>

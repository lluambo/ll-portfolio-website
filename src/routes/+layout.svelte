<script>
    import "./layout.css";
    import favicon from "$lib/assets/favicon.svg";
    import Background from "$lib/components/Background.svelte";

    let { children } = $props();
</script>

<svelte:head>
    <link rel="icon" type="image/svg+xml" href={favicon} />
</svelte:head>

<Background />

<div class="relative z-10">
    {@render children()}
</div>

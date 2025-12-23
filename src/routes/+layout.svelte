<script>
    import "./layout.css";
    import favicon from "$lib/assets/favicon.svg";
    // Adjust the path below to match where you saved the component
    import Background from "$lib/components/Background.svelte";

    let { children } = $props();
</script>

<svelte:head>
    <link rel="icon" href={favicon} />
</svelte:head>

<Background />

<div class="relative z-10">
    {@render children()}
</div>

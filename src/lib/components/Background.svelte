<script>
    import { onDestroy } from "svelte";

    let vantaRef = $state();
    let vantaEffect = null;

    // We define these outside the effect to ensure we don't load scripts twice
    // even if the component remounts rapidly.
    const THREE_CDN =
        "https://cdnjs.cloudflare.com/ajax/libs/three.js/r134/three.min.js";
    const VANTA_CDN =
        "https://cdnjs.cloudflare.com/ajax/libs/vanta/0.5.24/vanta.globe.min.js";

    const loadScript = (src) => {
        return new Promise((resolve, reject) => {
            // 1. Check if script is already in the DOM
            if (document.querySelector(`script[src="${src}"]`)) {
                resolve();
                return;
            }
            // 2. If not, create it
            const s = document.createElement("script");
            s.src = src;
            s.async = true;
            s.onload = () => resolve(s);
            s.onerror = reject;
            document.head.appendChild(s);
        });
    };

    $effect(() => {
        // Only run if DOM is ready
        if (!vantaRef) return;
        // Only run if not already initialized
        if (vantaEffect) return;

        let cancelled = false;

        const init = async () => {
            try {
                // 1. Load THREE.js (r134 specifically for Vanta compatibility)
                if (!window.THREE) {
                    await loadScript(THREE_CDN);
                }

                // 2. Load Vanta
                if (!window.VANTA) {
                    await loadScript(VANTA_CDN);
                }

                if (cancelled) return;

                // 3. Initialize
                // We use a small timeout to ensure the global variables are fully settled
                // sometimes purely awaiting the script load isn't enough for the global scope execution
                await new Promise((r) => setTimeout(r, 50));

                const VANTA = window.VANTA;

                if (VANTA && VANTA.GLOBE) {
                    vantaEffect = VANTA.GLOBE({
                        el: vantaRef,
                        THREE: window.THREE, // Pass the window instance explicitly
                        mouseControls: true,
                        touchControls: true,
                        gyroControls: false,
                        minHeight: 200.0,
                        minWidth: 200.0,
                        scale: 1.0,
                        scaleMobile: 1.0,
                        color: 0x50a0fc,
                        size: 1.3,
                        backgroundColor: 0x050509, // Ensure 6-digit hex code
                    });
                } else {
                    console.error(
                        "[Background] VANTA or VANTA.GLOBE is missing after loading scripts.",
                    );
                }
            } catch (err) {
                console.error("[Background] Failed to load 3D scripts:", err);
            }
        };

        init();

        // Cleanup
        return () => {
            cancelled = true;
            if (vantaEffect) {
                vantaEffect.destroy();
                vantaEffect = null;
            }
        };
    });
</script>

<div
    bind:this={vantaRef}
    class="fixed inset-0 z-0 pointer-events-none w-full h-screen"
    style="background-color: #050509;"
></div>

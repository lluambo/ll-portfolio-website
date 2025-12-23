<script>
    let vantaRef = $state();
    let vantaEffect;
    let injectedScripts = [];

    const injectScript = (src) =>
        new Promise((res, rej) => {
            const s = document.createElement("script");
            s.src = src;
            s.async = true;
            s.onload = () => res(s);
            s.onerror = rej;
            document.head.appendChild(s);
            injectedScripts.push(s);
        });

    $effect(() => {
        if (!vantaRef) return;

        let initialized = false;

        const initVanta = async () => {
            try {
                const THREEmod = await import("three");
                const THREE = THREEmod.default || THREEmod;
                const vantaMod = await import("vanta/dist/vanta.globe.min");
                const VANTA =
                    vantaMod.default || vantaMod || (window && window.VANTA);

                if (VANTA && typeof VANTA.GLOBE === "function") {
                    vantaEffect = VANTA.GLOBE({
                        el: vantaRef,
                        THREE,
                        mouseControls: true,
                        touchControls: true,
                        gyroControls: false,
                        minHeight: 200.0,
                        minWidth: 200.0,
                        scale: 1.0,
                        scaleMobile: 1.0,
                        color: 0x50a0fc,
                        size: 1.3,
                        backgroundColor: 0x50509,
                    });
                    initialized = true;
                }
            } catch (err) {
                console.debug("Vanta dynamic import failed, will try CDN", err);
            }

            if (!initialized) {
                try {
                    if (!window.THREE) {
                        await injectScript(
                            "https://cdnjs.cloudflare.com/ajax/libs/three.js/r134/three.min.js",
                        );
                    }
                    await injectScript(
                        "https://cdnjs.cloudflare.com/ajax/libs/vanta/0.5.24/vanta.globe.min.js",
                    );

                    const VANTA = window.VANTA || (window && window.VANTA);
                    if (VANTA && typeof VANTA.GLOBE === "function") {
                        vantaEffect = VANTA.GLOBE({
                            el: vantaRef,
                            THREE: window.THREE,
                            mouseControls: true,
                            touchControls: true,
                            gyroControls: false,
                            minHeight: 200.0,
                            minWidth: 200.0,
                            scale: 1.0,
                            scaleMobile: 1.0,
                            color: 0x50a0fc,
                            size: 1.3,
                            backgroundColor: 0x50509,
                        });
                    }
                } catch (err) {
                    console.error("Vanta CDN fallback failed", err);
                }
            }
        };

        initVanta();

        return () => {
            if (vantaEffect && typeof vantaEffect.destroy === "function") {
                vantaEffect.destroy();
                vantaEffect = null;
            }
            for (const s of injectedScripts) {
                if (s && s.parentNode) s.parentNode.removeChild(s);
            }
            injectedScripts = [];
        };
    });
</script>

<div
    bind:this={vantaRef}
    class="fixed inset-0 z-0 pointer-events-none w-full h-screen"
    aria-hidden="true"
></div>

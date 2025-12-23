<script>
	import './layout.css';
	import favicon from '$lib/assets/favicon.svg';
	import { onMount } from 'svelte';

	let { children } = $props();
	let vantaRef;
	let vantaEffect;
	let injectedScripts = [];

	const injectScript = (src) =>
		new Promise((res, rej) => {
			const s = document.createElement('script');
			s.src = src;
			s.async = true;
			s.onload = () => res(s);
			s.onerror = rej;
			document.head.appendChild(s);
			injectedScripts.push(s);
		});

	onMount(async () => {
		// wait until the element is bound
		if (!vantaRef) {
			await new Promise((r) => requestAnimationFrame(r));
		}

		// ensure container fills viewport
		if (vantaRef) {
			vantaRef.style.position = 'fixed';
			vantaRef.style.top = '0';
			vantaRef.style.left = '0';
			vantaRef.style.width = '100%';
			vantaRef.style.height = '100vh';
			vantaRef.style.pointerEvents = 'none';
			vantaRef.style.zIndex = '0';
		}

		let initialized = false;

		// try dynamic import first
		try {
			const THREEmod = await import('three');
			const THREE = THREEmod.default || THREEmod;
			const vantaMod = await import('vanta/dist/vanta.globe.min');
			const VANTA = vantaMod.default || vantaMod || (window && window.VANTA);
			if (VANTA && typeof VANTA.GLOBE === 'function') {
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
					backgroundColor: 0x50509
				});
				initialized = true;
			}
		} catch (err) {
			// fall through to CDN fallback
			console.debug('Vanta dynamic import failed, will try CDN fallback', err);
		}

		// CDN fallback: ensure three then vanta globe
		if (!initialized) {
			try {
				// inject three (r134) and vanta globe from CDN
				if (!window.THREE) {
					await injectScript('https://cdnjs.cloudflare.com/ajax/libs/three.js/r134/three.min.js');
				}
				await injectScript('https://cdnjs.cloudflare.com/ajax/libs/vanta/0.5.24/vanta.globe.min.js');
				const VANTA = window.VANTA || (window && window.VANTA);
				if (VANTA && typeof VANTA.GLOBE === 'function') {
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
						backgroundColor: 0x50509
					});
					initialized = true;
				} else {
					console.error('VANTA.GLOBE not available after CDN load');
				}
			} catch (err) {
				console.error('Vanta CDN fallback failed', err);
			}
		}

		// if still not initialized, inspect console for errors
		if (!initialized) console.error('Vanta did not initialize — check imports and console errors');

		return () => {
			if (vantaEffect && typeof vantaEffect.destroy === 'function') {
				vantaEffect.destroy();
				vantaEffect = null;
			}
			// remove injected scripts
			for (const s of injectedScripts) {
				if (s && s.parentNode) s.parentNode.removeChild(s);
			}
			injectedScripts = [];
		};
	});
</script>

<svelte:head><link rel="icon" href={favicon} /></svelte:head>

<!-- Vanta container: fixed full-viewport and z-0 so page content (z-10) sits above it -->
<div bind:this={vantaRef} class="fixed inset-0 z-0 pointer-events-none w-full h-screen" aria-hidden="true"></div>

<!-- ensure your main content has a higher z-index -->
<div class="relative z-10">
	{@render children()}
</div>

<script lang="ts">
    // State for the modal
    let selectedCert: { title: string; image: string } | null = $state(null);

    const certs = [
        {
            title: "AWS Certified Solutions Architect",
            issuer: "Amazon Web Services",
            date: "2023",
            logo: "☁️",
            image: "https://placehold.co/800x600/png?text=AWS+Certificate",
            // ✅ CHANGE 1: Data is now an array [] instead of a long string
            learned: [
                "Cloud architecture",
                "IAM security",
                "Scalable systems",
                "VPC networking",
            ],
        },
        {
            title: "Meta Frontend Developer",
            issuer: "Meta",
            date: "2022",
            logo: "∞",
            image: "https://placehold.co/800x600/png?text=Meta+Certificate",
            // ✅ CHANGE 1: Data is now an array
            learned: [
                "Advanced React",
                "UI/UX principles",
                "Version control",
                "API integration",
            ],
        },
        {
            title: "Google UX Design",
            issuer: "Google",
            date: "2021",
            logo: "G",
            image: "https://placehold.co/800x600/png?text=Google+Certificate",
            // ✅ CHANGE 1: Data is now an array
            learned: [
                "Wireframing",
                "Prototyping in Figma",
                "User research",
                "Accessibility standards",
            ],
        },
    ];

    function openModal(cert: (typeof certs)[0]) {
        selectedCert = cert;
    }

    function closeModal() {
        selectedCert = null;
    }
</script>

<div class="py-20 border-t border-white/10">
    <h2 class="text-3xl font-bold text-white text-center mb-12">
        Licenses & Certifications
    </h2>

    <div
        class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6 max-w-6xl mx-auto px-4"
    >
        {#each certs as cert}
            <button
                onclick={() => openModal(cert)}
                class="card bg-black/40 backdrop-blur-md border border-white/10 p-6 flex flex-col text-left gap-4 hover:bg-white/5 hover:border-cyan-500/30 transition-all duration-300 group h-full"
            >
                <div class="flex flex-row items-center gap-4 w-full">
                    <div
                        class="w-12 h-12 rounded-full bg-white/5 border border-white/10 flex items-center justify-center text-2xl group-hover:scale-110 transition-transform shadow-inner flex-shrink-0"
                    >
                        {cert.logo}
                    </div>

                    <div class="flex-1 min-w-0">
                        <h3
                            class="text-white font-bold truncate group-hover:text-cyan-300 transition-colors"
                        >
                            {cert.title}
                        </h3>
                        <p class="text-sm text-gray-400 truncate">
                            {cert.issuer}
                        </p>
                        <p class="text-xs text-gray-500 mt-1">
                            Issued {cert.date}
                        </p>
                    </div>

                    <div
                        class="text-gray-600 group-hover:text-cyan-400 transition-colors"
                    >
                        <svg
                            xmlns="http://www.w3.org/2000/svg"
                            class="h-5 w-5"
                            fill="none"
                            viewBox="0 0 24 24"
                            stroke="currentColor"
                            ><path
                                stroke-linecap="round"
                                stroke-linejoin="round"
                                stroke-width="2"
                                d="M4 8V4m0 0h4M4 4l5 5m11-1V4m0 0h-4m4 0l-5 5M4 16v4m0 0h4m-4 0l5-5m11 5l-5-5m5 5v-4m0 4h-4"
                            /></svg
                        >
                    </div>
                </div>

                <div class="w-full pt-4 border-t border-white/5 mt-auto">
                    <p
                        class="text-xs font-bold text-cyan-500 mb-3 uppercase tracking-wide"
                    >
                        Key Skills:
                    </p>

                    <div class="flex flex-wrap gap-2">
                        {#each cert.learned as skill}
                            <span
                                class="badge badge-outline border-purple-500/50 text-purple-200 hover:bg-purple-500/20 transition-colors"
                            >
                                {skill}
                            </span>
                        {/each}
                    </div>
                </div>
            </button>
        {/each}
    </div>

    {#if selectedCert}
        <div
            class="fixed inset-0 z-[100] flex items-center justify-center p-4 bg-black/80 backdrop-blur-sm transition-opacity"
            onclick={closeModal}
            role="dialog"
            aria-modal="true"
        >
            <div
                class="relative max-w-4xl w-full bg-black border border-white/10 rounded-xl overflow-hidden shadow-2xl animate-scale-in"
                onclick={(e) => e.stopPropagation()}
            >
                <div
                    class="flex justify-between items-center p-4 border-b border-white/10 bg-white/5"
                >
                    <h3 class="text-lg font-bold text-white">
                        {selectedCert.title}
                    </h3>
                    <button
                        onclick={closeModal}
                        class="btn btn-sm btn-circle btn-ghost text-white hover:bg-white/20"
                        >✕</button
                    >
                </div>

                <div class="p-1 bg-black">
                    <img
                        src={selectedCert.image}
                        alt={selectedCert.title}
                        class="w-full h-auto object-contain max-h-[80vh]"
                    />
                </div>
            </div>
        </div>
    {/if}
</div>

<style>
    @keyframes scale-in {
        from {
            opacity: 0;
            transform: scale(0.95);
        }
        to {
            opacity: 1;
            transform: scale(1);
        }
    }
    .animate-scale-in {
        animation: scale-in 0.2s ease-out forwards;
    }
</style>

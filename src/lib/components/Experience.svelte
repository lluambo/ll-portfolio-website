<script lang="ts">
    import { onMount } from "svelte";
    import { spring } from "svelte/motion";

    const experience = [
        {
            company: "LogicGate",
            period: "2022 - Present",
            role: "Frontend Developer III",
            desc: "Leading feature development on a team analyzing requirements, designing solutions, and assisting in evolving the frontend chapter.",
        },
        {
            company: "Cognizant",
            period: "2019 - 2021",
            role: "Senior Fullstack Developer",
            desc: "Designed and developed full-stack RESTful microservices using Netflix OSS, Java Spring Boot, SQL, Angular, and React.",
        },
        {
            company: "Freelance",
            period: "2017 - 2019",
            role: "Web Developer",
            desc: "Built bespoke websites for local businesses using modern web technologies and CMS solutions.",
        },
        {
            company: "Tech Solutions Inc.",
            period: "2015 - 2017",
            role: "Junior Developer",
            desc: "Assisted in developing internal tools and client projects, gaining experience in both frontend and backend technologies.",
        },
    ];

    let timelineRef: HTMLElement;
    let progress = spring(0, { stiffness: 0.1, damping: 0.4 });

    function handleScroll() {
        if (!timelineRef) return;
        const rect = timelineRef.getBoundingClientRect();
        const viewportHeight = window.innerHeight;

        // Calculate progress based on where the top of the timeline is relative to the viewport center
        // When top of timeline hits center of screen = 0%
        // When bottom of timeline hits center of screen = 100%
        const targetY = viewportHeight / 2;
        const dist = targetY - rect.top;
        const height = rect.height;

        // Calculate percentage (0 to 1)
        let p = dist / height;

        // Clamp between 0 and 1
        p = Math.max(0, Math.min(1, p));

        progress.set(p);
    }

    onMount(() => {
        window.addEventListener("scroll", handleScroll);
        handleScroll(); // Initial check
        return () => window.removeEventListener("scroll", handleScroll);
    });
</script>

<div class="py-20">
    <h2 class="text-3xl font-bold text-white text-center mb-16">
        Work History
    </h2>

    <div class="relative max-w-5xl mx-auto px-4" bind:this={timelineRef}>
        <div
            class="absolute left-4 md:left-1/2 top-2 bottom-0 w-0.5 bg-white/10 -translate-x-1/2 rounded-full"
        ></div>

        <div
            class="absolute left-4 md:left-1/2 top-2 w-0.5 bg-linear-to-b from-cyan-400 to-purple-500 -translate-x-1/2 rounded-full shadow-[0_0_15px_rgba(34,211,238,0.5)] origin-top"
            style="height: {$progress * 100}%;"
        ></div>

        <div
            class="absolute left-4 md:left-1/2 top-0 w-3 h-3 bg-cyan-500 rounded-full -translate-x-1/2 shadow-[0_0_10px_rgba(34,211,238,0.8)] z-10"
        ></div>

        <div
            class="absolute left-4 md:left-1/2 -translate-x-1/2 z-20"
            style="top: {$progress * 100}%"
        >
            <div class="relative -top-6">
                <div
                    class="w-12 h-12 rounded-full border-4 border-black bg-black ring-2 ring-purple-500 shadow-[0_0_20px_rgba(168,85,247,0.6)] overflow-hidden"
                >
                    <img
                        src="https://placehold.co/100x100/png?text=Me"
                        alt="avatar"
                        class="w-full h-full object-cover"
                    />
                </div>
            </div>
        </div>

        <div class="space-y-24 pt-4 pb-12">
            {#each experience as job, i}
                <div
                    class={`relative flex flex-col md:flex-row gap-8 ${i % 2 === 0 ? "md:flex-row-reverse" : ""}`}
                >
                    <div class="hidden md:block flex-1"></div>

                    <div class="flex-1 ml-12 md:ml-0">
                        <div
                            class="card bg-black/40 backdrop-blur-md border border-white/10 p-6 hover:border-cyan-500/30 transition-all hover:-translate-y-1 duration-300"
                        >
                            <div
                                class="flex flex-col sm:flex-row justify-between sm:items-center mb-4 gap-2"
                            >
                                <h3 class="text-xl font-bold text-white">
                                    {job.company}
                                </h3>
                                <span
                                    class="badge badge-primary badge-outline text-xs font-mono"
                                    >{job.period}</span
                                >
                            </div>
                            <h4 class="text-lg text-cyan-300 mb-2 font-medium">
                                {job.role}
                            </h4>
                            <p class="text-gray-400 text-sm leading-relaxed">
                                {job.desc}
                            </p>
                        </div>
                    </div>

                    <div
                        class="absolute left-4 md:left-1/2 top-8 w-4 h-4 bg-black border-2 border-white/20 rounded-full -translate-x-1/2 z-0 shadow-[0_0_10px_black]"
                    ></div>
                </div>
            {/each}
        </div>
    </div>
</div>

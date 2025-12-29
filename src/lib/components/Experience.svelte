<script lang="ts">
    import { onMount } from "svelte";
    import { spring } from "svelte/motion";
    import Pic from "$lib/assets/landingPictures/backup_landing_pic.png";

    const experience = [
        {
            company: "GlobalLogic",
            period: "Sep 2024 - Present",
            role: "Project Support Specialist",
            desc: `
				<p class="mb-4 text-gray-300">I coordinate operations for three language teams, managing technical setups to keep projects running smoothly and teams ready for action.</p>
                <ul class="list-disc list-inside space-y-2">
                    <li><strong class="text-white">Onboarded new hires</strong> by setting up workstations and leading training sessions on project tools, getting them operational from day one.</li>
                    <li><strong class="text-white">Led three language teams</strong>, managing schedules and providing consistent feedback to ensure we hit our project delivery targets.</li>
                    <li>Acting as the <strong class="text-white">primary liaison</strong> between our Wrocław team and global Project Managers to quickly clear up workflow blockers.</li>
                    <li>Troubleshoot <strong class="text-white">technical issues</strong> on internal tools and communicated bugs directly to the client, leading to faster resolutions.</li>
                    <li>Designed <strong class="text-white">process improvements</strong> by deploying new productivity tools that boosted team efficiency and helped us meet client standards.</li>
                </ul>
            `,
        },
        {
            company: "GlobalLogic",
            period: "Aug 2022 - Sep 2024",
            role: "Junior Project Support Specialist",
            desc: `
				<p class="mb-4 text-gray-300">I processed client tickets and supported daily team operations, maintaining high quality standards in a fast-paced environment.</p>
                <ul class="list-disc list-inside space-y-2">
                    <li>Maintained <strong class="text-white">high quality standards</strong> by conducting regular reviews and giving feedback, helping the team sustain 80%+ quality scores.</li>
                    <li>Facilitated <strong class="text-white">knowledge transfer</strong> by mentoring team members on new tools and processes to keep everyone efficient.</li>
                    <li>Demonstrated <strong class="text-white">adaptability</strong> as an early adopter for a new client platform, getting certified before the rest of the team to lead the way.</li>
                    <li>Resolved tickets with a personal <strong class="text-white">95% quality rating</strong>, consistently exceeding the standard benchmarks.</li>
                </ul>
            `,
        },
    ];

    let timelineRef: HTMLElement;
    let progress = spring(0, { stiffness: 0.1, damping: 0.4 });

    function handleScroll() {
        if (!timelineRef) return;
        const rect = timelineRef.getBoundingClientRect();
        const viewportHeight = window.innerHeight;

        const targetY = viewportHeight / 2;
        const dist = targetY - rect.top;
        const height = rect.height;

        let p = dist / height;

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
                        src={Pic}
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

                            <div class="text-gray-400 text-sm leading-relaxed">
                                {@html job.desc}
                            </div>
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

```

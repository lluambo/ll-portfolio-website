<script lang="ts">
    import Header from "$lib/components/Header.svelte";
    import Footer from "$lib/components/Footer.svelte";

    const navLinks = [
        { name: "Home", href: "/" },
        { name: "About", href: "/about" },
        { name: "Projects", href: "/#projects" },
        { name: "Contact", href: "/contact" },
    ];

    // FORM STATE
    let isSubmitting = $state(false);
    let isSuccess = $state(false);

    // GOOGLE FORM CONFIGURATION
    const GOOGLE_FORM_ACTION_URL =
        "https://docs.google.com/forms/d/e/1FAIpQLSfkQWz69YUWq2cFAJ5vbQStncv6O7_u124h24yYT-Tde6dfdw/formResponse";

    const ENTRY_NAME = "entry.951355377";
    const ENTRY_EMAIL = "entry.590909460";
    const ENTRY_MESSAGE = "entry.186434413";

    async function handleSubmit(e: SubmitEvent) {
        e.preventDefault();
        isSubmitting = true;

        const form = e.target as HTMLFormElement;
        const data = new FormData(form);

        try {
            await fetch(GOOGLE_FORM_ACTION_URL, {
                method: "POST",
                mode: "no-cors",
                body: data,
            });

            isSuccess = true;
            form.reset();
            setTimeout(() => (isSuccess = false), 5000);
        } catch (error) {
            console.error("Error submitting form:", error);
            alert("Something went wrong. Please try again.");
        } finally {
            isSubmitting = false;
        }
    }
</script>

<div
    class="min-h-screen font-sans selection:bg-cyan-500 selection:text-white text-white"
>
    <Header links={navLinks} />

    <main
        class="container mx-auto px-4 pt-32 pb-20 flex flex-col items-center justify-center min-h-[85vh]"
    >
        <div class="text-center mb-12">
            <h1
                class="text-5xl md:text-7xl font-black mb-6 text-white drop-shadow-2xl"
            >
                Get in <span
                    class="text-transparent bg-clip-text bg-linear-to-r from-cyan-300 to-purple-400"
                    >Touch</span
                >
            </h1>
            <p
                class="text-lg md:text-xl text-gray-300 max-w-xl mx-auto leading-relaxed"
            >
                Have a project in mind or just want to say hi? <br
                    class="hidden md:block"
                />
                Fill out the form below and I'll get back to you.
            </p>
        </div>

        <div
            class="card w-full max-w-2xl bg-black/60 backdrop-blur-2xl border border-white/10 shadow-[0_0_50px_rgba(0,0,0,0.6)] p-8 md:p-12 relative overflow-hidden rounded-3xl"
        >
            {#if isSuccess}
                <div
                    class="absolute inset-0 bg-black/90 flex flex-col items-center justify-center z-20 animate-fade-in text-center p-8 backdrop-blur-sm"
                >
                    <div
                        class="w-20 h-20 bg-green-500 rounded-full flex items-center justify-center mb-6 shadow-[0_0_30px_#22c55e]"
                    >
                        <svg
                            xmlns="http://www.w3.org/2000/svg"
                            class="h-10 w-10 text-black"
                            fill="none"
                            viewBox="0 0 24 24"
                            stroke="currentColor"
                            stroke-width="3"
                            ><path
                                stroke-linecap="round"
                                stroke-linejoin="round"
                                d="M5 13l4 4L19 7"
                            /></svg
                        >
                    </div>
                    <h3 class="text-3xl font-bold text-white mb-3">
                        Message Sent!
                    </h3>
                    <p class="text-gray-400 text-lg">
                        Thanks for reaching out. I'll be in touch shortly.
                    </p>
                    <button
                        class="btn btn-outline btn-wide text-white mt-8 hover:bg-white hover:text-black transition-all"
                        onclick={() => (isSuccess = false)}>Send Another</button
                    >
                </div>
            {/if}

            <form onsubmit={handleSubmit} class="flex flex-col gap-6">
                <div class="grid md:grid-cols-2 gap-6">
                    <div class="form-control w-full">
                        <label class="label pl-1" for="name-input">
                            <span
                                class="label-text text-gray-300 font-medium text-base"
                                >Name</span
                            >
                        </label>
                        <input
                            type="text"
                            name={ENTRY_NAME}
                            placeholder="John Doe"
                            required
                            class="input input-lg w-full bg-white/5 border-white/10 text-white placeholder-gray-500 focus:bg-white/10 focus:border-cyan-500 focus:outline-none transition-all rounded-xl"
                        />
                    </div>

                    <div class="form-control w-full">
                        <label class="label pl-1" for="email-input">
                            <span
                                class="label-text text-gray-300 font-medium text-base"
                                >Email</span
                            >
                        </label>
                        <input
                            type="email"
                            name={ENTRY_EMAIL}
                            placeholder="john@example.com"
                            required
                            class="input input-lg w-full bg-white/5 border-white/10 text-white placeholder-gray-500 focus:bg-white/10 focus:border-cyan-500 focus:outline-none transition-all rounded-xl"
                        />
                    </div>
                </div>

                <div class="form-control">
                    <label class="label pl-1" for="message-input">
                        <span
                            class="label-text text-gray-300 font-medium text-base"
                            >Message</span
                        >
                    </label>
                    <textarea
                        name={ENTRY_MESSAGE}
                        class="textarea textarea-lg bg-white/5 border-white/10 text-white placeholder-gray-500 focus:bg-white/10 focus:border-cyan-500 focus:outline-none transition-all min-h-40 leading-relaxed rounded-xl resize-none"
                        placeholder="Tell me about your project..."
                        required
                    ></textarea>
                </div>

                <button
                    type="submit"
                    class="btn bg-cyan-500 hover:bg-cyan-400 text-black border-none btn-lg w-full mt-4 shadow-[0_0_25px_rgba(34,211,238,0.3)] rounded-xl font-bold text-lg group"
                    disabled={isSubmitting}
                >
                    {#if isSubmitting}
                        <span class="loading loading-spinner"></span> Sending...
                    {:else}
                        Send Message
                        <svg
                            xmlns="http://www.w3.org/2000/svg"
                            class="h-6 w-6 ml-2 transition-transform group-hover:translate-x-1 group-hover:-translate-y-1"
                            fill="none"
                            viewBox="0 0 24 24"
                            stroke="currentColor"
                            ><path
                                stroke-linecap="round"
                                stroke-linejoin="round"
                                stroke-width="2"
                                d="M12 19l9 2-9-18-9 18 9-2zm0 0v-8"
                            /></svg
                        >
                    {/if}
                </button>
            </form>
        </div>
    </main>

    <Footer />
</div>

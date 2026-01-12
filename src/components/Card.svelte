<script>
    import { fade } from "svelte/transition";

    let activeSection = $state(null);
    let boxExpanded = $state(false);

    const sections = {
        "About Me":
            "This is where your about me content will go. Tell visitors about yourself, your background, and what you do.",
        Projects:
            "Your projects will be listed here. Showcase your best work and achievements.",
        Contact: "Contact information and form will appear here.",
        Resume: "Your resume and experience details will be displayed here.",
    };

    function openSection(section) {
        activeSection = section;
        boxExpanded = true;
    }

    function closeSection() {
        activeSection = null;
        // Delay box shrink until content fades out
        setTimeout(() => {
            if (!activeSection) boxExpanded = false;
        }, 200);
    }
</script>

<div
    class="bg-transparent border-2 border-accent rounded-3xl p-8 transition-all duration-500 ease-out overflow-hidden relative"
    style={boxExpanded
        ? "width: 600px; height: 500px;"
        : "width: 400px; height: 400px;"}
>
    {#if activeSection}
        <!-- Expanded View -->
        <div
            in:fade={{ duration: 200, delay: 200 }}
            out:fade={{ duration: 200 }}
            class="absolute inset-0 p-8 flex flex-col gap-6"
        >
            <div class="flex items-center gap-3">
                <button
                    onclick={closeSection}
                    class="text-white/50 hover:text-accent transition-colors"
                    aria-label="Back"
                >
                    <svg
                        xmlns="http://www.w3.org/2000/svg"
                        width="24"
                        height="24"
                        viewBox="0 0 24 24"
                        fill="none"
                        stroke="currentColor"
                        stroke-width="2"
                        stroke-linecap="round"
                        stroke-linejoin="round"
                    >
                        <path d="M19 12H5M12 19l-7-7 7-7" />
                    </svg>
                </button>
                <span class="text-white/90 text-2xl font-semibold"
                    >{activeSection}</span
                >
            </div>

            <div class="text-white/70 text-base leading-relaxed flex-1">
                {sections[activeSection]}
            </div>
        </div>
    {:else}
        <!-- Default View -->
        <div
            in:fade={{ duration: 200, delay: 200 }}
            out:fade={{ duration: 200 }}
            class="absolute inset-0 p-8 flex flex-col gap-6"
        >
            <div class="flex items-center gap-4">
                <img
                    src="/src/assets/perfil.jpg"
                    alt="Nuno Moreira"
                    class="w-14 h-14 rounded-full object-cover"
                />
                <span class="text-white/90 text-xl font-medium tracking-tight"
                    >Nuno Moreira</span
                >
            </div>

            <div class="flex flex-col gap-1">
                {#each Object.keys(sections) as section}
                    <button
                        onclick={() => openSection(section)}
                        class="w-full py-2.5 px-3 text-left text-white/70 rounded-lg font-medium bg-transparent hover:text-white hover:underline hover:decoration-accent hover:decoration-2 transition-all duration-200"
                    >
                        {section}
                    </button>
                {/each}
            </div>

            <div class="flex justify-center gap-4 pt-2">
                <a
                    href="#"
                    class="text-white/50 hover:text-accent transition-colors"
                    aria-label="LinkedIn"
                >
                    <svg
                        xmlns="http://www.w3.org/2000/svg"
                        width="20"
                        height="20"
                        viewBox="0 0 24 24"
                        fill="currentColor"
                        ><path
                            d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433c-1.144 0-2.063-.926-2.063-2.065 0-1.138.92-2.063 2.063-2.063 1.14 0 2.064.925 2.064 2.063 0 1.139-.925 2.065-2.064 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"
                        /></svg
                    >
                </a>
                <a
                    href="#"
                    class="text-white/50 hover:text-accent transition-colors"
                    aria-label="GitHub"
                >
                    <svg
                        xmlns="http://www.w3.org/2000/svg"
                        width="20"
                        height="20"
                        viewBox="0 0 24 24"
                        fill="currentColor"
                        ><path
                            d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"
                        /></svg
                    >
                </a>
                <a
                    href="#"
                    class="text-white/50 hover:text-accent transition-colors"
                    aria-label="Facebook"
                >
                    <svg
                        xmlns="http://www.w3.org/2000/svg"
                        width="20"
                        height="20"
                        viewBox="0 0 24 24"
                        fill="currentColor"
                        ><path
                            d="M24 12.073c0-6.627-5.373-12-12-12s-12 5.373-12 12c0 5.99 4.388 10.954 10.125 11.854v-8.385H7.078v-3.47h3.047V9.43c0-3.007 1.792-4.669 4.533-4.669 1.312 0 2.686.235 2.686.235v2.953H15.83c-1.491 0-1.956.925-1.956 1.874v2.25h3.328l-.532 3.47h-2.796v8.385C19.612 23.027 24 18.062 24 12.073z"
                        /></svg
                    >
                </a>
                <a
                    href="mailto:#"
                    class="text-white/50 hover:text-accent transition-colors"
                    aria-label="Email"
                >
                    <svg
                        xmlns="http://www.w3.org/2000/svg"
                        width="20"
                        height="20"
                        viewBox="0 0 24 24"
                        fill="currentColor"
                        ><path
                            d="M0 3v18h24v-18h-24zm21.518 2l-9.518 7.713-9.518-7.713h19.036zm-19.518 14v-11.817l10 8.104 10-8.104v11.817h-20z"
                        /></svg
                    >
                </a>
            </div>
        </div>
    {/if}
</div>

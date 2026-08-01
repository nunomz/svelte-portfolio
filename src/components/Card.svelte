<script>
    import { fade } from "svelte/transition";
    import perfil from "../assets/perfil.jpg";

    let activeSection = $state(null);
    let boxExpanded = $state(false);

    const sections = ["About Me", "Projects", "Resume"];

    const about = {
        paragraphs: [
            "24 years old, from Portugal. I've had a passion for technology for as long as I can remember. My family and friends always call me to fix their tech problems and, to be honest, I enjoy it...",
            "I started using Linux in high school and I've daily driven it in some way since then. I started with Ubuntu like everyone else, traveled through Pop!_OS, Fedora and Arch, and am currently on CachyOS.",
            "My first tech job was as a systems administrator, where I gained real hands-on experience with deploying and maintaining real production systems — both software and physical. I also got to run Fedora KDE on my work laptop, which was great.",
            "I'm currently working as a QA Engineer, which enables me to learn every day about how to build great products that people enjoy. And I get to do it at a global market-leading company.",
        ],
    };

    const resume = [
        {
            title: "Professional Experience",
            items: [
                {
                    role: "QA Engineer @ Veeam Software",
                    org: "Remote / Lisbon, PT",
                    dates: "Oct 2024 - Now",
                    bullets: [
                        "Development and maintenance of automated testing suites, internal tools and AI tools",
                        "Manual and automated product testing",
                        "Specialized customer support",
                    ],
                    tech: "Veeam, Linux, Manual testing, Automated testing",
                },
                {
                    role: "Systems Administrator @ DigitalSign",
                    org: "Guimarães, PT",
                    dates: "Jan 2023 - Sept 2024",
                    bullets: [
                        "Physical and virtual infrastructure management and monitoring",
                        "Tech helpdesk and support",
                        "Firewall maintenance and configuration",
                        "Implemented various internal tools based on open source software, such as a new company-wide knowledge base using Wiki.JS and PostgreSQL, a new password manager and a new Git platform using GitLab running on Docker",
                    ],
                    tech: "Linux, Docker, Zabbix, Ansible, Kubernetes",
                },
                {
                    role: "Video Editor @ soundscout.pt",
                    org: "Remote",
                    dates: "May 2022 - May 2024",
                    bullets: [
                        "Freelance video editing for a renowned music magazine in Portugal. This was more of a passion project I worked on while attending university.",
                    ],
                },
            ],
        },
                {
            title: "Education",
            items: [
                {
                    role: "Degree in Engineering and Management of Information Systems",
                    org: "University of Minho",
                    dates: "2019 - 2022",
                    bullets: [
                        "Learned subjects such as Data Engineering, Web Development, Distributed Systems, Artificial Intelligence",
                        "Acted as project manager and team leader for multiple projects including one involving a consulting simulation, achieving the highest grade in the course",
                    ],
                },
            ],
        },
    ];

    const projects = [
        // {
        //     name: "Web Design",
        //     description: '"IT Applications Development" University Project',
        // },
        // {
        //     name: "Data Engineering",
        //     description: "Development of Full Data Pipeline",
        // },
        // {
        //     name: "Web Design",
        //     description: '"Web Programming" University Project',
        // },
        // {
        //     name: "Predictive Data Analysis about Cinema",
        //     description: "Development of Classification Model",
        // },
        {
            name: "Kyanos",
            description: "Coming soon",
            href: "https://kyanos.eu/",
        },
        {
            name: "nubuilds",
            description: "My own store where I sell computers I build or repair",
            href: "https://builds.nuno.gg/",
        },
        {
            name: "YASIM",
            description: 'Yet Another Smart Inventory Manager',
        },
        {
            name: "Video Project for Sound Magazine",
            description: '"Capitão Fausto" Video Interview',
            href: "https://www.youtube.com/watch?v=b8E2-X0ZalU",
        },
        {
            name: "Video Project for Sound Magazine",
            description: '"Ganso" Video Interview',
            href: "https://www.youtube.com/watch?v=wJBeNs66P-8",
        },
    ];

    const email = "nunomoreirac@gmail.com";

    const socials = [
        { label: "LinkedIn", href: "https://www.linkedin.com/in/nuno-moreira-95b52818a/" },
        { label: "GitHub", href: "https://github.com/nunomz" },
        { label: "Email", href: `mailto:${email}` },
    ];

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

            <div
                class="text-white/70 text-base leading-relaxed flex-1 overflow-y-auto pr-3"
            >
                {#if activeSection === "About Me"}
                    {#each about.paragraphs as paragraph}
                        <p class="text-sm first:mt-0 mt-4">{paragraph}</p>
                    {/each}
                {:else if activeSection === "Projects"}
                    <ul class="flex flex-col gap-4">
                        {#each projects as project}
                            <li class="border-l-2 border-accent/40 pl-4">
                                <h3 class="text-white/90 font-medium">
                                    {#if project.href}
                                        <a
                                            href={project.href}
                                            target="_blank"
                                            rel="noopener noreferrer"
                                            class="inline-flex items-center gap-1.5 hover:text-accent hover:underline hover:decoration-accent transition-colors"
                                        >
                                            {project.name}
                                            <svg
                                                xmlns="http://www.w3.org/2000/svg"
                                                width="14"
                                                height="14"
                                                viewBox="0 0 24 24"
                                                fill="none"
                                                stroke="currentColor"
                                                stroke-width="2"
                                                stroke-linecap="round"
                                                stroke-linejoin="round"
                                                aria-hidden="true"
                                            >
                                                <path
                                                    d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6"
                                                />
                                                <polyline
                                                    points="15 3 21 3 21 9"
                                                />
                                                <line
                                                    x1="10"
                                                    y1="14"
                                                    x2="21"
                                                    y2="3"
                                                />
                                            </svg>
                                        </a>
                                    {:else}
                                        {project.name}
                                    {/if}
                                </h3>
                                <p class="text-sm text-white/60">
                                    {project.description}
                                </p>
                            </li>
                        {/each}
                    </ul>
                {:else if activeSection === "Resume"}
                    <div class="flex flex-col gap-6">
                        {#each resume as group}
                            <section>
                                <h3
                                    class="text-white/90 font-semibold uppercase text-xs tracking-widest"
                                >
                                    {group.title}
                                </h3>
                                <div class="flex flex-col gap-4 mt-3">
                                    {#each group.items as item}
                                        <div
                                            class="border-l-2 border-accent/40 pl-4"
                                        >
                                            <h4
                                                class="text-white/90 text-sm font-medium"
                                            >
                                                {item.role}
                                            </h4>
                                            <p class="text-xs text-white/50">
                                                {item.org} · {item.dates}
                                            </p>
                                            <ul
                                                class="mt-2 flex flex-col gap-1 text-sm text-white/60 list-disc list-outside ml-4"
                                            >
                                                {#each item.bullets as bullet}
                                                    <li>{bullet}</li>
                                                {/each}
                                            </ul>
                                            {#if item.tech}
                                                <p
                                                    class="mt-2 text-xs text-white/50"
                                                >
                                                    <span
                                                        class="text-white/70 font-medium"
                                                        >Technologies:</span
                                                    >
                                                    {item.tech}
                                                </p>
                                            {/if}
                                        </div>
                                    {/each}
                                </div>
                            </section>
                        {/each}
                    </div>
                {/if}
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
                    src={perfil.src}
                    alt="Nuno Moreira"
                    class="w-14 h-14 rounded-full object-cover"
                />
                <div class="flex flex-col">
                    <span class="text-white/90 text-xl font-medium tracking-tight"
                        >Nuno Moreira</span
                    >
                    <span class="text-white/50 text-sm"
                        >Guimarães, Portugal</span
                    >
                </div>
            </div>

            <div class="flex flex-col gap-1">
                {#each sections as section}
                    <button
                        onclick={() => openSection(section)}
                        class="w-full py-2.5 px-3 text-left text-white/70 rounded-lg font-medium bg-transparent hover:text-white hover:underline hover:decoration-accent hover:decoration-2 transition-all duration-200"
                    >
                        {section}
                    </button>
                {/each}
            </div>

            <div class="flex justify-center gap-4 pt-2">
                {#each socials as social}
                    <a
                        href={social.href}
                        target={social.label === "Email" ? null : "_blank"}
                        rel={social.label === "Email" ? null : "noopener noreferrer"}
                        class="text-white/50 hover:text-accent transition-colors"
                        aria-label={social.label}
                    >
                        {#if social.label === "LinkedIn"}
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
                        {:else if social.label === "GitHub"}
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
                        {:else}
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
                        {/if}
                    </a>
                {/each}
            </div>
        </div>
    {/if}
</div>

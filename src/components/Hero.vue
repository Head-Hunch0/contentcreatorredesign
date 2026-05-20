<template>
    <div class="bg-gray-900">


        <header class="pt-8 inset-x-0 top-0 z-50 sticky hidden">
            <div class="max-w-7xl mx-auto px-4 xl:px-0">
                <div
                    class="bg-white flex items-center justify-between gap-x-4 rounded-2xl py-2.5 pl-5 pr-2.5 shadow-[0_2px_10px_0px_rgba(0,0,0,0.15)] lg:grid lg:grid-cols-[1fr_auto_1fr] lg:justify-stretch lg:gap-x-12 lg:rounded-[1.375rem]">
                    <div class="flex items-center gap-x-10">
                        <a href="/" title="Home">
                            <img class="h-8" src="https://tailkits.com/ui/iframe/assets/img/logo.svg" alt="Logo" />
                        </a>
                        <span class="hidden h-4 w-[1px] bg-neutral-300 lg:block"></span>
                    </div>
                    <nav class="hidden lg:block">
                        <ul class="flex items-center">
                            <li>
                                <a class="px-3 py-2 text-sm font-medium text-neutral-700 transition hover:text-neutral-600"
                                    href="#">
                                    Features
                                </a>
                            </li>
                            <li>
                                <a class="px-3 py-2 text-sm font-medium text-neutral-700 transition hover:text-neutral-600"
                                    href="#">
                                    About
                                </a>
                            </li>

                            <li>
                                <a class="flex items-center gap-x-1.5 px-3 py-2 text-sm font-medium text-neutral-700 transition hover:text-neutral-600"
                                    href="#">
                                    Contact
                                    <svg class="h-4 text-neutral-500" xmlns="http://www.w3.org/2000/svg"
                                        viewBox="0 0 24 24" fill="currentColor" aria-hidden="true" data-slot="icon">
                                        <path fill-rule="evenodd"
                                            d="M8.25 3.75H19.5a.75.75 0 0 1 .75.75v11.25a.75.75 0 0 1-1.5 0V6.31L5.03 20.03a.75.75 0 0 1-1.06-1.06L17.69 5.25H8.25a.75.75 0 0 1 0-1.5Z"
                                            clip-rule="evenodd" />
                                    </svg>
                                </a>
                            </li>
                            <li>
                                <a class="px-3 py-2 text-sm font-medium text-neutral-700 transition hover:text-neutral-600"
                                    href="#">
                                    Blog
                                </a>
                            </li>
                            <li>
                                <a class="px-3 py-2 text-sm font-medium text-neutral-700 transition hover:text-neutral-600"
                                    href="#">
                                    Services
                                </a>
                            </li>
                            <li>
                                <a class="px-3 py-2 text-sm font-medium text-neutral-700 transition hover:text-neutral-600"
                                    href="#">
                                    Pricing
                                </a>
                            </li>
                        </ul>
                    </nav>
                    <div class="flex items-center gap-x-10 justify-self-end">
                        <span class="hidden h-4 w-[1px] bg-neutral-300 lg:block"></span>
                        <div class="flex items-center gap-x-3 lg:gap-x-3 lg:mr-5">
                            <a href="#" title="Log in"
                                class="items-center justify-center whitespace-nowrap text-sm font-medium transition-all focus:shadow-[0_0px_0px_2px_rgba(15,23,42,0.25),0_2px_10px_0px_rgba(0,0,0,0.05)] shadow-[0_2px_10px_0px_rgba(0,0,0,0.05)] border border-neutral-100 bg-white text-neutral-700 hover:border-neutral-200 hover:bg-neutral-100 disabled:border-slate-900/5 disabled:bg-slate-50/30 disabled:text-slate-900/20 px-3 py-2 rounded-[0.625rem] hidden lg:flex">
                                Log in
                            </a>
                            <a href="#" title="Try free"
                                class="items-center justify-center whitespace-nowrap text-sm font-medium transition-all focus:shadow-[0_0px_0px_2px_rgba(15,23,42,0.25),0_2px_10px_0px_rgba(0,0,0,0.05)] shadow-[0_2px_10px_0px_rgba(0,0,0,0.05)] bg-slate-900 text-white hover:bg-slate-800 disabled:bg-slate-900/30 disabled:text-slate-50/70 px-3 py-2 rounded-[0.625rem] flex">
                                Try free
                                <span class="ml-1 text-slate-400"> - 14 days</span>
                            </a>
                            <button type="button" aria-label="Open menu" class="lg:hidden" title="Open menu">
                                <svg class="h-6 text-slate-500" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"
                                    fill="currentColor" aria-hidden="true" data-slot="icon">
                                    <path fill-rule="evenodd"
                                        d="M3 9a.75.75 0 0 1 .75-.75h16.5a.75.75 0 0 1 0 1.5H3.75A.75.75 0 0 1 3 9Zm0 6.75a.75.75 0 0 1 .75-.75h16.5a.75.75 0 0 1 0 1.5H3.75a.75.75 0 0 1-.75-.75Z"
                                        clip-rule="evenodd" />
                                </svg>
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </header>
        <div class="relative isolate px-6 hidden lg:px-8">
            

            <div class="absolute inset-x-0 -top-40 -z-10 transform-gpu overflow-hidden blur-3xl sm:-top-80"
                aria-hidden="true">
                <div
                    class="relative left-[calc(50%-11rem)] aspect-square w-96 -translate-x-1/2 rounded-full bg-gradient-to-r from-blue-500 to-cyan-400 opacity-30 sm:w-[600px]">
                </div>
            </div>
            <div class="mx-auto max-w-2xl py-32 sm:py-48 lg:py-48">
                <div class="hidden sm:mb-8 sm:flex sm:justify-center">
                    <div
                        class="relative rounded-full px-4 py-2 text-2xl text-gray-400 ring-1 ring-white/50 animate-pulse shadow-[0_0_20px_rgba(255,255,255,0.5)]">
                        Introducing.
                    </div>

                    
                </div>
                <div class="text-center">
                    <h1 class="text-5xl font-semibold tracking-tight text-balance text-white sm:text-7xl">Prompt Edit</h1>
                    <p class="mt-8 text-lg font-medium text-pretty text-gray-400 sm:text-xl/8">The most affordable AI
                        marketplace featuring the best AI tools. Each one accessible WITHOUT the need for a
                        subscription. Just pay as you go.</p>
                    <div class="py-5 flex items-center justify-center gap-x-6 ">
                        <p class="text-sm font-semibold text-white">Learn more </p>
                    </div>
                </div>
            </div>
            <div class="absolute inset-x-0 top-[calc(100%-13rem)] -z-10 transform-gpu overflow-hidden blur-3xl sm:top-[calc(100%-30rem)]"
                aria-hidden="true">
                <div class="relative left-[calc(50%+3rem)] aspect-1155/678 w-144.5 -translate-x-1/2 bg-linear-to-tr from-[#ff80b5] to-[#9089fc] opacity-30 sm:left-[calc(50%+36rem)] sm:w-288.75"
                    style="clip-path: polygon(74.1% 44.1%, 100% 61.6%, 97.5% 26.9%, 85.5% 0.1%, 80.7% 2%, 72.5% 32.5%, 60.2% 62.4%, 52.4% 68.1%, 47.5% 58.3%, 45.2% 34.5%, 27.5% 76.7%, 0.1% 64.9%, 17.9% 100%, 27.6% 76.8%, 76.1% 97.7%, 74.1% 44.1%)">
                </div>
            </div>
            
        </div>

        <div class="relative isolate px-6 lg:px-8">
            
            <div class="absolute inset-x-0 -top-40 -z-10 transform-gpu overflow-hidden blur-3xl sm:-top-80"
                aria-hidden="true">
                <div
                    class="relative left-[calc(50%-11rem)] aspect-square w-96 -translate-x-1/2 rounded-full bg-gradient-to-r from-blue-500 to-cyan-400 opacity-30 sm:w-[600px]">
                </div>
            </div>
            <div class="absolute inset-x-0 top-[calc(100%-13rem)] -z-10 transform-gpu overflow-hidden blur-3xl sm:top-[calc(100%-30rem)]"
                aria-hidden="true">
                <div class="relative left-[calc(50%+3rem)] aspect-1155/678 w-144.5 -translate-x-1/2 bg-linear-to-tr from-[#ff80b5] to-[#9089fc] opacity-30 sm:left-[calc(50%+36rem)] sm:w-288.75"
                    style="clip-path: polygon(74.1% 44.1%, 100% 61.6%, 97.5% 26.9%, 85.5% 0.1%, 80.7% 2%, 72.5% 32.5%, 60.2% 62.4%, 52.4% 68.1%, 47.5% 58.3%, 45.2% 34.5%, 27.5% 76.7%, 0.1% 64.9%, 17.9% 100%, 27.6% 76.8%, 76.1% 97.7%, 74.1% 44.1%)">
                </div>
            </div>

            <!-- Hero Content Container -->
            <div class="mx-auto max-w-2xl py-32 sm:py-48 lg:py-48">
                <!-- Your existing hero text and badge -->
                <div class="hidden sm:mb-8 sm:flex sm:justify-center">
                    <div
                        class="relative rounded-full px-4 py-2 text-2xl text-gray-400 ring-1 ring-white/50 animate-pulse shadow-[0_0_20px_rgba(255,255,255,0.5)]">
                        Introducing.
                    </div>
                </div>

                <!-- Both images visible only on large screens and above -->
                <div class="hidden lg:block">
                    <!-- Right Image - 40% from top -->
                    <div class="absolute inset-0 -z-5 pointer-events-none overflow-hidden">
                        <div class="grid h-full grid-cols-1 items-end lg:grid-cols-2">
                            <div class="hidden lg:block"></div>
                            <div
                                class="relative flex h-full items-center justify-end opacity-30 md:opacity-40 lg:opacity-50 xl:opacity-60">
                                <div
                                    class="absolute right-0 top-[40%] max-w-md transform-gpu transition-all duration-1000 hover:scale-105 hover:opacity-80 mr-16 lg:mr-24 -translate-y-1/2">
                                    <img class="h-48 w-full rounded-3xl object-cover shadow-2xl"
                                        src="https://tailkits.com/ui/iframe/assets/img/bg-fade-6.png"
                                        alt="Abstract background art" />
                                </div>
                            </div>
                        </div>
                    </div>

                    <!-- Left Image - 40% from top -->
                    <div class="absolute inset-0 -z-5 pointer-events-none overflow-hidden">
                        <div class="grid h-full grid-cols-1 items-end lg:grid-cols-2">
                            <div
                                class="relative flex h-full items-center justify-start opacity-30 md:opacity-40 lg:opacity-50 xl:opacity-60">
                                <div
                                    class="absolute left-0 top-[40%] max-w-md transform-gpu transition-all duration-1000 hover:scale-105 hover:opacity-80 ml-16 lg:ml-24 -translate-y-1/2">
                                    <img class="h-48 w-full rounded-3xl object-cover shadow-2xl"
                                        src="https://tailkits.com/ui/iframe/assets/img/bg-fade-6.png"
                                        alt="Abstract background art left" />
                                </div>
                            </div>
                            <div class="hidden lg:block"></div>
                        </div>
                    </div>
                </div>
                

                <div class="text-center">
                    <h1 class="text-5xl font-semibold tracking-tight text-balance text-white sm:text-7xl">Prompt Edit
                    </h1>
                    <p class="mt-8 text-lg font-medium text-pretty text-gray-400 sm:text-xl/8">The most affordable AI
                        marketplace featuring the best AI tools. Each one accessible WITHOUT the need for a
                        subscription. Just pay as you go.</p>
                    <div class="py-6 flex items-center justify-center gap-x-6">
                        <p class="text-sm font-semibold text-white">Learn more</p>
                    </div>
                </div>
            </div>

            <!-- Both images visible only on large screens and above -->
            <div class="hidden lg:block">
                <!-- Right Image - Normal flow -->
                <div class="absolute inset-0 -z-5 pointer-events-none overflow-hidden">
                    <div class="grid h-full grid-cols-1 items-end lg:grid-cols-2">
                        <div class="hidden lg:block"></div>
                        <div
                            class="flex h-full items-center justify-end opacity-30 md:opacity-40 lg:opacity-50 xl:opacity-60">
                            <div
                                class="max-w-md transform-gpu transition-all duration-1000 hover:scale-105 hover:opacity-80">
                                <img class="h-48 w-full rounded-3xl object-cover shadow-2xl"
                                    src="https://tailkits.com/ui/iframe/assets/img/bg-fade-6.png"
                                    alt="Abstract background art" />
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Left Image - Normal flow -->
                <div class="absolute inset-0 -z-5 pointer-events-none overflow-hidden">
                    <div class="grid h-full grid-cols-1 items-end lg:grid-cols-2">
                        <div
                            class="flex h-full items-center justify-start opacity-30 md:opacity-40 lg:opacity-50 xl:opacity-60">
                            <div
                                class="max-w-md transform-gpu transition-all duration-1000 hover:scale-105 hover:opacity-80">
                                <img class="h-48 w-full rounded-3xl object-cover shadow-2xl"
                                    src="https://tailkits.com/ui/iframe/assets/img/bg-fade-6.png"
                                    alt="Abstract background art left" />
                            </div>
                        </div>
                        <div class="hidden lg:block"></div>
                    </div>
                </div>
            </div>

            
            <!-- END: Background Image Grid -->
        </div>
    </div>


    <section>
        <div class="absolute bottom-8 left-1/2 transform -translate-x-1/2 z-20 cursor-pointer group"
        :class="[
            'bottom-4',      // Mobile default (16px)
            'sm:bottom-6',   // 640px+ (24px)  
            'md:bottom-8',   // 768px+ (32px)
            'lg:bottom-10'   // 1024px+ (40px)
        ]"
            title="Scroll down">
            <div class="flex flex-col items-center gap-3">
                <!-- Mouse with moving wheel -->
                <div
                    class="relative w-7 h-11 border-2 border-white/50 rounded-full group-hover:border-white/80 transition-all duration-300">
                    <div
                        class="absolute left-1/2 transform -translate-x-1/2 top-1.5 w-1.5 h-2.5 bg-white/60 rounded-full animate-scroll-mouse">
                    </div>
                </div>

                <!-- Animated chevrons -->
                <div class="flex flex-col items-center gap-0.5">
                    <svg class="w-5 h-5 text-white/50 animate-chevron-1" fill="none" stroke="currentColor"
                        viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5"
                            d="M19 14l-7 7m0 0l-7-7m7 7V3" />
                    </svg>
                    <svg class="w-5 h-5 text-white/50 animate-chevron-2 -mt-2" fill="none" stroke="currentColor"
                        viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5"
                            d="M19 14l-7 7m0 0l-7-7m7 7V3" />
                    </svg>
                    <svg class="w-5 h-5 text-white/50 animate-chevron-3 -mt-2" fill="none" stroke="currentColor"
                        viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5"
                            d="M19 14l-7 7m0 0l-7-7m7 7V3" />
                    </svg>
                </div>
            </div>
        </div>
    </section>
    
</template>

<script setup lang="ts">

</script>

<style scoped>
@keyframes scroll-mouse {

    0%,
    100% {
        opacity: 1;
        transform: translateX(-50%) translateY(0);
    }

    50% {
        opacity: 0;
        transform: translateX(-50%) translateY(6px);
    }
}

@keyframes chevron-1 {

    0%,
    100% {
        opacity: 0.2;
        transform: translateY(0);
    }

    50% {
        opacity: 0.8;
        transform: translateY(4px);
    }
}

@keyframes chevron-2 {

    0%,
    100% {
        opacity: 0.1;
        transform: translateY(0);
    }

    50% {
        opacity: 0.6;
        transform: translateY(4px);
    }
}

@keyframes chevron-3 {

    0%,
    100% {
        opacity: 0;
        transform: translateY(0);
    }

    50% {
        opacity: 0.4;
        transform: translateY(4px);
    }
}

.animate-scroll-mouse {
    animation: scroll-mouse 2s ease-in-out infinite;
}

.animate-chevron-1 {
    animation: chevron-1 2s ease-in-out infinite;
}

.animate-chevron-2 {
    animation: chevron-2 2s ease-in-out infinite 0.3s;
}

.animate-chevron-3 {
    animation: chevron-3 2s ease-in-out infinite 0.6s;
}
</style>
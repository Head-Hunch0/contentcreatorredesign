<template>
    <section class="pt-12 lg:pt-16 relative pb-12 lg:pb-16">
        <img class="absolute left-0 top-0 -z-20 h-full w-full object-cover" :src="backgroundImage"
            alt="Background image" />
        <div class="max-w-7xl mx-auto px-4 xl:px-0">
            <div
                class="flex flex-col items-start sm:items-center sm:text-center md:px-4 lg:items-start lg:px-8 lg:text-left">
                <div
                    class="items-center justify-center rounded-full text-sm font-medium whitespace-nowrap shadow-[0_2px_10px_0px_rgba(0,0,0,0.15)] inline-flex bg-white text-neutral-700 px-2.5 py-1">
                    {{ sectionHeader.badge }}
                </div>
                <div
                    class="mt-8 bg-gradient-to-b from-slate-800 to-slate-600 bg-clip-text text-xl font-semibold text-transparent md:text-2xl lg:mt-9 lg:w-5/6 lg:leading-tight xl:w-3/4 xl:text-3xl">
                    {{ sectionHeader.title }}
                </div>
                <p class="mt-4 text-sm font-medium text-slate-600 sm:w-1/2 lg:w-2/5">
                    {{ sectionHeader.description }}
                </p>
            </div>
            <div class="mt-4 border-b border-b-neutral-100 lg:mt-6"></div>

            <!-- Desktop Grid View (3 columns) -->
            <div
                class="relative mt-6 hidden sm:mx-auto sm:w-2/3 md:w-1/2 md:px-4 lg:mt-9 lg:grid lg:w-full lg:grid-cols-3 lg:gap-x-6 lg:gap-y-0 lg:px-8">
                <article v-for="member in teamMembers" :key="member.id" class="flex flex-col">
                    <figure class="w-full rounded-2xl lg:rounded-3xl lg:shadow-[0_2px_10px_0px_rgba(0,0,0,0.05)]">
                        <img class="h-40 w-full rounded-2xl object-cover lg:h-64 lg:rounded-3xl" :src="member.image"
                            :alt="member.name" />
                    </figure>
                    <div class="flex flex-col items-start p-3 lg:p-4">
                        <div class="font-semibold text-neutral-700 md:text-lg lg:text-xl">
                            {{ member.name }}
                        </div>
                        <p class="mt-0.5 text-sm font-medium text-neutral-500 lg:mt-1 lg:text-base">
                            {{ member.role }}
                        </p>
                    </div>
                </article>
            </div>

            <!-- Mobile Carousel View -->
            <div class="relative mt-6 lg:hidden">
                <button type="button" aria-label="Previous team member"
                    class="rounded-full cursor-pointer flex items-center justify-center whitespace-nowrap transition-all focus:shadow-[0_0px_0px_2px_rgba(15,23,42,0.25),0_2px_10px_0px_rgba(0,0,0,0.05)] shadow-[0_2px_10px_0px_rgba(0,0,0,0.05)] bg-slate-900 text-white hover:bg-slate-800 disabled:bg-slate-900/30 disabled:text-slate-50/70 w-8 h-8 p-1.5 md:w-10 md:h-10 md:p-2.5 absolute left-0 top-1/2 z-10 -translate-y-1/2"
                    @click="prevSlide" :disabled="currentSlide === 0">
                    <svg class="h-5 shrink-0 rotate-180" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"
                        fill="currentColor">
                        <path fill-rule="evenodd"
                            d="M16.28 11.47a.75.75 0 0 1 0 1.06l-7.5 7.5a.75.75 0 0 1-1.06-1.06L14.69 12 7.72 5.03a.75.75 0 0 1 1.06-1.06l7.5 7.5Z"
                            clip-rule="evenodd" />
                    </svg>
                </button>

                <div class="overflow-hidden px-8">
                    <transition-group name="fade" mode="out-in" class="flex justify-center">
                        <article :key="currentSlide" class="flex flex-col w-full">
                            <figure class="w-full rounded-2xl shadow-[0_2px_10px_0px_rgba(0,0,0,0.05)]">
                                <img class="h-64 w-full rounded-2xl object-cover" :src="currentMember.image"
                                    :alt="currentMember.name" />
                            </figure>
                            <div class="flex flex-col items-start p-4">
                                <div class="font-semibold text-neutral-700 text-xl">
                                    {{ currentMember.name }}
                                </div>
                                <p class="mt-1 text-sm font-medium text-neutral-500">
                                    {{ currentMember.role }}
                                </p>
                            </div>
                        </article>
                    </transition-group>
                </div>

                <button type="button" aria-label="Next team member"
                    class="rounded-full cursor-pointer flex items-center justify-center whitespace-nowrap transition-all focus:shadow-[0_0px_0px_2px_rgba(15,23,42,0.25),0_2px_10px_0px_rgba(0,0,0,0.05)] shadow-[0_2px_10px_0px_rgba(0,0,0,0.05)] bg-slate-900 text-white hover:bg-slate-800 disabled:bg-slate-900/30 disabled:text-slate-50/70 w-8 h-8 p-1.5 md:w-10 md:h-10 md:p-2.5 absolute right-0 top-1/2 z-10 -translate-y-1/2"
                    @click="nextSlide" :disabled="currentSlide === teamMembers.length - 1">
                    <svg class="h-5 shrink-0" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"
                        fill="currentColor">
                        <path fill-rule="evenodd"
                            d="M16.28 11.47a.75.75 0 0 1 0 1.06l-7.5 7.5a.75.75 0 0 1-1.06-1.06L14.69 12 7.72 5.03a.75.75 0 0 1 1.06-1.06l7.5 7.5Z"
                            clip-rule="evenodd" />
                    </svg>
                </button>

                <!-- Carousel Indicators -->
                <div class="flex justify-center gap-2 mt-6">
                    <button v-for="(_, index) in teamMembers" :key="index" @click="currentSlide = index" :class="[
                        'w-2 h-2 rounded-full transition-all duration-300',
                        currentSlide === index
                            ? 'bg-slate-900 w-6'
                            : 'bg-neutral-300 hover:bg-neutral-400'
                    ]" :aria-label="`Go to slide ${index + 1}`" />
                </div>
            </div>
        </div>
    </section>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'

// Type definitions
interface TeamMember {
    id: number
    name: string
    role: string
    image: string
}

interface SectionHeader {
    badge: string
    title: string
    description: string
}

// Background image constant (not a prop since it's hardcoded)
const backgroundImage = 'https://tailkits.com/ui/iframe/assets/img/bg-overlay-3.png'

// Section header data
const sectionHeader = ref<SectionHeader>({
    badge: 'Amazing team',
    title: 'What Our Clients Have to Say',
    description: "Don't just take our word for it. Here's what our clients have to say."
})

// Team members data
const teamMembers = ref<TeamMember[]>([
    {
        id: 1,
        name: 'John Anderson',
        role: 'Thank you so much for the Content Creator Templates Library! My daughter and I got more editing work done today in 3 hours than we normally do in 3 days!',
        image: 'https://tailkits.com/ui/iframe/assets/img/profile.png'
    },
    {
        id: 2,
        name: 'Emily Thompson',
        role: "My videos wouldn't look HALF as good as they do if it wasn't for the Content Creator Templates Library. I lean into them heavily for every edit I do.",
        image: 'https://tailkits.com/ui/iframe/assets/img/profile-2.png'
    },
    {
        id: 3,
        name: 'Sarah Roberts',
        role: 'The Content Creator Templates Library is a fantastic resource! I don’t need any other digital asset subscriptions.',
        image: 'https://tailkits.com/ui/iframe/assets/img/profile-3.png'
    }
])

// Carousel state
const currentSlide = ref<number>(0)

// Computed property for current member in carousel
const currentMember = computed(() => teamMembers.value[currentSlide.value])

// Methods
const nextSlide = () => {
    if (currentSlide.value < teamMembers.value.length - 1) {
        currentSlide.value++
    }
}

const prevSlide = () => {
    if (currentSlide.value > 0) {
        currentSlide.value--
    }
}
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
    transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
    opacity: 0;
}
</style>
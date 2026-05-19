<template>
    <section class="pt-12 lg:pt-16 relative pb-12 mb-10 lg:pb-2 overflow-hidden">
        <img class="absolute left-0 top-0 -z-20 h-full w-full object-cover mb-10"
            src="https://tailkits.com/ui/iframe/assets/img/bg-overlay-3.png" alt="Background image" />
        <div class="max-w-7xl mx-auto px-4 xl:px-0 flex flex-col">
            <div
                class="flex flex-col items-start sm:items-center sm:text-center md:px-4 lg:items-start lg:px-8 lg:text-left">
                <div
                    class="bg-gradient-to-b from-slate-800 to-slate-600 bg-clip-text text-3xl font-semibold text-transparent lg:text-5xl mt-6 lg:mt-8 lg:w-5/6 lg:leading-tight xl:w-3/4">
                    {{ assetsHeader.title }}
                </div>
                <p class="mt-4 text-sm font-medium text-slate-600 sm:w-1/2 lg:w-2/5">
                    {{ assetsHeader.description }}
                </p>
            </div>
            <div class="mt-6 border-b border-b-neutral-100"></div>
            <div class="mt-6 flex flex-col gap-y-6 sm:px-4 lg:mt-9 lg:flex-row lg:gap-x-9 lg:gap-y-0 lg:px-8 mb-10">
                <!-- Left Side - Clickable Items -->
                <div
                    class="flex flex-col gap-y-4 sm:mx-auto sm:w-7/12 md:w-1/2 lg:mx-0 lg:mb-20 lg:w-2/5 lg:gap-y-6 xl:w-1/3">
                    <article v-for="asset in assets" :key="asset.id" @click="activeAssetId = asset.id" :class="[
                        'flex flex-col items-start cursor-pointer transition-all duration-300 rounded-xl p-2',
                        activeAssetId === asset.id ? 'bg-white/10 scale-[1.02]' : 'opacity-50 hover:opacity-100'
                    ]">
                        <figure>
                            <svg class="h-6 text-slate-400 lg:h-8" xmlns="http://www.w3.org/2000/svg"
                                viewBox="0 0 24 24" fill="currentColor">
                                <path fill-rule="evenodd"
                                    d="M12 2.25c-5.385 0-9.75 4.365-9.75 9.75s4.365 9.75 9.75 9.75 9.75-4.365 9.75-9.75S17.385 2.25 12 2.25Zm-2.625 6c-.54 0-.828.419-.936.634a1.96 1.96 0 0 0-.189.866c0 .298.059.605.189.866.108.215.395.634.936.634.54 0 .828-.419.936-.634.13-.26.189-.568.189-.866 0-.298-.059-.605-.189-.866-.108-.215-.395-.634-.936-.634Zm4.314.634c.108-.215.395-.634.936-.634.54 0 .828.419.936.634.13.26.189.568.189.866 0 .298-.059.605-.189.866-.108.215-.395.634-.936.634-.54 0-.828-.419-.936-.634a1.96 1.96 0 0 1-.189-.866c0-.298.059-.605.189-.866Zm2.023 6.828a.75.75 0 1 0-1.06-1.06 3.75 3.75 0 0 1-5.304 0 .75.75 0 0 0-1.06 1.06 5.25 5.25 0 0 0 7.424 0Z"
                                    clip-rule="evenodd" />
                            </svg>
                        </figure>
                        <div class="mt-3 font-bold text-neutral-700 md:text-lg lg:mt-4 xl:text-xl">
                            {{ asset.title }}
                        </div>
                        <p class="mt-2 text-sm font-medium text-neutral-500">
                            {{ asset.description }}
                        </p>
                    </article>
                </div>

                <!-- Right Side - Image Container -->
                <div class="hidden lg:flex grow ml-8 lg:ml-12">
                    <figure
                        class="relative w-full overflow-hidden rounded-xl sm:mx-auto sm:w-2/3 md:h-60 md:rounded-2xl lg:h-full lg:w-full lg:rounded-3xl">
                        <transition name="fade" mode="out-in">
                            <img :key="activeAssetId"
                                class="relative w-full h-auto rounded-md border-4 border-slate-900/5 object-cover shadow-[0_2px_10px_0px_rgba(0,0,0,0.15)] lg:rounded-2xl"
                                :src="currentAssetImage" :alt="currentAssetTitle" />
                        </transition>
                    </figure>
                </div>
            </div>
        </div>
    </section>

    <section class="pt-12 lg:pt-2 pb-12 lg:pb-16 relative">
        <div class="max-w-7xl mx-auto px-4 xl:px-0 flex flex-col p-6">
            <div class="absolute right-0 top-1/7 -translate-y-1/2 -z-100 transform-gpu overflow-hidden blur-3xl"
                aria-hidden="true">
                <div class="relative right-0 w-96 h-96 opacity-30 sm:w-[500px] sm:h-[500px] animate-pulse"
                    style="background: linear-gradient(135deg, #F59E0B, #F97316, #EF4444, #EC4899); clip-path: polygon(25% 0%, 75% 0%, 100% 25%, 100% 75%, 75% 100%, 25% 100%, 0% 75%, 0% 25%);">
                </div>
            </div>

            <div class="flex flex-col items-center">
                <div
                    class="mt-6 bg-gradient-to-b from-slate-800 to-slate-600 bg-clip-text text-center text-3xl font-semibold text-transparent sm:mx-auto sm:w-2/3 md:w-1/2 lg:mt-1 lg:pb-4 lg:text-4xl lg:leading-tight xl:w-2/3">
                    {{ toolsHeader.title }}
                </div>
                <p
                    class="text-sm font-medium text-slate-600 leading-normal lg:py-5 lg:leading-normal lg:text-base mt-4 text-center sm:mx-auto sm:w-2/3 md:w-1/2 xl:w-2/5">
                    {{ toolsHeader.description }}
                </p>

                <!-- Category Pills / Filter Buttons -->
                <div class="mt-6 flex flex-wrap items-center justify-center gap-3">
                    <button v-for="pill in categoryPills" :key="pill.id" @click="activePill = pill.id" :class="[
                        'py-2 px-5 text-sm flex items-center justify-center font-medium shadow-[0_2px_10px_0px_rgba(0,0,0,0.15)] rounded-full whitespace-nowrap transition-all duration-300',
                        activePill === pill.id
                            ? 'bg-slate-900 text-white'
                            : 'text-neutral-700 bg-white hover:bg-slate-100'
                    ]">
                        {{ pill.name }}
                    </button>
                </div>
            </div>

            <!-- Dynamic Grid Cards -->
            <div
                class="mt-6 grid gap-y-3 sm:mx-auto sm:w-2/3 md:w-1/2 md:px-4 lg:mx-0 lg:mt-12 lg:w-full lg:grid-cols-2 lg:gap-x-8 lg:gap-y-6 lg:px-8">
                <transition-group name="card-fade" mode="out-in">
                    <article v-for="card in filteredCards" :key="card.id"
                        class="grid gap-x-6 gap-y-2 lg:gap-y-0 xl:grid-cols-[15.625rem_auto]">
                        <figure
                            class="relative w-full self-start rounded-2xl shadow-[0_2px_10px_0px_rgba(0,0,0,0.05)] hidden lg:block">
                            <img class="h-28 w-full42 rounded-2xl object-cover object-left-top lg:h-48" :src="card.image"
                                :alt="card.title" />
                            <div
                                class="items-center justify-center rounded-full text-sm font-medium whitespace-nowrap shadow-[0_2px_10px_0px_rgba(0,0,0,0.15)] bg-white text-neutral-700 px-2.5 py-1 absolute right-3 top-3 z-10 xl:hidden">
                                {{ card.badge }}
                            </div>
                        </figure>

                        <div class="flex flex-col items-start p-4 xl:p-0">
                            <div
                                class="items-center justify-center rounded-full text-sm font-medium whitespace-nowrap shadow-[0_2px_10px_0px_rgba(0,0,0,0.15)] bg-white text-neutral-700 px-2.5 py-1 hidden xl:block">
                                {{ card.badge }}
                            </div>
                            <div class="xl:mt-2.5">
                                <a class="font-bold text-neutral-700 hover:text-slate-800 transition" href="#"
                                    :title="card.title">
                                    {{ card.title }}
                                </a>
                                <p class="mt-2 text-sm font-medium text-neutral-500">
                                    {{ card.description }}
                                </p>
                            </div>
                        </div>
                    </article>
                </transition-group>
            </div>
        </div>
    </section>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'


// Type definitions
interface Asset {
    id: number
    title: string
    description: string
    imageUrl: string
}

interface Header {
    title: string
    description: string
}

interface CategoryPill {
    id: string
    name: string
}

interface ToolCard {
    id: number
    category: string
    badge: string
    title: string
    description: string
    author?: string
    date?: string
    image: string
    useCase?: string
}

const getImageUrl = (path: string) => {
    return import.meta.env.BASE_URL + path.replace(/^\//, '')
}

// Assets Section Data
const assetsHeader = ref<Header>({
    title: 'Our Most Popular Assets',
    description: "Let's go through some of our most popular asset categories..."
})

const assets = ref<Asset[]>([
    {
        id: 1,
        title: 'LUTs for Color Grading',
        description: 'Our LUTs work flawlessly with any editing software, giving your videos that professional, cinematic look in seconds',
        imageUrl: getImageUrl('/luts.svg')
    },
    {
        id: 2,
        title: 'Text & Title Templates',
        description: 'With our professionally-designed text templates, you can create scroll-stopping, binge-worthy content in seconds.',
        imageUrl: getImageUrl('/templates.svg')
    },
    {
        id: 3,
        title: 'Overlays & Backgrounds',
        description: 'Overlays make it super easy! Just drag it onto your video, change the blend mode — your video has a whole new style.',
        imageUrl: getImageUrl('/overlays.svg')
    }
])

const activeAssetId = ref<number>(1)

const currentAssetImage = computed(() => {
    const asset = assets.value.find(a => a.id === activeAssetId.value)
    return asset?.imageUrl || assets.value[0].imageUrl
})

const currentAssetTitle = computed(() => {
    const asset = assets.value.find(a => a.id === activeAssetId.value)
    return asset?.title || ''
})

// Tools Section Data
const toolsHeader = ref<Header>({
    title: 'Exploring Trends, Innovations, Stories in The most affordable AI marketplace featuring the best AI tools.',
    description: "Let's break down exactly what you can access with Prompt Edit"
})

const categoryPills = ref<CategoryPill[]>([
    { id: 'image', name: '🖼️ Image Tools' },
    { id: 'audio', name: '🎵 Audio Tools' },
    { id: 'video', name: '🎬 Video Tools' }
])

const activePill = ref<string>('image')

const cardsData = ref<ToolCard[]>([
    // Image Tools
    {
        id: 1,
        category: 'image',
        badge: 'Social Media',
        title: 'Stop Scrolling: Create Social Media Posts That Convert',
        description: "Generate scroll-stopping Instagram posts, TikTok thumbnails, and Facebook ads in seconds. Our AI understands what makes content go viral and helps you replicate that magic every single time.",
        author: 'Sarah Thompson',
        date: '16 April 2023',
        image: getImageUrl('/social.svg'),
        useCase: 'Social Media Posts'
    },
    {
        id: 2,
        category: 'image',
        badge: 'Design',
        title: 'From Blank Canvas to Brand Identity in Minutes',
        description: "Whether you need logos, brochures, flyers, or complete brand kits — our AI tools help you create professional graphic design assets without hiring an expensive designer. Just describe what you need, and watch it come to life.",
        author: 'David Wilson',
        date: '15 April 2023',
        image: getImageUrl('/social.svg'),
        useCase: 'Graphic Design'
    },
    {
        id: 3,
        category: 'image',
        badge: 'YouTube',
        title: 'Double Your Click-Through Rate with AI Thumbnails',
        description: "YouTube creators are using our tools to design thumbnails that get clicks. Our AI analyzes what's working in your niche and generates attention-grabbing visuals that make viewers stop and click. More clicks = more views = more revenue.",
        author: 'Emily Roberts',
        date: '14 April 2023',
        image: getImageUrl('/social.svg'),
        useCase: 'YouTube Thumbnails'
    },
    {
        id: 4,
        category: 'image',
        badge: 'Ads',
        title: 'Turn Ad Spend into Revenue with High-Converting Creatives',
        description: "Stop wasting money on ads that don't convert. Generate multiple ad variations in seconds, test different visuals, and find what resonates with your audience — all without hiring a creative team. Facebook, Google, TikTok — we support them all.",
        author: 'Michael Anderson',
        date: '13 April 2023',
        image: getImageUrl('/social.svg'),
        useCase: 'Online Ads'
    },
    // Audio Tools
    {
        id: 5,
        category: 'audio',
        badge: 'Voiceovers',
        title: 'Professional Voiceovers in Minutes, Not Days — No Studio Required',
        description: "Stop waiting for voice talent or expensive studio time. Generate natural, emotion-filled voiceovers in dozens of languages and voices. Perfect for YouTube videos, commercials, e-learning, and explainer videos — all with a few clicks.",
        author: 'Jessica Lee',
        date: '12 April 2023',
        image: getImageUrl('/audio.svg'),
        useCase: 'AI Voiceovers'
    },
    {
        id: 6,
        category: 'audio',
        badge: 'Voice Clones',
        title: 'Clone Your Voice or Create Custom Characters — The Choice Is Yours',
        description: "Create a perfect digital replica of your own voice for consistent branding. Or generate entirely new character voices for animations, games, and storytelling. Your audience will never know it's AI.",
        author: 'Chris Evans',
        date: '11 April 2023',
        image: getImageUrl('/audio.svg'),
        useCase: 'AI Voice Clones'
    },
    {
        id: 7,
        category: 'audio',
        badge: 'Podcasts',
        title: 'Launch Your Podcast Faster with AI-Powered Audio Tools',
        description: "From automatic noise reduction to leveling and mastering — our AI handles post-production so you can focus on your message. Remove ums and ahs, add intro/outro music, and publish studio-quality episodes in record time.",
        author: 'Nina Martinez',
        date: '10 April 2023',
        image: getImageUrl('/audio.svg'),
        useCase: 'Podcasts'
    },
    {
        id: 8,
        category: 'audio',
        badge: 'Voice Swaps',
        title: 'Voice Swaps Made Easy: Change Voices Without Re-Recording',
        description: "Record once, swap voices instantly. Perfect for dubbing content, creating multilingual versions, or experimenting with different vocal styles. Save hours of re-recording time and reach global audiences effortlessly.",
        author: 'Alex Turner',
        date: '9 April 2023',
        image: getImageUrl('/audio.svg'),
        useCase: 'Voice Swaps'
    },
    // Video Tools
    {
        id: 9,
        category: 'video',
        badge: 'Films',
        title: 'From Script to Screen: Create Cinematic Films Without a Studio',
        description: "Turn your vision into reality. Generate storyboards, color grade like Hollywood pros, and add VFX that used to cost thousands — all with AI. Perfect for indie filmmakers and content creators who want that premium look.",
        author: 'Oliver Chen',
        date: '8 April 2023',
        image: getImageUrl('/video.svg'),
        useCase: 'Cinematic Films'
    },
    {
        id: 10,
        category: 'video',
        badge: 'Ads',
        title: 'Stop Scrolling: Video Ads That Convert Viewers Into Customers',
        description: "Generate multiple ad variations in seconds. Our AI analyzes what drives clicks and sales, then helps you create compelling video ads for Facebook, YouTube, TikTok, and Instagram — all without a production budget.",
        author: 'Sophia Rodriguez',
        date: '7 April 2023',
        image: getImageUrl('/video.svg'),
        useCase: 'Video Ads'
    },
    {
        id: 11,
        category: 'video',
        badge: 'Reels',
        title: 'Go Viral on Reels & TikTok with AI-Powered Short-Form Magic',
        description: "Short-form content is king. Our tools help you edit, add captions, apply trending effects, and optimize your vertical videos for maximum engagement. Join creators getting millions of views using our templates.",
        author: 'Liam Walker',
        date: '6 April 2023',
        image: getImageUrl('/video.svg'),
        useCase: 'Reels & TikToks'
    },
    {
        id: 12,
        category: 'video',
        badge: 'YouTube',
        title: 'Grow Your Channel: YouTube Videos That Keep People Watching',
        description: "From eye-catching intros to seamless transitions and retention-boosting edits — our AI helps you create content that ranks, retains, and converts viewers into subscribers. Stop guessing, start growing.",
        author: 'Emma Davis',
        date: '5 April 2023',
        image: getImageUrl('/video.svg'),
        useCase: 'YouTube Videos'
    }
])

// Computed property for filtered cards
const filteredCards = computed(() => {
    return cardsData.value.filter(card => card.category === activePill.value)
})

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

.card-fade-enter-active,
.card-fade-leave-active {
    transition: opacity 0.3s ease, transform 0.3s ease;
}

.card-fade-enter-from {
    opacity: 0;
    transform: translateY(10px);
}

.card-fade-leave-to {
    opacity: 0;
    transform: translateY(-10px);
}
</style>
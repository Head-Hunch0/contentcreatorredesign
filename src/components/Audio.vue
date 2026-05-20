<template>
    <section class="py-12 lg:py-16 ">
        <div class="max-w-7xl mx-auto px-4 xl:px-0">
            <div
                class="flex flex-col items-start sm:items-center sm:text-center md:px-4 lg:items-start lg:px-8 lg:text-left">
                <div
                    class="items-center justify-center rounded-full text-sm font-medium whitespace-nowrap shadow-[0_2px_10px_0px_rgba(0,0,0,0.15)] inline-flex bg-white text-neutral-700 px-2.5 py-1">
                    🔊 Sound Effects
                </div>
                <div
                    class="mt-8 bg-gradient-to-b from-slate-800 to-slate-600 bg-clip-text text-3xl font-semibold text-transparent sm:w-4/5 md:w-3/5 lg:mt-9 lg:w-11/12 lg:text-4xl lg:leading-tight">
                    60,000+ Professional Sound Effects
                </div>
                <p
                    class="text-sm font-medium text-slate-600 leading-normal lg:leading-normal lg:text-base mt-4 sm:w-2/3 md:w-1/2 xl:w-1/2">
                    Hear the difference quality audio makes. Drag, drop, done.
                </p>
            </div>

            <div class="mt-10 lg:mt-14">
                <div class="rounded-2xl border border-neutral-200 bg-white p-4 md:p-6">
                    <div class="flex flex-col lg:flex-row lg:items-start gap-6">
                        <div class="flex-1">
                            <div class="relative rounded-xl overflow-hidden bg-slate-900 shadow-lg">
                                <div class="relative">
                                    <img src="https://picsum.photos/id/20/800/450" alt="Video thumbnail"
                                        class="w-full h-auto opacity-90" />
                                    <div class="absolute inset-0 flex items-center justify-center">
                                        <div class="w-16 h-16 rounded-full bg-white/20 backdrop-blur flex items-center justify-center cursor-pointer hover:bg-white/30 transition-all"
                                            @click="togglePlay">
                                            <svg v-if="!isPlaying" class="w-8 h-8 text-white ml-1" fill="currentColor"
                                                viewBox="0 0 24 24">
                                                <path d="M8 5v14l11-7z" />
                                            </svg>
                                            <svg v-else class="w-8 h-8 text-white" fill="currentColor"
                                                viewBox="0 0 24 24">
                                                <path d="M6 19h4V5H6v14zm8-14v14h4V5h-4z" />
                                            </svg>
                                        </div>
                                    </div>
                                </div>

                                <div
                                    class="absolute bottom-0 left-0 right-0 bg-gradient-to-t from-black/70 to-transparent p-4">
                                    <div class="flex items-center gap-3">
                                        <div class="text-white text-xs font-medium">SFX:</div>
                                        <div class="flex-1 h-12 flex items-center gap-0.5">
                                            <div v-for="(height, idx) in waveformHeights" :key="idx"
                                                class="flex-1 bg-white/40 rounded-t transition-all duration-75"
                                                :style="{ height: isPlaying ? height + 'px' : '4px' }">
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>

                            <div class="mt-4 space-y-3">
                                <div class="flex items-center gap-3">
                                    <button @click="toggleMute"
                                        class="p-2 rounded-lg bg-neutral-100 hover:bg-neutral-200 transition-colors">
                                        <svg v-if="!isMuted" class="w-5 h-5 text-slate-700" fill="none"
                                            stroke="currentColor" viewBox="0 0 24 24">
                                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                                d="M15.536 8.464a5 5 0 010 7.072m2.828-9.9a9 9 0 010 12.728M5.586 15H4a1 1 0 01-1-1v-4a1 1 0 011-1h1.586l4.707-4.707C10.923 3.663 12 4.109 12 5v14c0 .891-1.077 1.337-1.707.707L5.586 15z" />
                                        </svg>
                                        <svg v-else class="w-5 h-5 text-slate-700" fill="none" stroke="currentColor"
                                            viewBox="0 0 24 24">
                                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                                d="M5.586 15H4a1 1 0 01-1-1v-4a1 1 0 011-1h1.586l4.707-4.707C10.923 3.663 12 4.109 12 5v14c0 .891-1.077 1.337-1.707.707L5.586 15zM17 14l2-2m0 0l2-2m-2 2l-2-2m2 2l2 2" />
                                        </svg>
                                    </button>

                                    <input type="range" v-model="volumeValue" min="0" max="100"
                                        class="w-24 h-1 bg-neutral-200 rounded-lg appearance-none cursor-pointer"
                                        @input="updateVolume" />

                                    <div class="flex-1 text-right">
                                        <span class="text-xs text-slate-500">{{ formatTime(currentTimeValue) }} /
                                            {{ formatTime(durationValue) }}</span>
                                    </div>
                                </div>

                                <input type="range" v-model="progressValue" min="0" max="100"
                                    class="w-full h-1 bg-neutral-200 rounded-lg appearance-none cursor-pointer"
                                    @input="seekAudio" />
                            </div>
                        </div>

                        <div class="flex-1">
                            <div class="flex items-center justify-between mb-4">
                                <h3 class="font-semibold text-slate-900">Choose a sound effect:</h3>
                                <div class="text-xs text-slate-400">{{ currentSound.name }}</div>
                            </div>

                            <div class="space-y-2 max-h-96 overflow-y-auto pr-2">
                                <button v-for="sound in sounds" :key="sound.id" @click="playSound(sound)"
                                    class="w-full text-left p-3 rounded-lg transition-all"
                                    :class="currentSound.id === sound.id ? 'bg-slate-900 text-white shadow-md' : 'bg-neutral-100 hover:bg-neutral-200 text-slate-700'">
                                    <div class="flex items-center justify-between">
                                        <div class="flex items-center gap-3">
                                            <div class="w-8 h-8 rounded-full flex items-center justify-center"
                                                :class="currentSound.id === sound.id ? 'bg-white/20' : 'bg-white'">
                                                <svg v-if="currentSound.id !== sound.id" class="w-4 h-4 text-slate-600"
                                                    fill="currentColor" viewBox="0 0 24 24">
                                                    <path d="M8 5v14l11-7z" />
                                                </svg>
                                                <svg v-else-if="isPlaying && currentSound.id === sound.id"
                                                    class="w-4 h-4 text-white" fill="currentColor" viewBox="0 0 24 24">
                                                    <path d="M6 19h4V5H6v14zm8-14v14h4V5h-4z" />
                                                </svg>
                                                <svg v-else-if="!isPlaying && currentSound.id === sound.id"
                                                    class="w-4 h-4 text-white" fill="currentColor" viewBox="0 0 24 24">
                                                    <path d="M8 5v14l11-7z" />
                                                </svg>
                                            </div>
                                            <div>
                                                <div class="font-medium text-sm">{{ sound.name }}</div>
                                                <div class="text-xs opacity-70">{{ sound.category }}</div>
                                            </div>
                                        </div>
                                        <div class="text-xs opacity-60">{{ sound.duration }}</div>
                                    </div>
                                </button>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <div class="mt-10 grid grid-cols-2 gap-4 md:grid-cols-4">
                <div class="rounded-xl border border-neutral-200 bg-white p-4 text-center">
                    <div class="text-2xl font-bold text-slate-900">60,000+</div>
                    <div class="text-xs text-slate-500 mt-1">Sound Effects</div>
                </div>
                <div class="rounded-xl border border-neutral-200 bg-white p-4 text-center">
                    <div class="text-2xl font-bold text-slate-900">500+</div>
                    <div class="text-xs text-slate-500 mt-1">Categories</div>
                </div>
                <div class="rounded-xl border border-neutral-200 bg-white p-4 text-center">
                    <div class="text-2xl font-bold text-slate-900">96kHz</div>
                    <div class="text-xs text-slate-500 mt-1">Studio Quality</div>
                </div>
                <div class="rounded-xl border border-neutral-200 bg-white p-4 text-center">
                    <div class="text-2xl font-bold text-slate-900">Royalty-Free</div>
                    <div class="text-xs text-slate-500 mt-1">Commercial Use</div>
                </div>
            </div>

            <div class="mt-10 text-center">
                <button
                    class="inline-flex items-center justify-center rounded-xl bg-slate-900 px-6 py-3 text-sm font-medium text-white shadow-sm transition-all hover:bg-slate-800">
                    Explore All 60,000+ Sounds
                    <svg class="ml-2 h-4 w-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
                    </svg>
                </button>
                <p class="text-xs text-slate-400 mt-3">All sounds are royalty-free for commercial use</p>
            </div>
        </div>
    </section>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

interface Sound {
    id: number
    name: string
    category: string
    duration: string
    url: string
}

const sounds = ref<Sound[]>([
    {
        id: 1,
        name: 'Cinematic Boom',
        category: 'Impact',
        duration: '0:03',
        url: 'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3'
    },
    {
        id: 2,
        name: 'Whoosh Transition',
        category: 'Whoosh',
        duration: '0:02',
        url: 'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-2.mp3'
    },
    {
        id: 3,
        name: 'Ambient Drone',
        category: 'Atmosphere',
        duration: '0:08',
        url: 'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-3.mp3'
    },
    {
        id: 4,
        name: 'Glitch Effect',
        category: 'Digital',
        duration: '0:01',
        url: 'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-4.mp3'
    },
    {
        id: 5,
        name: 'Rising Tension',
        category: 'Build Up',
        duration: '0:05',
        url: 'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-5.mp3'
    },
    {
        id: 6,
        name: 'Soft Piano Hit',
        category: 'Musical',
        duration: '0:02',
        url: 'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-6.mp3'
    }
])

const currentSound = ref<Sound>(sounds.value[0])
const isPlaying = ref(false)
const isMuted = ref(false)
const volumeValue = ref(80)
const currentTimeValue = ref(0)
const durationValue = ref(0)
const progressValue = ref(0)
const waveformHeights = ref<number[]>(Array(40).fill(4))

let audio: HTMLAudioElement | null = null
let animationFrame: number | null = null
let isSeeking = false

const initAudio = () => {
    if (audio) {
        audio.pause()
        audio.removeEventListener('timeupdate', updateProgress)
        audio.removeEventListener('loadedmetadata', onLoadedMetadata)
        audio.removeEventListener('ended', onEnded)
        audio = null
    }

    audio = new Audio(currentSound.value.url)
    audio.volume = volumeValue.value / 100
    audio.loop = false

    audio.addEventListener('timeupdate', updateProgress)
    audio.addEventListener('loadedmetadata', onLoadedMetadata)
    audio.addEventListener('ended', onEnded)
}

const onLoadedMetadata = () => {
    if (audio) {
        durationValue.value = audio.duration
    }
}

const onEnded = () => {
    isPlaying.value = false
    currentTimeValue.value = 0
    progressValue.value = 0
    if (animationFrame) cancelAnimationFrame(animationFrame)
    waveformHeights.value = Array(40).fill(4)
}

const updateProgress = () => {
    if (audio && !isSeeking) {
        currentTimeValue.value = audio.currentTime
        progressValue.value = (audio.currentTime / audio.duration) * 100
    }
}

const playSound = (sound: Sound) => {
    if (currentSound.value.id !== sound.id) {
        currentSound.value = sound
        initAudio()
    }

    if (isPlaying.value) {
        audio?.pause()
        isPlaying.value = false
        if (animationFrame) cancelAnimationFrame(animationFrame)
    }

    audio?.play()
    isPlaying.value = true
    startWaveformAnimation()
}

const togglePlay = () => {
    if (isPlaying.value) {
        audio?.pause()
        isPlaying.value = false
        if (animationFrame) cancelAnimationFrame(animationFrame)
    } else {
        if (!audio) initAudio()
        audio?.play()
        isPlaying.value = true
        startWaveformAnimation()
    }
}

const toggleMute = () => {
    isMuted.value = !isMuted.value
    if (audio) {
        audio.muted = isMuted.value
    }
}

const updateVolume = () => {
    if (audio) {
        audio.volume = volumeValue.value / 100
    }
}

const seekAudio = () => {
    if (audio && durationValue.value) {
        isSeeking = true
        const seekTime = (progressValue.value / 100) * durationValue.value
        audio.currentTime = seekTime
        currentTimeValue.value = seekTime
        setTimeout(() => {
            isSeeking = false
        }, 50)
    }
}

const formatTime = (seconds: number): string => {
    if (isNaN(seconds) || !isFinite(seconds)) return '0:00'
    const mins = Math.floor(seconds / 60)
    const secs = Math.floor(seconds % 60)
    return `${mins}:${secs.toString().padStart(2, '0')}`
}

const startWaveformAnimation = () => {
    if (animationFrame) cancelAnimationFrame(animationFrame)

    const animate = () => {
        if (isPlaying.value) {
            waveformHeights.value = waveformHeights.value.map(() => Math.random() * 40 + 4)
            animationFrame = requestAnimationFrame(animate)
        } else {
            waveformHeights.value = Array(40).fill(4)
        }
    }
    animate()
}

onMounted(() => {
    initAudio()
})

onUnmounted(() => {
    if (audio) {
        audio.pause()
        audio = null
    }
    if (animationFrame) cancelAnimationFrame(animationFrame)
})
</script>

<style scoped>
input[type="range"] {
    -webkit-appearance: none;
    background: #e5e5e5;
}

input[type="range"]:focus {
    outline: none;
}

input[type="range"]::-webkit-slider-thumb {
    -webkit-appearance: none;
    width: 12px;
    height: 12px;
    border-radius: 50%;
    background: #0f172a;
    cursor: pointer;
    border: 2px solid white;
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.2);
}

input[type="range"]::-webkit-slider-thumb:hover {
    transform: scale(1.2);
}

input.w-24::-webkit-slider-thumb {
    width: 10px;
    height: 10px;
}

.max-h-96::-webkit-scrollbar {
    width: 6px;
}

.max-h-96::-webkit-scrollbar-track {
    background: #e5e5e5;
    border-radius: 10px;
}

.max-h-96::-webkit-scrollbar-thumb {
    background: #a3a3a3;
    border-radius: 10px;
}

.max-h-96::-webkit-scrollbar-thumb:hover {
    background: #737373;
}
</style>
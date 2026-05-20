<template>
    <section class="px-16">
        <div class="mb-4 rounded-lg bg-amber-50 border border-amber-200 p-3">
            <div class="flex items-center gap-2 text-sm text-amber-700">
                <svg class="w-5 h-5 flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                        d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                </svg>
                <span>UI Prototype Demo – Shows workflow only.</span>
            </div>
        </div>
    </section>
    <section class="py-12 lg:py-16 bg-white">
        <div class="max-w-7xl mx-auto px-4 xl:px-0">
            <div
                class="flex flex-col items-start sm:items-center sm:text-center md:px-4 lg:items-start lg:px-8 lg:text-left">
                <div
                    class="items-center justify-center rounded-full text-sm font-medium whitespace-nowrap shadow-[0_2px_10px_0px_rgba(0,0,0,0.15)] inline-flex bg-white text-neutral-700 px-2.5 py-1">
                    🤖 AI Video Generator
                </div>
                <div
                    class="mt-8 bg-gradient-to-b from-slate-800 to-slate-600 bg-clip-text text-3xl font-semibold text-transparent sm:w-4/5 md:w-3/5 lg:mt-9 lg:w-11/12 lg:text-4xl lg:leading-tight">
                    Create Stunning Videos with AI
                </div>
                <p
                    class="text-sm font-medium text-slate-600 leading-normal lg:leading-normal lg:text-base mt-4 sm:w-2/3 md:w-1/2 xl:w-1/2">
                    Powered by Veo, Kling, Nano Banana & more. Generate professional videos in seconds.
                </p>
            </div>

            <div class="mt-10 lg:mt-14">
                <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
                    <div class="lg:col-span-2 space-y-6">
                        <div class="rounded-2xl border border-neutral-200 bg-white p-6 shadow-sm">
                            <label class="block text-sm font-medium text-slate-700 mb-2">
                                Prompt
                                <span class="text-xs text-slate-400 ml-2">Describe the video you want to create</span>
                            </label>
                            <textarea v-model="prompt" rows="4"
                                class="w-full rounded-xl border border-neutral-200 p-4 text-sm focus:border-slate-400 focus:outline-none focus:ring-1 focus:ring-slate-400"
                                placeholder="E.g., Cinematic drone shot flying over mountains at sunset, 4k, dramatic lighting..."></textarea>

                            <div class="mt-3 flex flex-wrap gap-2">
                                <button v-for="example in examplePrompts" :key="example" @click="prompt = example"
                                    class="rounded-full bg-neutral-100 px-3 py-1.5 text-xs text-slate-600 hover:bg-neutral-200 transition-colors">
                                    {{ example }}
                                </button>
                            </div>
                        </div>

                        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                            <div class="rounded-2xl border border-neutral-200 bg-white p-6 shadow-sm">
                                <label class="block text-sm font-medium text-slate-700 mb-3">AI Model</label>
                                <div class="space-y-2">
                                    <button v-for="model in models" :key="model.id" @click="selectedModel = model.id"
                                        class="w-full flex items-center justify-between p-3 rounded-xl transition-all"
                                        :class="selectedModel === model.id ? 'bg-slate-900 text-white' : 'bg-neutral-50 hover:bg-neutral-100 text-slate-700'">
                                        <div class="flex items-center gap-3">
                                            <div class="w-8 h-8 rounded-full flex items-center justify-center"
                                                :class="selectedModel === model.id ? 'bg-white/20' : 'bg-white'">
                                                <span class="text-sm">{{ model.emoji }}</span>
                                            </div>
                                            <div class="text-left">
                                                <div class="text-sm font-medium">{{ model.name }}</div>
                                                <div class="text-xs opacity-70">{{ model.description }}</div>
                                            </div>
                                        </div>
                                        <div class="text-xs"
                                            :class="selectedModel === model.id ? 'text-white/70' : 'text-slate-400'">
                                            {{ model.creditCost }} credits
                                        </div>
                                    </button>
                                </div>
                            </div>

                            <div class="rounded-2xl border border-neutral-200 bg-white p-6 shadow-sm space-y-4">
                                <label class="block text-sm font-medium text-slate-700">Settings</label>

                                <div>
                                    <div class="flex justify-between text-xs text-slate-500 mb-2">
                                        <span>Aspect Ratio</span>
                                        <span>{{ aspectRatioLabel }}</span>
                                    </div>
                                    <div class="flex gap-2">
                                        <button v-for="ratio in aspectRatios" :key="ratio.value"
                                            @click="selectedAspectRatio = ratio.value"
                                            class="flex-1 py-2 rounded-lg text-xs font-medium transition-all"
                                            :class="selectedAspectRatio === ratio.value ? 'bg-slate-900 text-white' : 'bg-neutral-100 text-slate-600 hover:bg-neutral-200'">
                                            {{ ratio.label }}
                                        </button>
                                    </div>
                                </div>

                                <div>
                                    <div class="flex justify-between text-xs text-slate-500 mb-2">
                                        <span>Duration</span>
                                        <span>{{ selectedDuration }}s</span>
                                    </div>
                                    <input type="range" v-model="selectedDuration" min="5" max="15" step="5"
                                        class="w-full h-1 bg-neutral-200 rounded-lg appearance-none cursor-pointer" />
                                    <div class="flex justify-between text-xs text-slate-400 mt-1">
                                        <span>5s</span>
                                        <span>10s</span>
                                        <span>15s</span>
                                    </div>
                                </div>

                                <div>
                                    <div class="flex justify-between text-xs text-slate-500 mb-2">
                                        <span>Quality</span>
                                        <span>{{ selectedQuality === 'fast' ? 'Fast (cheaper)' : 'Premium (better)' }}</span>
                                    </div>
                                    <div class="flex gap-2">
                                        <button v-for="quality in qualities" :key="quality.value"
                                            @click="selectedQuality = quality.value"
                                            class="flex-1 py-2 rounded-lg text-xs font-medium transition-all"
                                            :class="selectedQuality === quality.value ? 'bg-slate-900 text-white' : 'bg-neutral-100 text-slate-600 hover:bg-neutral-200'">
                                            {{ quality.label }}
                                        </button>
                                    </div>
                                </div>
                            </div>
                        </div>

                        <div
                            class="rounded-2xl border border-neutral-200 bg-gradient-to-r from-slate-50 to-neutral-50 p-6">
                            <div class="flex flex-col sm:flex-row sm:items-center sm:justify-between gap-4">
                                <div>
                                    <div class="text-sm text-slate-500">Estimated cost</div>
                                    <div class="text-2xl font-bold text-slate-900">{{ totalCreditCost }} credits</div>
                                    <div class="text-xs text-slate-400 mt-1">Your balance: {{ creditBalance }} credits
                                    </div>
                                </div>
                                <button @click="generateVideo" :disabled="isGenerating || !prompt.trim()"
                                    class="inline-flex items-center justify-center rounded-xl px-8 py-3 text-sm font-medium text-white transition-all"
                                    :class="isGenerating || !prompt.trim() ? 'bg-slate-400 cursor-not-allowed' : 'bg-slate-900 hover:bg-slate-800'">
                                    <svg v-if="isGenerating" class="animate-spin h-4 w-4 mr-2 text-white" fill="none"
                                        viewBox="0 0 24 24">
                                        <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor"
                                            stroke-width="4"></circle>
                                        <path class="opacity-75" fill="currentColor"
                                            d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z">
                                        </path>
                                    </svg>
                                    <span v-else>Generate Video</span>
                                </button>
                            </div>
                            <p class="text-xs text-slate-400 mt-4 flex items-center gap-2">
                                <svg class="w-3 h-3" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                        d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                                </svg>
                                Generation typically takes 30-60 seconds
                            </p>
                        </div>
                    </div>

                    <div class="space-y-6">
                        <div class="rounded-2xl border border-neutral-200 bg-white p-6 shadow-sm">
                            <h3 class="text-sm font-medium text-slate-700 mb-3">Generated Video</h3>
                            <div
                                class="aspect-video rounded-xl bg-gradient-to-br from-slate-100 to-neutral-100 flex items-center justify-center overflow-hidden">
                                <div v-if="!generatedVideoUrl && !isGenerating" class="text-center">
                                    <svg class="w-12 h-12 text-slate-300 mx-auto mb-2" fill="none" stroke="currentColor"
                                        viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                            d="M15 10l4.553-2.276A1 1 0 0121 8.618v6.764a1 1 0 01-1.447.894L15 14M5 18h8a2 2 0 002-2V8a2 2 0 00-2-2H5a2 2 0 00-2 2v8a2 2 0 002 2z">
                                        </path>
                                    </svg>
                                    <p class="text-sm text-slate-400">Your video will appear here</p>
                                </div>
                                <div v-else-if="isGenerating" class="text-center">
                                    <div
                                        class="w-12 h-12 border-4 border-slate-200 border-t-slate-900 rounded-full animate-spin mx-auto mb-2">
                                    </div>
                                    <p class="text-sm text-slate-500">Generating...</p>
                                    <p class="text-xs text-slate-400 mt-1">{{ generationProgress }}</p>
                                </div>
                                <video v-else :src="generatedVideoUrl" controls
                                    class="w-full h-full object-cover"></video>
                            </div>

                            <button v-if="generatedVideoUrl" @click="downloadVideo"
                                class="w-full mt-4 inline-flex items-center justify-center gap-2 rounded-xl border border-slate-200 bg-white px-4 py-2 text-sm font-medium text-slate-700 hover:bg-slate-50 transition-colors">
                                <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                        d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4"></path>
                                </svg>
                                Download Video
                            </button>
                        </div>

                        <div class="rounded-2xl border border-neutral-200 bg-white p-6 shadow-sm">
                            <div class="flex items-center justify-between mb-3">
                                <h3 class="text-sm font-medium text-slate-700">Recent Generations</h3>
                                <button @click="clearHistory"
                                    class="text-xs text-slate-400 hover:text-slate-600">Clear</button>
                            </div>
                            <div class="space-y-3 max-h-80 overflow-y-auto">
                                <div v-for="item in history" :key="item.id"
                                    class="flex gap-3 p-2 rounded-lg hover:bg-neutral-50 cursor-pointer transition-colors"
                                    @click="reuseGeneration(item)">
                                    <div
                                        class="w-16 h-12 rounded bg-slate-100 flex items-center justify-center overflow-hidden">
                                        <svg class="w-6 h-6 text-slate-400" fill="none" stroke="currentColor"
                                            viewBox="0 0 24 24">
                                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                                d="M15 10l4.553-2.276A1 1 0 0121 8.618v6.764a1 1 0 01-1.447.894L15 14M5 18h8a2 2 0 002-2V8a2 2 0 00-2-2H5a2 2 0 00-2 2v8a2 2 0 002 2z">
                                            </path>
                                        </svg>
                                    </div>
                                    <div class="flex-1 min-w-0">
                                        <p class="text-xs font-medium text-slate-700 truncate">
                                            {{ item.prompt.substring(0, 50) }}...</p>
                                        <div class="flex items-center gap-2 mt-1">
                                            <span class="text-xs text-slate-400">{{ item.model }}</span>
                                            <span class="text-xs text-slate-300">•</span>
                                            <span class="text-xs text-slate-400">{{ item.date }}</span>
                                        </div>
                                    </div>
                                </div>
                                <div v-if="history.length === 0" class="text-center py-8">
                                    <p class="text-sm text-slate-400">No generations yet</p>
                                    <p class="text-xs text-slate-300 mt-1">Your history will appear here</p>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'

interface Model {
    id: string
    name: string
    description: string
    emoji: string
    creditCost: number
}

interface HistoryItem {
    id: number
    prompt: string
    model: string
    date: string
    videoUrl: string
}

const prompt = ref('')
const selectedModel = ref('veo')
const selectedAspectRatio = ref('16:9')
const selectedDuration = ref(5)
const selectedQuality = ref('premium')
const isGenerating = ref(false)
const generationProgress = ref('')
const generatedVideoUrl = ref('')
const creditBalance = ref(247)

const history = ref<HistoryItem[]>([])

const models = ref<Model[]>([
    {
        id: 'veo',
        name: 'Veo',
        description: 'Best for realism',
        emoji: '🎥',
        creditCost: 15
    },
    {
        id: 'kling',
        name: 'Kling',
        description: 'Great for motion',
        emoji: '🎬',
        creditCost: 12
    },
    {
        id: 'nano-banana',
        name: 'Nano Banana',
        description: 'Fast & efficient',
        emoji: '🍌',
        creditCost: 8
    },
    {
        id: 'seedance',
        name: 'Seedance',
        description: 'Cinematic quality',
        emoji: '✨',
        creditCost: 20
    }
])

const aspectRatios = ref([
    { value: '16:9', label: '16:9' },
    { value: '9:16', label: '9:16' },
    { value: '1:1', label: '1:1' }
])

const qualities = ref([
    { value: 'fast', label: 'Fast' },
    { value: 'premium', label: 'Premium' }
])

const examplePrompts = ref([
    'Cinematic drone shot flying over mountains at sunset',
    'Product rotating on white background, studio lighting',
    'Animated explainer video about AI technology',
    'Slow motion waterfall in a tropical forest, 4k'
])

const aspectRatioLabel = computed(() => {
    const ratio = aspectRatios.value.find(r => r.value === selectedAspectRatio.value)
    return ratio?.label || '16:9'
})

const totalCreditCost = computed(() => {
    const model = models.value.find(m => m.id === selectedModel.value)
    const baseCost = model?.creditCost || 10
    const durationMultiplier = selectedDuration.value / 5
    const qualityMultiplier = selectedQuality.value === 'premium' ? 1.5 : 1
    return Math.round(baseCost * durationMultiplier * qualityMultiplier)
})

const generateVideo = async () => {
    if (!prompt.value.trim()) return
    if (creditBalance.value < totalCreditCost.value) {
        alert(`Insufficient credits. Need ${totalCreditCost.value} credits but you have ${creditBalance.value}.`)
        return
    }

    isGenerating.value = true
    creditBalance.value -= totalCreditCost.value

    const steps = ['Initializing AI model...', 'Analyzing prompt...', 'Generating frames...', 'Rendering video...', 'Finalizing...']
    for (let i = 0; i < steps.length; i++) {
        generationProgress.value = steps[i]
        await new Promise(resolve => setTimeout(resolve, 800))
    }

    generatedVideoUrl.value = 'https://sample-videos.com/video123/mp4/720/big_buck_bunny_720p_1mb.mp4'

    const modelName = models.value.find(m => m.id === selectedModel.value)?.name || 'Unknown'
    history.value.unshift({
        id: Date.now(),
        prompt: prompt.value,
        model: modelName,
        date: new Date().toLocaleTimeString(),
        videoUrl: generatedVideoUrl.value
    })

    isGenerating.value = false
    generationProgress.value = ''
}

const downloadVideo = () => {
    const link = document.createElement('a')
    link.href = generatedVideoUrl.value
    link.download = `ai-video-${Date.now()}.mp4`
    link.click()
}

const reuseGeneration = (item: HistoryItem) => {
    prompt.value = item.prompt
    generatedVideoUrl.value = item.videoUrl
}

const clearHistory = () => {
    history.value = []
}
</script>

<style scoped>
input[type="range"] {
    -webkit-appearance: none;
}

input[type="range"]:focus {
    outline: none;
}

input[type="range"]::-webkit-slider-thumb {
    -webkit-appearance: none;
    width: 14px;
    height: 14px;
    border-radius: 50%;
    background: #0f172a;
    cursor: pointer;
    border: 2px solid white;
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
}

@keyframes spin {
    from {
        transform: rotate(0deg);
    }

    to {
        transform: rotate(360deg);
    }
}

.animate-spin {
    animation: spin 1s linear infinite;
}

.max-h-80 {
    max-height: 320px;
}

.max-h-80::-webkit-scrollbar {
    width: 4px;
}

.max-h-80::-webkit-scrollbar-track {
    background: #e5e5e5;
    border-radius: 10px;
}

.max-h-80::-webkit-scrollbar-thumb {
    background: #a3a3a3;
    border-radius: 10px;
}
</style>
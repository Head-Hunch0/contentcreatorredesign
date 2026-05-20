<template>
    <section class="py-12 lg:py-16 bg-white">
        <div class="max-w-7xl mx-auto px-4 xl:px-0">
            <!-- Section Header -->
            <div
                class="flex flex-col items-start sm:items-center sm:text-center md:px-4 lg:items-start lg:px-8 lg:text-left">
                <div
                    class="items-center justify-center rounded-full text-sm font-medium whitespace-nowrap shadow-[0_2px_10px_0px_rgba(0,0,0,0.15)] inline-flex bg-white text-neutral-700 px-2.5 py-1">
                    🎨 Color Grading
                </div>
                <div
                    class="mt-8 bg-gradient-to-b from-slate-800 to-slate-600 bg-clip-text text-3xl font-semibold text-transparent sm:w-4/5 md:w-3/5 lg:mt-9 lg:w-11/12 lg:text-4xl lg:leading-tight">
                    Transform Your Footage with Professional LUTs
                </div>
                <p
                    class="text-sm font-medium text-slate-600 leading-normal lg:leading-normal lg:text-base mt-4 sm:w-2/3 md:w-1/2 xl:w-1/2">
                    Used by Hollywood editors. One click. Instant cinematic color.
                </p>
            </div>

            <!-- Before/After Slider Showcase -->
            <div class="mt-10 lg:mt-14">
                <div class="rounded-2xl border border-neutral-200 bg-neutral-50 p-4 md:p-6">
                    <div class="flex flex-col lg:flex-row lg:items-start lg:justify-between gap-6">
                        <!-- Slider Container -->
                        <div class="flex-1">
                            <div ref="sliderContainer"
                                class="relative w-full overflow-hidden rounded-xl shadow-lg cursor-ew-resize"
                                @mousemove="onDrag" @mousedown="startDrag" @mouseup="stopDrag" @mouseleave="stopDrag"
                                @touchmove="onTouchDrag" @touchstart="startTouchDrag" @touchend="stopDrag">
                                <div class="relative">
                                    <img :src="currentImage.after" alt="After LUT applied"
                                        class="w-full h-auto pointer-events-none"
                                        :style="{ filter: currentImage.filter }" />
                                    <div class="absolute top-0 left-0 h-full overflow-hidden pointer-events-none"
                                        :style="{ width: sliderPosition + '%' }">
                                        <img :src="currentImage.before" alt="Before LUT" class="w-full h-auto" />
                                    </div>
                                    <div class="absolute top-0 bottom-0 w-1 bg-white shadow-lg cursor-ew-resize z-10"
                                        :style="{ left: `calc(${sliderPosition}% - 2px)` }">
                                        <div
                                            class="absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 bg-white rounded-full p-1 shadow-lg">
                                            <svg class="w-4 h-4 text-slate-700" fill="none" stroke="currentColor"
                                                viewBox="0 0 24 24">
                                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                                    d="M8 9l4-4 4 4m0 6l-4 4-4-4" />
                                            </svg>
                                        </div>
                                    </div>
                                </div>
                            </div>

                            <div class="flex justify-between mt-3 text-xs font-medium text-slate-500">
                                <span>Before (Original)</span>
                                <span>After (LUT Applied)</span>
                            </div>

                            <input type="range" min="0" max="100" v-model="sliderPosition"
                                class="w-full mt-4 h-1 bg-neutral-200 rounded-lg appearance-none cursor-pointer" />
                        </div>

                        <!-- Info Panel -->
                        <div class="flex-1 space-y-4">
                            <div>
                                <h3 class="text-xl font-semibold text-slate-900">{{ currentImage.name }}</h3>
                                <p class="text-sm text-slate-500 mt-1">{{ currentImage.description }}</p>
                            </div>

                            <div class="flex flex-wrap gap-2">
                                <span v-for="tag in currentImage.tags" :key="tag"
                                    class="rounded-full bg-neutral-200 px-3 py-1 text-xs font-medium text-neutral-700">
                                    {{ tag }}
                                </span>
                            </div>

                            <div class="border-t border-neutral-200 pt-4">
                                <div class="flex items-center gap-2 text-sm text-slate-600">
                                    <svg class="w-5 h-5 text-green-600 flex-shrink-0" fill="none" stroke="currentColor"
                                        viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                            d="M5 13l4 4L19 7" />
                                    </svg>
                                    <span>Works with Premiere Pro, DaVinci Resolve, Final Cut, and more</span>
                                </div>
                                <div class="flex items-center gap-2 mt-2 text-sm text-slate-600">
                                    <svg class="w-5 h-5 text-green-600 flex-shrink-0" fill="none" stroke="currentColor"
                                        viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                            d="M4 16l4.586-4.586a2 2 0 012.828 0L16 16m-2-2l1.586-1.586a2 2 0 012.828 0L20 14m-6-6h.01M6 20h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z" />
                                    </svg>
                                    <span>Drag & drop – no color grading experience needed</span>
                                </div>
                            </div>

                            <!-- Thumbnail Gallery -->
                            <div class="pt-2">
                                <p class="text-xs font-medium text-slate-500 mb-2">Try different LUTs:</p>
                                <div class="flex gap-2">
                                    <button v-for="(image, idx) in lutImages" :key="idx" @click="switchImage(image)"
                                        class="relative w-16 h-16 rounded-lg overflow-hidden border-2 transition-all"
                                        :class="currentImage.id === image.id ? 'border-slate-900 shadow-md' : 'border-transparent hover:border-slate-300'">
                                        <img :src="image.thumbnail" :alt="image.name"
                                            class="w-full h-full object-cover" />
                                        <div
                                            class="absolute bottom-0 left-0 right-0 bg-black/50 text-white text-[10px] font-medium text-center py-0.5">
                                            {{ image.name.split(' ')[0] }}
                                        </div>
                                    </button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Stats Row -->
            <div class="mt-10 grid grid-cols-2 gap-4 md:grid-cols-4">
                <div class="rounded-xl border border-neutral-200 bg-white p-4 text-center">
                    <div class="text-2xl font-bold text-slate-900">4,000+</div>
                    <div class="text-xs text-slate-500 mt-1">Professional LUTs</div>
                </div>
                <div class="rounded-xl border border-neutral-200 bg-white p-4 text-center">
                    <div class="text-2xl font-bold text-slate-900">50+</div>
                    <div class="text-xs text-slate-500 mt-1">Film Stock Emulations</div>
                </div>
                <div class="rounded-xl border border-neutral-200 bg-white p-4 text-center">
                    <div class="text-2xl font-bold text-slate-900">100%</div>
                    <div class="text-xs text-slate-500 mt-1">Camera Compatible</div>
                </div>
                <div class="rounded-xl border border-neutral-200 bg-white p-4 text-center">
                    <div class="text-2xl font-bold text-slate-900">1-Click</div>
                    <div class="text-xs text-slate-500 mt-1">Apply & Export</div>
                </div>
            </div>

            <!-- CTA -->
            <div class="mt-10 text-center">
                <button
                    class="inline-flex items-center justify-center rounded-xl bg-slate-900 px-6 py-3 text-sm font-medium text-white shadow-sm transition-all hover:bg-slate-800">
                    Access All 4,000+ LUTs
                    <svg class="ml-2 h-4 w-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
                    </svg>
                </button>
                <p class="text-xs text-slate-400 mt-3">Included with any PromptEdit subscription</p>
            </div>
        </div>
    </section>
</template>

<script setup lang="ts">
import { ref } from 'vue'

interface LutImage {
    id: number
    name: string
    description: string
    before: string
    after: string
    thumbnail: string
    tags: string[]
    filter: string
}

const lutImages = ref<LutImage[]>([
    {
        id: 1,
        name: 'Cinematic Warmth',
        description: 'Adds rich amber highlights and deep teal shadows – perfect for narrative and travel content',
        before: 'https://picsum.photos/id/104/800/500',
        after: 'https://picsum.photos/id/104/800/500',
        thumbnail: 'https://picsum.photos/id/104/100/100',
        tags: ['Cinematic', 'Warm', 'Teal & Orange'],
        filter: 'brightness(1.05) contrast(1.15) saturate(1.3) sepia(0.1) hue-rotate(-5deg)'
    },
    {
        id: 2,
        name: 'Moody Blue',
        description: 'Cool, desaturated look with lifted shadows – great for urban and dramatic scenes',
        before: 'https://picsum.photos/id/15/800/500',
        after: 'https://picsum.photos/id/15/800/500',
        thumbnail: 'https://picsum.photos/id/15/100/100',
        tags: ['Cool', 'Desaturated', 'Dramatic'],
        filter: 'brightness(0.95) contrast(1.2) saturate(0.7) hue-rotate(10deg)'
    },
    {
        id: 3,
        name: 'Vintage Film',
        description: 'Authentic 16mm film grain with subtle halation and warm skin tones',
        before: 'https://picsum.photos/id/106/800/500',
        after: 'https://picsum.photos/id/106/800/500',
        thumbnail: 'https://picsum.photos/id/106/100/100',
        tags: ['Vintage', 'Film Grain', 'Retro'],
        filter: 'brightness(1.02) contrast(0.95) saturate(0.85) sepia(0.15)'
    }
])

const currentImage = ref<LutImage>(lutImages.value[0])
const sliderPosition = ref(50)

let isDragging = false
const sliderContainer = ref<HTMLElement | null>(null)

const switchImage = (image: LutImage) => {
    currentImage.value = image
    sliderPosition.value = 50
}

const startDrag = (event: MouseEvent) => {
    isDragging = true
    event.preventDefault()
}

const onDrag = (event: MouseEvent) => {
    if (!isDragging || !sliderContainer.value) return

    const rect = sliderContainer.value.getBoundingClientRect()
    let newPosition = ((event.clientX - rect.left) / rect.width) * 100
    newPosition = Math.min(Math.max(newPosition, 0), 100)
    sliderPosition.value = newPosition
}

const stopDrag = () => {
    isDragging = false
}

const startTouchDrag = (event: TouchEvent) => {
    isDragging = true
    event.preventDefault()
}

const onTouchDrag = (event: TouchEvent) => {
    if (!isDragging || !sliderContainer.value || !event.touches.length) return

    const rect = sliderContainer.value.getBoundingClientRect()
    let newPosition = ((event.touches[0].clientX - rect.left) / rect.width) * 100
    newPosition = Math.min(Math.max(newPosition, 0), 100)
    sliderPosition.value = newPosition
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
    width: 16px;
    height: 16px;
    border-radius: 50%;
    background: #0f172a;
    cursor: pointer;
    border: 2px solid white;
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
}

input[type="range"]::-webkit-slider-thumb:hover {
    transform: scale(1.2);
}
</style>
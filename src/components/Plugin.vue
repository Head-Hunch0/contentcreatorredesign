<template>
    <section class="py-12 lg:py-16 bg-neutral-50">
        <div class="max-w-7xl mx-auto px-4 xl:px-0">
            <!-- Section Header -->
            <div
                class="flex flex-col items-start sm:items-center sm:text-center md:px-4 lg:items-start lg:px-8 lg:text-left">
                <div
                    class="items-center justify-center rounded-full text-sm font-medium whitespace-nowrap shadow-[0_2px_10px_0px_rgba(0,0,0,0.15)] inline-flex bg-white text-neutral-700 px-2.5 py-1">
                    🎬 Editing Software Plugins
                </div>
                <div
                    class="mt-8 bg-gradient-to-b from-slate-800 to-slate-600 bg-clip-text text-3xl font-semibold text-transparent sm:w-4/5 md:w-3/5 lg:mt-9 lg:w-11/12 lg:text-4xl lg:leading-tight">
                    AI Tools Inside Your Editing Software
                </div>
                <p
                    class="text-sm font-medium text-slate-600 leading-normal lg:leading-normal lg:text-base mt-4 sm:w-2/3 md:w-1/2 xl:w-1/2">
                    Available for Adobe Premiere Pro & DaVinci Resolve
                </p>
            </div>

            <!-- Plugin Showcase - Side by Side -->
            <div class="mt-10 grid grid-cols-1 lg:grid-cols-2 gap-6">
                <!-- Premiere Pro Plugin -->
                <div class="rounded-2xl border border-neutral-200 bg-white shadow-sm overflow-hidden">
                    <div
                        class="bg-gradient-to-r from-purple-600 to-purple-700 px-4 py-2 flex items-center justify-between">
                        <div class="flex items-center gap-2">
                            <span class="text-white font-semibold text-sm">Premiere Pro</span>
                            <span class="bg-white/20 text-white text-xs px-2 py-0.5 rounded">Extension</span>
                        </div>
                        <div class="flex gap-1">
                            <div class="w-3 h-3 rounded-full bg-red-500"></div>
                            <div class="w-3 h-3 rounded-full bg-yellow-500"></div>
                            <div class="w-3 h-3 rounded-full bg-green-500"></div>
                        </div>
                    </div>
                    <div class="p-4 bg-slate-900">
                        <!-- Plugin Panel UI -->
                        <div class="bg-slate-800 rounded-lg p-3">
                            <!-- Drag Handle -->
                            <div class="flex items-center justify-between mb-3 text-slate-400 text-xs">
                                <div class="flex items-center gap-2 cursor-move">
                                    <svg class="w-4 h-4" fill="currentColor" viewBox="0 0 24 24">
                                        <circle cx="9" cy="12" r="1.5" />
                                        <circle cx="15" cy="12" r="1.5" />
                                        <circle cx="9" cy="16" r="1.5" />
                                        <circle cx="15" cy="16" r="1.5" />
                                    </svg>
                                    <span>PromptEdit AI</span>
                                </div>
                                <div class="flex gap-2">
                                    <button class="hover:text-white">⚙️</button>
                                    <button class="hover:text-white">✖️</button>
                                </div>
                            </div>

                            <!-- Prompt Input (Compact) -->
                            <textarea v-model="pluginPrompt" rows="2"
                                class="w-full rounded-md bg-slate-700 border border-slate-600 p-2 text-sm text-white placeholder-slate-400 focus:outline-none focus:border-purple-500"
                                placeholder="Describe what you want to generate..."></textarea>

                            <!-- Model Selector (Compact) -->
                            <div class="mt-3 flex gap-2">
                                <select v-model="pluginModel"
                                    class="flex-1 rounded-md bg-slate-700 border border-slate-600 px-2 py-1.5 text-sm text-white">
                                    <option value="veo">Veo</option>
                                    <option value="kling">Kling</option>
                                    <option value="nano">Nano Banana</option>
                                </select>
                                <button
                                    class="px-3 py-1.5 bg-purple-600 hover:bg-purple-700 rounded-md text-sm text-white font-medium transition-colors">
                                    Generate
                                </button>
                            </div>

                            <!-- Insert Options -->
                            <div class="mt-3 flex gap-2">
                                <button
                                    class="flex-1 py-1.5 text-xs bg-slate-700 hover:bg-slate-600 rounded-md text-slate-300 transition-colors flex items-center justify-center gap-1">
                                    <svg class="w-3 h-3" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                            d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4"></path>
                                    </svg>
                                    Insert at Playhead
                                </button>
                                <button
                                    class="flex-1 py-1.5 text-xs bg-slate-700 hover:bg-slate-600 rounded-md text-slate-300 transition-colors flex items-center justify-center gap-1">
                                    <svg class="w-3 h-3" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                            d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z">
                                        </path>
                                    </svg>
                                    New Track
                                </button>
                            </div>

                            <!-- Credit Display (Compact) -->
                            <div class="mt-3 pt-2 border-t border-slate-700 flex justify-between text-xs">
                                <span class="text-slate-400">Available credits:</span>
                                <span class="text-white font-medium">{{ creditBalance }} credits</span>
                            </div>
                        </div>

                        <!-- Mock Timeline Preview -->
                        <div class="mt-3 bg-slate-950 rounded p-2">
                            <div class="flex items-center gap-1 text-[10px] text-slate-500 mb-1">
                                <span>V1</span>
                                <div class="flex-1 h-6 bg-slate-800 rounded flex items-center px-2">
                                    <span class="text-purple-400">← AI Generated Clip</span>
                                </div>
                            </div>
                            <div class="flex items-center gap-1 text-[10px] text-slate-500">
                                <span>A1</span>
                                <div class="flex-1 h-6 bg-slate-800 rounded"></div>
                            </div>
                        </div>
                    </div>
                    <div class="bg-slate-100 px-4 py-2 text-xs text-slate-500 flex justify-between">
                        <span>React + Tailwind</span>
                        <span>Compatible with Premiere Pro 2024+</span>
                    </div>
                </div>

                <!-- DaVinci Resolve Plugin -->
                <div class="rounded-2xl border border-neutral-200 bg-white shadow-sm overflow-hidden">
                    <div class="bg-gradient-to-r from-teal-600 to-teal-700 px-4 py-2 flex items-center justify-between">
                        <div class="flex items-center gap-2">
                            <span class="text-white font-semibold text-sm">DaVinci Resolve</span>
                            <span class="bg-white/20 text-white text-xs px-2 py-0.5 rounded">Extension</span>
                        </div>
                        <div class="flex gap-1">
                            <div class="w-3 h-3 rounded-full bg-red-500"></div>
                            <div class="w-3 h-3 rounded-full bg-yellow-500"></div>
                            <div class="w-3 h-3 rounded-full bg-green-500"></div>
                        </div>
                    </div>
                    <div class="p-4 bg-gray-900">
                        <div class="bg-gray-800 rounded-lg p-3">
                            <!-- Similar structure but DaVinci-specific styling -->
                            <div class="flex items-center justify-between mb-3 text-gray-400 text-xs">
                                <div class="flex items-center gap-2 cursor-move">
                                    <svg class="w-4 h-4" fill="currentColor" viewBox="0 0 24 24">
                                        <circle cx="9" cy="12" r="1.5" />
                                        <circle cx="15" cy="12" r="1.5" />
                                    </svg>
                                    <span>PromptEdit AI (Fusion)</span>
                                </div>
                            </div>

                            <textarea rows="2"
                                class="w-full rounded-md bg-gray-700 border border-gray-600 p-2 text-sm text-white placeholder-gray-400 focus:outline-none focus:border-teal-500"
                                placeholder="Enter prompt for DaVinci Fusion..." disabled></textarea>

                            <div class="mt-3 flex gap-2">
                                <button
                                    class="flex-1 py-2 bg-teal-600 hover:bg-teal-700 rounded-md text-sm text-white font-medium transition-colors opacity-50 cursor-not-allowed">
                                    Coming Soon
                                </button>
                            </div>

                            <div class="mt-3 text-center text-xs text-gray-500">
                                Fusion composition integration in development
                            </div>
                        </div>
                    </div>
                    <div class="bg-gray-100 px-4 py-2 text-xs text-gray-500 flex justify-between">
                        <span>React + Tailwind</span>
                        <span>Compatible with Resolve 18.5+</span>
                    </div>
                </div>
            </div>

            <!-- Feature List -->
            <div class="mt-8 grid grid-cols-2 md:grid-cols-4 gap-3">
                <div class="flex items-center gap-2 text-sm text-slate-600">
                    <svg class="w-4 h-4 text-green-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path>
                    </svg>
                    <span>No browser tab switching</span>
                </div>
                <div class="flex items-center gap-2 text-sm text-slate-600">
                    <svg class="w-4 h-4 text-green-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path>
                    </svg>
                    <span>Direct timeline insertion</span>
                </div>
                <div class="flex items-center gap-2 text-sm text-slate-600">
                    <svg class="w-4 h-4 text-green-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path>
                    </svg>
                    <span>Real-time credit checking</span>
                </div>
                <div class="flex items-center gap-2 text-sm text-slate-600">
                    <svg class="w-4 h-4 text-green-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path>
                    </svg>
                    <span>No rendering delays</span>
                </div>
            </div>
        </div>
    </section>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const pluginPrompt = ref('Cinematic sunset drone shot')
const pluginModel = ref('veo')
const creditBalance = ref(247)
</script>
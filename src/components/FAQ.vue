<template>
    <section class="pt-12 lg:pt-16 pb-6 lg:pb-16">
        <div class="max-w-7xl mx-auto px-4 xl:px-0">
            <div class="flex flex-col items-start md:px-4 lg:items-start lg:px-8">
                <div
                    class="items-center justify-center rounded-full text-sm font-medium whitespace-nowrap shadow-[0_2px_10px_0px_rgba(0,0,0,0.15)] inline-flex bg-white text-neutral-700 px-2.5 py-1">
                    {{ header.badge }}
                </div>
                <div
                    class="mt-8 bg-gradient-to-b from-slate-800 to-slate-600 bg-clip-text text-3xl font-semibold text-transparent sm:w-2/3 md:w-1/2 lg:mt-9 lg:text-4xl lg:leading-tight xl:w-2/3">
                    {{ header.title }}
                </div>
                <p
                    class="text-sm font-medium text-slate-600 leading-normal lg:leading-normal lg:text-base mt-4 sm:w-2/3 md:w-1/2 xl:w-2/5">
                    {{ header.description }}
                </p>
            </div>
            <div class="mt-4 border-b border-b-neutral-100 lg:mt-6"></div>
            <div class="mt-6 space-y-0.5 md:px-4 lg:mt-9 lg:px-8">
                <details v-for="(faq, index) in faqs" :key="index"
                    class="group open:bg-slate-50 divide-y divide-neutral-100 focus:shadow-[0_0px_2px_0px_rgba(0,0,0,0.10)] open:mt-3 open:rounded-2xl hover:rounded-2xl">
                    <summary
                        class="group/question flex cursor-pointer hover:opacity-90 transition-all items-center justify-between gap-x-4 rounded-t-2xl p-4">
                        <div class="font-semibold text-neutral-700 md:text-lg xl:text-xl">
                            {{ faq.question }}
                        </div>
                        <figure
                            class="hidden shrink-0 items-center gap-x-3 whitespace-nowrap rounded-full bg-slate-200 py-1.5 pl-3 pr-1.5 text-sm text-slate-600 transition-all group-open:flex">
                            Collapse
                            <svg class="h-5 text-slate-600" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"
                                fill="currentColor" aria-hidden="true" data-slot="icon">
                                <path fill-rule="evenodd"
                                    d="M4.25 12a.75.75 0 0 1 .75-.75h14a.75.75 0 0 1 0 1.5H5a.75.75 0 0 1-.75-.75Z"
                                    clip-rule="evenodd" />
                            </svg>
                        </figure>
                        <figure
                            class="flex shrink-0 items-center justify-center transition-all rounded-full bg-slate-200 p-1.5 shadow-[0_2px_10px_0px_rgba(0,0,0,0.05)] group-open:hidden">
                            <svg class="h-5 text-slate-600" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"
                                fill="currentColor" aria-hidden="true" data-slot="icon">
                                <path fill-rule="evenodd"
                                    d="M12 3.75a.75.75 0 0 1 .75.75v6.75h6.75a.75.75 0 0 1 0 1.5h-6.75v6.75a.75.75 0 0 1-1.5 0v-6.75H4.5a.75.75 0 0 1 0-1.5h6.75V4.5a.75.75 0 0 1 .75-.75Z"
                                    clip-rule="evenodd" />
                            </svg>
                        </figure>
                    </summary>
                    <div class="px-4 pb-4">
                        <p v-for="(paragraph, pIndex) in faq.answer" :key="pIndex" class="text-neutral-500"
                            :class="{ 'mt-2': pIndex > 0 }">
                            {{ paragraph }}
                        </p>
                    </div>
                </details>
            </div>
        </div>
    </section>
</template>

<script setup lang="ts">
import { ref } from 'vue'

// Type definitions
interface Header {
    badge: string
    title: string
    description: string
}

interface FAQ {
    question: string
    answer: string[]
}

// Reactive data
const header = ref<Header>({
    badge: 'Introducing PromptEdit.com',
    title: 'Frequently Asked Questions',
    description: 'Here are some of the most common questions about PromptEdit.com. If you have any other questions, feel free to reach out to our support team!'
})

const faqs = ref<FAQ[]>([
    {
        question: 'What is PromptEdit.com?',
        answer: [
            'Think of PromptEdit like a "grocery store for AI tools"',
            'PromptEdit allows you to access all of your favorite AI tools in one place, WITHOUT having to subscribe to each tool individually.',
            'You "pay" for the AI tools by simply purchasing and using credits. No subscription required, just pay for what you use.',
            'Any time new, revolutionary AI tools come out, we make sure to add them to our site, so you can use them'
        ]
    },
    {
        question: 'Can I use what I create for social media or commercial videos?',
        answer: [
            'Absolutely!',
            'Everything you create or download during your active membership is cleared for use in all commercial projects! You pay one fee for everything, we do not charge extra for commercial licensing.'
        ]
    },
    {
        question: 'Is there a difference in quality between AI tools on PromptEdit.com and the same tool on the companies main website?',
        answer: [
            'There is no quality difference whatsoever. By using PromptEdit.com you are simply accessing the same tool on a "pay-per-use" basis compared to paying through a subscription on the tool\'s main site.'
        ]
    },
    {
        question: 'Do any limits apply to downloads?',
        answer: [
            'No limits apply to downloads!',
            'With your one login you get unlimited downloads of all the templates on the site.',
            'However, per our User Terms and Privacy Policy, please remember:',
            'The subscription is for an individual.',
            'No robots allowed. So that means no sharing of accounts or use of automated tools to scrape and download items.'
        ]
    },
    {
        question: 'Will the templates work in my editing platform?',
        answer: [
            'Yes, the templates on Content Creator Templates are compatible with all video editing platforms. This means you can download them and use in whatever program you already have.',
            'That being said, there are some custom templates made for specific video editing platforms as well.'
        ]
    }
])


</script>

<style scoped>
/* Add any component-specific styles here */
details summary::-webkit-details-marker {
    display: none;
}

details>summary {
    list-style: none;
}
</style>
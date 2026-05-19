<template>
    <section class="pt-12 lg:pt-16 pb-12 lg:pb-16">
        <div class="max-w-7xl mx-auto px-4 xl:px-0">
            <div class="flex flex-col">
                <div
                    class="flex flex-col items-start sm:items-center sm:text-center md:px-4 lg:items-start lg:px-8 lg:text-left">
                    <div
                        class="items-center justify-center rounded-full text-sm font-medium whitespace-nowrap shadow-[0_2px_10px_0px_rgba(0,0,0,0.15)] inline-flex bg-white text-neutral-700 px-2.5 py-1">
                        {{ header.badge }}
                    </div>
                    <div
                        class="mt-8 bg-gradient-to-b from-slate-800 to-slate-600 bg-clip-text text-3xl font-semibold text-transparent sm:w-4/5 md:w-3/5 lg:mt-9 lg:w-11/12 lg:text-4xl lg:leading-tight">
                        {{ header.title }}
                    </div>
                    <p
                        class="text-sm font-medium text-slate-600 leading-normal lg:leading-normal lg:text-base mt-4 sm:w-2/3 md:w-1/2 xl:w-1/2">
                        {{ header.subtitle }}
                    </p>
                </div>
                <div class="mt-6 w-full border-b border-b-neutral-100 lg:mt-12"></div>
                <div
                    class="mt-6 grid w-full gap-y-4 sm:mx-auto sm:w-2/3 md:w-1/2 md:px-4 lg:mx-0 lg:mt-12 lg:w-full lg:grid-cols-3 lg:gap-x-4 lg:gap-y-0 lg:px-8 xl:gap-x-8">

                    <!-- Credit Plan Card -->
                    <div v-for="plan in pricingPlans" :key="plan.id"
                        :class="['flex flex-col rounded-2xl border border-neutral-200 bg-neutral-100 p-4 xl:p-6', plan.isPopular ? 'shadow-[0_0px_0px_2px_rgba(15,23,42,0.25),0_2px_10px_3px_rgba(0,0,0,0.05)]' : '']">
                        <div class="flex flex-col">
                            <div class="flex items-center justify-between">
                                <div class="text-lg font-medium text-neutral-700">{{ plan.name }}</div>
                                <div v-if="plan.isPopular"
                                    class="items-center justify-center rounded-full text-sm font-medium whitespace-nowrap shadow-[0_2px_10px_0px_rgba(0,0,0,0.15)] inline-flex bg-slate-900 text-white px-2 py-0.5">
                                    most popular
                                </div>
                            </div>

                            <div class="mt-6 flex items-end gap-x-3">
                                <div class="text-4xl font-semibold text-slate-900">{{ formatPrice(plan.price) }}</div>
                                <span class="text-lg text-slate-600">{{ plan.period }}</span>
                            </div>

                            <p class="mt-2 text-lg font-semibold text-neutral-700">
                                {{ plan.mainBenefit }}
                            </p>

                            <p v-if="plan.savingsText" class="mt-2 text-sm font-medium text-green-600">
                                {{ plan.savingsText }}
                            </p>

                            <p class="mt-4 font-medium text-neutral-500">
                                {{ plan.description }}
                            </p>

                            <!-- Tools List -->
                            <ul v-if="plan.tools" class="mt-4 flex flex-wrap gap-x-3 gap-y-2">
                                <li v-for="tool in plan.tools" :key="tool"
                                    class="rounded-full bg-neutral-200 px-3 py-1 text-xs font-medium text-neutral-700">
                                    {{ tool }}
                                </li>
                            </ul>

                            <!-- Features List -->
                            <ul v-if="plan.features" class="mt-4 space-y-2">
                                <li v-for="feature in plan.features" :key="feature"
                                    class="flex items-center gap-x-2 text-sm text-neutral-600">
                                    <svg class="h-4 w-4 text-green-500 flex-shrink-0" fill="none" stroke="currentColor"
                                        viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                            d="M5 13l4 4L19 7" />
                                    </svg>
                                    {{ feature }}
                                </li>
                            </ul>

                            <!-- Bonus Section -->
                            <div v-if="plan.bonus" class="mt-6 rounded-lg bg-neutral-200/50 p-4">
                                <p class="text-sm font-medium text-neutral-800">{{ plan.bonus.mainText }}</p>
                                <p v-if="plan.bonus.subText" class="mt-3 text-sm font-medium text-neutral-800">
                                    {{ plan.bonus.subText }}</p>
                                <ul v-if="plan.bonus.items" class="mt-2 space-y-1">
                                    <li v-for="item in plan.bonus.items" :key="item"
                                        class="flex items-center gap-x-2 text-sm text-neutral-600">
                                        <svg class="h-4 w-4 text-green-500 flex-shrink-0" fill="none"
                                            stroke="currentColor" viewBox="0 0 24 24">
                                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                                d="M5 13l4 4L19 7" />
                                        </svg>
                                        {{ item }}
                                    </li>
                                </ul>
                            </div>

                            <p v-if="plan.footerNote" class="mt-4 text-xs italic text-neutral-400">
                                {{ plan.footerNote }}
                            </p>
                        </div>

                        <div class="mt-6 flex grow flex-col justify-end">
                            <button @click="handlePurchase(plan)"
                                :class="['items-center justify-center whitespace-nowrap text-sm font-medium transition-all px-5 py-3 rounded-xl flex',
                                    plan.primaryButtonClass || 'border border-slate-900/5 bg-neutral-50 text-slate-700 hover:border-slate-100 hover:bg-slate-50']">
                                {{ plan.buttonText }}
                            </button>
                            <p v-if="plan.buttonNote" class="mt-3 text-xs font-medium text-neutral-400">
                                {{ plan.buttonNote }}
                            </p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<script setup lang="ts">
import { ref } from 'vue'

// Type definitions
interface Bonus {
    mainText: string
    subText?: string
    items?: string[]
}

interface PricingPlan {
    id: number
    name: string
    price: number
    period: string
    mainBenefit: string
    savingsText?: string
    description: string
    tools?: string[]
    features?: string[]
    bonus?: Bonus
    footerNote?: string
    buttonText: string
    buttonNote?: string
    primaryButtonClass?: string
    isPopular?: boolean
}

interface Header {
    badge: string
    title: string
    subtitle: string
}

// Reactive data
const header = ref<Header>({
    badge: 'Get full access',
    title: 'A Subscription to PromptEdit.com, which includes the Content Creator Templates Library is for you',
    subtitle: 'Existing Student Discount'
})

const pricingPlans = ref<PricingPlan[]>([
    {
        id: 1,
        name: 'Save on Credits',
        price: 98,
        period: 'one time',
        mainBenefit: 'Get $110 Worth of AI Credits Today',
        savingsText: 'Save 10% when you claim offer.',
        description: 'Use your credits on any AI tool across the entire site!',
        tools: ['Nano Banana Pro', 'Grok', 'Seedance', 'Kling', 'Veo', 'Heygen', 'Eleven labs', 'Suno', 'Ideogram'],
        footerNote: 'If you run out of credits, you can simply purchase more, no subscriptions required',
        buttonText: 'Claim Offer',
        primaryButtonClass: 'focus:shadow-[0_0px_0px_2px_rgba(15,23,42,0.25),0_2px_10px_0px_rgba(0,0,0,0.05)] shadow-[0_2px_10px_0px_rgba(0,0,0,0.05)] focus:bg-white focus:border-slate-50 border border-slate-900/5 bg-neutral-50 text-slate-700 hover:border-slate-100 hover:bg-slate-50'
    },
    {
        id: 2,
        name: 'Save on Everything',
        price: 39,
        period: '/ month',
        mainBenefit: 'Get $49 Worth of AI Credits every month',
        savingsText: '+ 10% off anytime you purchase more credits',
        description: 'Use your credits on any AI tool across the entire site!',
        isPopular: true,
        bonus: {
            mainText: 'Get a lifetime 20% boost on monthly credits and save 10% anytime you purchase additional credits.',
            subText: 'You also get access to some huge bonuses:',
            items: [
                'Access our Content Creator Templates Library',
                'Faster generation speeds',
                'Run multiple generations at once'
            ]
        },
        buttonText: 'Subscribe Now',
        buttonNote: '*cancel anytime, no questions asked',
        primaryButtonClass: 'bg-slate-900 text-white hover:bg-slate-800 shadow-[0_2px_10px_0px_rgba(0,0,0,0.05)]'
    }
])

// Methods
const formatPrice = (price: number): string => {
    return `$${price}`
}

const handlePurchase = (plan: PricingPlan) => {
    // Log the purchase attempt
    console.log('Purchasing plan:', plan)
    // Add your purchase logic here
}
</script>
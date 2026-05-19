<template>
    <header class="sticky top-0 z-50 py-5">
        <div class="max-w-7xl mx-auto px-4 xl:px-0 sticky top-0 z-50">
            <div
                class="bg-white flex items-center justify-between gap-x-4 rounded-2xl py-2.5 pl-5 pr-2.5 shadow-[0_2px_10px_0px_rgba(0,0,0,0.15)] lg:grid lg:grid-cols-[1fr_auto_1fr] lg:justify-stretch lg:gap-x-12 lg:rounded-[1.375rem]">

                <!-- Logo Section -->
                <div class="flex items-center gap-x-10">
                    <a href="/" :title="logo.title">
                        <img class="h-8" :src="logo.url" :alt="logo.alt" />
                    </a>
                    <span class="hidden h-4 w-px bg-neutral-300 lg:block"></span>
                </div>

                <!-- Navigation Menu -->
                <nav class="hidden lg:block">
                    <ul class="flex items-center">
                        <li v-for="item in navItems" :key="item.text">
                            <a :href="item.href" :title="item.title"
                                class="px-3 py-2 text-sm font-medium text-neutral-700 transition hover:text-neutral-600"
                                @click="handleNavClick(item)">
                                {{ item.text }}
                            </a>
                        </li>
                    </ul>
                </nav>

                <!-- Action Buttons -->
                <div class="flex items-center gap-x-10 justify-self-end">
                    <span class="hidden h-4 w-[1px] bg-neutral-300 lg:block"></span>
                    <div class="flex items-center gap-x-3 lg:gap-x-3 lg:mr-5">
                        <a :href="ctaButton.href" :title="ctaButton.title" :class="ctaButton.class"
                            @click="handleCTAClick">
                            {{ ctaButton.text }}
                            <span v-if="ctaButton.subtext" class="ml-1" :class="ctaButton.subtextClass">
                                {{ ctaButton.subtext }}
                            </span>
                        </a>

                        <!-- Mobile Menu Button -->
                        <button type="button" aria-label="Open menu" class="lg:hidden" :title="mobileMenuButton.title"
                            @click="toggleMobileMenu">
                            <svg class="h-6 text-slate-500" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"
                                fill="currentColor">
                                <path fill-rule="evenodd"
                                    d="M3 9a.75.75 0 0 1 .75-.75h16.5a.75.75 0 0 1 0 1.5H3.75A.75.75 0 0 1 3 9Zm0 6.75a.75.75 0 0 1 .75-.75h16.5a.75.75 0 0 1 0 1.5H3.75a.75.75 0 0 1-.75-.75Z"
                                    clip-rule="evenodd" />
                            </svg>
                        </button>
                    </div>
                </div>
            </div>
        </div>

        <!-- Mobile Menu -->
        <transition name="mobile-menu">
            <div v-if="isMobileMenuOpen" class="fixed inset-0 z-40 bg-white lg:hidden" @click.self="closeMobileMenu">
                <div class="flex flex-col h-full pt-20 pb-6 px-6">
                    <nav class="flex-1">
                        <ul class="space-y-4">
                            <li v-for="item in navItems" :key="item.text">
                                <a :href="item.href" :title="item.title"
                                    class="block py-2 text-lg font-medium text-neutral-700 hover:text-neutral-600"
                                    @click="handleMobileNavClick(item)">
                                    {{ item.text }}
                                </a>
                            </li>
                        </ul>
                    </nav>
                </div>
                <button @click="closeMobileMenu" class="absolute top-5 right-5 p-2" aria-label="Close menu">
                    <svg class="h-6 w-6 text-slate-500" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                            d="M6 18L18 6M6 6l12 12" />
                    </svg>
                </button>
            </div>
        </transition>
    </header>
</template>

<script setup lang="ts">
import { ref } from 'vue'

// Type definitions
interface Logo {
    url: string
    alt: string
    title: string
}

interface NavItem {
    text: string
    href: string
    title: string
}

interface Button {
    text: string
    href: string
    title: string
    class?: string
    subtext?: string
    subtextClass?: string
}

interface MobileMenuButton {
    title: string
}

// Emits for parent communication
const emit = defineEmits<{
    (e: 'nav-click', item: NavItem): void
    (e: 'cta-click'): void
    (e: 'mobile-menu-toggle', isOpen: boolean): void
}>()

// Reactive data
const logo = ref<Logo>({
    url: 'https://tailkits.com/ui/iframe/assets/img/logo.svg',
    alt: 'Logo',
    title: 'Home'
})

const navItems = ref<NavItem[]>([
    { text: 'Features', href: '#', title: 'Features' },
    { text: 'Assets', href: '#', title: 'Assets' },
    { text: 'FAQs', href: '#', title: 'FAQs' },
    { text: 'Pricing', href: '#', title: 'Pricing' }
])

const ctaButton = ref<Button>({
    text: 'Log In',
    href: '#',
    title: 'Log In',
    subtextClass: 'text-slate-400',
    class: 'items-center justify-center whitespace-nowrap text-sm font-medium transition-all focus:shadow-[0_0px_0px_2px_rgba(15,23,42,0.25),0_2px_10px_0px_rgba(0,0,0,0.05)] shadow-[0_2px_10px_0px_rgba(0,0,0,0.05)] bg-slate-900 text-white hover:bg-slate-800 disabled:bg-slate-900/30 disabled:text-slate-50/70 px-3 py-2 rounded-[0.625rem] flex'
})

const mobileMenuButton = ref<MobileMenuButton>({
    title: 'Open menu'
})

const isMobileMenuOpen = ref<boolean>(false)

// Methods
const toggleMobileMenu = () => {
    isMobileMenuOpen.value = !isMobileMenuOpen.value
    emit('mobile-menu-toggle', isMobileMenuOpen.value)

    // Prevent body scroll when mobile menu is open
    if (isMobileMenuOpen.value) {
        document.body.style.overflow = 'hidden'
    } else {
        document.body.style.overflow = ''
    }
}

const closeMobileMenu = () => {
    isMobileMenuOpen.value = false
    document.body.style.overflow = ''
    emit('mobile-menu-toggle', false)
}

const handleNavClick = (item: NavItem) => {
    console.log('Navigation clicked:', item.text)
    emit('nav-click', item)
}

const handleMobileNavClick = (item: NavItem) => {
    handleNavClick(item)
    closeMobileMenu()
}

const handleCTAClick = () => {
    console.log('CTA button clicked')
    emit('cta-click')
}

// You can also add methods to update nav items dynamically
const updateNavItems = (newItems: NavItem[]) => {
    navItems.value = newItems
}

// Expose methods for parent component if needed
defineExpose({
    closeMobileMenu,
    updateNavItems
})
</script>

<style scoped>
.mobile-menu-enter-active,
.mobile-menu-leave-active {
    transition: transform 0.3s ease, opacity 0.3s ease;
}

.mobile-menu-enter-from,
.mobile-menu-leave-to {
    transform: translateX(100%);
    opacity: 0;
}

.mobile-menu-enter-to,
.mobile-menu-leave-from {
    transform: translateX(0);
    opacity: 1;
}
</style>
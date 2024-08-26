<template>
    <AuthenticatedLayout :user="auth.user">
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 dark:text-gray-200 leading-tight">
                {{ feature.name }}
            </h2>
        </template>

        <Head :title="feature.name" />

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div v-if="answer !== null" class="mb-3 py-3 px-5 rounded text-white bg-emerald-600 text-xl">
                    Result of calculation: {{ answer }}
                </div>
                <div class="bg-white dark:bg-gray-800 overflow-hidden shadow-sm sm:rounded-lg relative">
                    <div v-if="availableCredits !== null && feature.required_credits > availableCredits"
                         class="absolute left-0 top-0 right-0 bottom-0 z-20 flex flex-col items-center justify-center bg-white/70 gap-3">
                        <svg xmlns="http://www.w3.org/2000/svg"
                             fill="none"
                             viewBox="0 0 24 24"
                             stroke-width="1.5"
                             stroke="currentColor"
                             class="size-6">
                            <path stroke-linecap="round"
                                  stroke-linejoin="round"
                                  d="M16.5 10.5V6.75a4.5 4.5 0 1 0-9 0v3.75m-.75 11.25h10.5a2.25 2.25 0 0 0 2.25-2.25v-6.75a2.25 2.25 0 0 0-2.25-2.25H6.75a2.25 2.25 0 0 0-2.25 2.25v6.75a2.25 2.25 0 0 0 2.25 2.25Z" />
                        </svg>
                        <div>
                            You don't have enough credits for this feature. Go
                            <Link :href="route('/')" class="underline"> // Replace route later with credit.index
                                buy more credits
                            </Link>
                        </div>
                    </div>
                    <div class="p-8 text-gray-400 border-b pb-4">
                        <p>{{ feature.description }}</p>
                        <p class="text-sm italic text-right">
                            Requires {{ feature.required_credits }} credits
                        </p>
                    </div>
                    <slot />
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>

<script setup>
import { usePage, Link, Head } from '@inertiajs/vue3';
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';

const props = defineProps({
    feature: Object,
    answer: [String, Number, null],
});

const { auth } = usePage().props;
const availableCredits = auth.user.available_credits;
</script>

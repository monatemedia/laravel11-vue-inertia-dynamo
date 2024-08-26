<template>
    <Feature :feature="feature" :answer="answer">
        <form @submit.prevent="submit" class="p-8 grid grid-cols-2 gap-3">
            <div>
                <InputLabel for="number1" :value="'Number 1'" />

                <TextInput
                    id="number1"
                    type="text"
                    name="number1"
                    v-model="data.number1"
                    class="mt-1 block w-full"
                />

                <InputError :message="errors.number1" class="mt-2" />
            </div>
            <div>
                <InputLabel for="number2" :value="'Number 2'" />

                <TextInput
                    id="number2"
                    type="text"
                    name="number2"
                    v-model="data.number2"
                    class="mt-1 block w-full"
                />

                <InputError :message="errors.number2" class="mt-2" />
            </div>
            <div class="flex items-center justify-end mt-4 col-span-2">
                <PrimaryButton class="ms-4" :disabled="processing">
                    Calculate
                </PrimaryButton>
            </div>
        </form>
    </Feature>
</template>

<script setup>
import { ref } from 'vue';
import { useForm } from '@inertiajs/vue3';
import Feature from '@/Components/Feature.vue';
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import TextInput from '@/Components/TextInput.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';

const props = defineProps({
    feature: Object,
    answer: [String, Number, null],
});

const { data, setData, post, reset, errors, processing } = useForm({
    number1: '',
    number2: '',
});

const submit = () => {
    post(route('feature1.calculate'), {
        onSuccess: () => reset(),
    });
};
</script>

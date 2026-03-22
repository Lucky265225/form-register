<script setup>

const data = defineProps({
    label: String,
    type: String,
    data: Array,
    error: [String,Boolean],
    modelValue: String
})

const emit = defineEmits(["update:modelValue"])

</script>

<template>

    <div class="flex flex-col space-y-2">
        <label class="font-bold">{{ data.label }}<span class="text-red-500"> *</span></label>
        <div class="flex space-x-5">
            <div v-for="option in data.data" tabindex="0" class="flex flex-col border space-y-2 border-gray-300 py-1 px-2 rounded-lg 
            focus:border-3 focus:border-blue-500 focus:bg-blue-50"
            @click="emit('update:modelValue', option.value)">
                <div class="flex space-x-2 justify-between">
                    <label :for="option.label">{{ option.label }}</label>
                    <input :type="data.type" :id="option.label" :value="option.value" class="accent-blue-500"
                        :checked="modelValue === option.value"
                        @click.stop
                        @change="emit('update:modelValue', option.value)">
                </div>
                <p class="text-gray-500">{{ option.desc }}</p>
            </div>
        </div>
        <p v-if="error" class="text-red-500">{{ error }}</p>
    </div>
    
</template>

<style scoped></style>
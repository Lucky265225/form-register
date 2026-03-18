<script setup>

const data = defineProps({
    label: String,
    type: String,
    desc: String,
    data: Array,
    modelValue: String
})

const emit = defineEmits(["update:modelValue"])

</script>

<template>

    <div class="flex flex-col space-y-2">
        <label class="font-bold">{{ data.label }}</label>
        <div class="flex space-x-5">
            <div v-for="option in data.data" class="flex space-x-2 border border-gray-300 py-1 px-2 rounded-lg">
                <input :type="data.type" :id="option.label" :value="option.value"
                    :checked="modelValue === option.value"
                    @change="emit('update:modelValue', option.value)">
                <label :for="option.label">{{ option.label }}</label>
            </div>
        </div>
    </div>
    
</template>

<style scoped></style>
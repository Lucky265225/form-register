<script setup>

const data = defineProps({
    label: String,
    type: String,
    desc: String,
    modelValue: String
})

const emit = defineEmits(["update:modelValue"])

</script>

<template>

    <div class="flex flex-col space-y-2">
        <label for="fullname" class="font-bold">{{ data.label }}</label>
        <textarea name="" id="" :placeholder="desc"
        :value="modelValue"
        @input="emit('update:modelValue', $event.target.value)"
        class="border border-gray-300 rounded-md py-1 px-3 h-32"
        ></textarea>
        <p class="text-gray-500">Optional: briefly describe your interests or previous experience.</p>
    </div>
    
</template>

<style scoped></style>
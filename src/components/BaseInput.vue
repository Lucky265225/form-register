<script setup>

const data = defineProps({
    label: String,
    type: String,
    desc: String,
    error: String,
    modelValue: String
})

const emit = defineEmits(["update:modelValue"])

</script>

<template>

    <div class="flex flex-col space-y-2">
        <label for="fullname" class="font-bold">{{ data.label }}</label>
        <input :type="data.type" name="" id="fullname" :placeholder="desc"
        :value="modelValue"
        @input="emit('update:modelValue', $event.target.value)"
        class="border border-gray-300 rounded-md py-1 px-3"
        :class=" error ? 'border-red-500' : ''">
        <p v-if="error" class="text-red-500">{{ error }}</p>
    </div>
    
</template>

<style scoped></style>
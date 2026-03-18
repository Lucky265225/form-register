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
        <label for="fullname" class="font-bold">{{ data.label }}</label>
        <select name="" id=""
        :value="modelValue"
        @change="emit('update:modelValue', $event.target.value)"
        class="border border-gray-300 rounded-md py-1 px-3">
            <option disabled value="">{{ data.desc }}</option>
            <option v-for="option in data.data" :value="option.value">{{ option.label }}</option>
        </select>
    </div>
    
</template>

<style scoped></style>
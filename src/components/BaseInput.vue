<script setup>

const data = defineProps({
    label: String,
    type: String,
    desc: String
})

</script>

<template>

    <div class="flex flex-col space-y-2">
        <label for="fullname" class="font-bold">{{ data.label }}</label>
        <input :type="data.type" name="" id="fullname" :placeholder="desc" 
        class="border border-gray-300 rounded-md py-1 px-3">
    </div>
    
</template>

<style scoped></style>
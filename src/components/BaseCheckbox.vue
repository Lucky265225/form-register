<script setup>

const props = defineProps({
  modelValue: Boolean
})

const emit = defineEmits(["update:modelValue"])

</script>

<template>

    <div class="flex space-x-3">
        <input class="accent-blue-500"
            id="agree"  
            type="checkbox"
            :checked="modelValue"
            @change="emit('update:modelValue', $event.target.checked)"/>
        <label for="agree">I comfirm that the informatiom provided is correct and I agree to participate in the workshop activities.</label>
    </div>
    
</template>

<style scoped></style>
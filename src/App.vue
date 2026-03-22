<script setup>
import { computed, reactive, ref } from "vue";
import BaseInput from "./components/BaseInput.vue";
import BaseCheckbox from "./components/BaseCheckbox.vue";
import BaseRadioGroup from "./components/BaseRadioGroup.vue";
import BaseSelect from "./components/BaseSelect.vue";
import BaseTextarea from "./components/BaseTextarea.vue";


const form = reactive({
  fullName: "",
  studentId: "",
  email: "",
  password: "",
  program: "",
  yearLevel: "",
  bio: "",
  track: "",
  agree: false,
})

const submitted = ref(false)

const programOptions = [
  { label: "Computer Science", value: "CS" },
  { label: "Digital Service Innovation", value: "DSI" },
  { label: "Information Technology", value: "IT" },
  { label: "Software Engineering", value: "SE" },
]

const trackOptions = [
  { label: "Frontend UI Development", value: "frontend" },
  { label: "Backend API Design", value: "backend" },
  { label: "UX/UI Design", value: "ux" },
  { label: "AI for Productivity", value: "ai" },
]

const yearOptions = [
  { label: "Year 1", value: "1", desc: "Beginner student level"},
  { label: "Year 2", value: "2", desc: "intermidate foundation" },
  { label: "Year 3", value: "3", desc: "Project-focused stage" },
  { label: "Year 4", value: "4", desc: "internship or capstone stage" },
]

const errors = computed(() => {
  const e = {}

  if (!form.fullName.trim()) e.fullName = "Full name is required."

  if (!form.studentId.trim()) {
    e.studentId = "Student ID is required."
  } else if (!/^\d{11}$/.test(form.studentId)) {
    e.studentId = "Student ID must be 11 digits."
  }

  if (!form.email.trim()) {
    e.email = "Email is required."
  } else if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(form.email)) {
    e.email = "Please enter a valid email address."
  }

  if (!form.password.trim()) {
    e.password = "Password is required."
  } else if (form.password.length < 8) {
    e.password = "Password must be at least 8 characters."
  }

  if (!form.program) e.program = "Please select your program."
  if (!form.yearLevel) e.yearLevel = "Please select your year level."
  if (!form.track) e.track = "Please choose a workshop track."
  if (!form.agree) e.agree = "You must accept the terms before submitting."

  return e
})

const isFormValid = computed(() => Object.keys(errors.value).length === 0)

function handleSubmit() {
  console.log(form);
  console.log(errors);
  
  
  submitted.value = true

  if (!isFormValid.value) return

  showAlert.value = true

  form.fullName = ""
  form.studentId = ""
  form.email = ""
  form.password = ""
  form.program = ""
  form.yearLevel = ""
  form.bio = ""
  form.track = ""
  form.agree = false
  submitted.value = false
}

function handleReset() {
  submitted.value = false 

  form.fullName = ""
  form.studentId = ""
  form.email = ""
  form.password = ""
  form.program = ""
  form.yearLevel = ""
  form.bio = ""
  form.track = ""
  form.agree = false
}

const showAlert = ref(false)

function handleClose() {
  showAlert.value = false
}
</script>

<template>
  
  <div class="h-min-screen p-10">
    <!-- header -->
    <div class="mb-10">
      <h4 class="text-blue-500 text-md font-medium">Hands-on Lab</h4>
      <h2 class="font-bold text-2xl">Student Workshop Registration Form</h2>
      <p>Practice styling form controls, focus states, and validation feedback with Vue.js and Tailwind CSS.</p>
    </div>

    <!-- form -->
    <div>
      <form @submit.prevent="handleSubmit">

        <div class="grid grid-cols-2 gap-x-5 gap-y-5 mb-10">
          <BaseInput v-model="form.fullName" label="Full Name" type="text" desc="Enter your full name" :error="submitted && errors.fullName"/>
          <BaseInput v-model="form.studentId" label="Student ID" type="tel" desc="e.g. 6601234567" :error="submitted && errors.studentId"/>
          <BaseInput v-model="form.email" label="Email" type="email" desc="yourname@example.com" :error="submitted && errors.email"/>
          <BaseInput v-model="form.password" label="Password" type="password" desc="At least 8 characters" :error="submitted && errors.password"/>
          <BaseSelect v-model="form.program" label="Program / Major" desc="Select your program" :data="programOptions" :error="submitted && errors.program"/>
          <BaseSelect v-model="form.track" label="Workshop Track" desc="Select a track" :data="trackOptions" :error="submitted && errors.track"/>
        </div>

        <div class="mb-10">
          <BaseTextarea v-model="form.bio" label="Short Bio" desc="Tell us about your interests..." />
        </div>

        <div class="mb-10">
          <BaseRadioGroup v-model="form.yearLevel" label="Year Level" type="radio" :data="yearOptions" :error="submitted && errors.yearLevel"/>
        </div>

        <div class="mb-10">
          <BaseCheckbox v-model="form.agree"/>
        </div>
        
        <div class="flex justify-between border-t border-gray-300 pt-10">
          <p><span class="font-medium">Tip: </span><span class="text-gray-500">Try submitting the form with missing fields to see validation feedback.</span></p>
          <div class="flex space-x-10">
            <button @click="handleReset" class="font-medium text-md py-2 px-3 rounded-xl border border-gray-300">Reset Form</button>
            <button type="submit" :disabled="!form.agree"
            :class=" !form.agree ? 'bg-gray-300' : ''"
            class="font-bold text-xl py-2 px-3 rounded-xl bg-blue-600 text-white">Submit Registration</button>
          </div>
        </div>
      </form>
    </div>

    <!-- alert -->
    <div v-if="showAlert" class="fixed inset-0 flex items-center justify-center bg-gray-500/20">
      <div class="bg-white p-5 rounded-2xl shadow-lg">
        <h2 class="text-xl font-bold">Registration Submitted</h2>
        <p class="text-gray-500 text-sm">Your workshop registration has been recorded successfully.</p>
        <button @click="handleClose" class="mt-4 px-4 py-2 bg-green-500 text-white rounded-lg">Close</button>
      </div>
    </div>
  </div>

</template>

<style scoped></style>

<template>
  <Motion
    tag="form"
    class="space-y-6 bg-white dark:bg-neutral-900 p-8 rounded-2xl shadow-xl"
    :initial="{ opacity: 0, y: 40 }"
    :while-in-view="{ opacity: 1, y: 0 }"
    :transition="{ duration: 0.8, ease: 'easeOut' }"
    @submit.prevent="handleSubmit"
  >
    <div v-for="input in fields" :key="input.name">
      <label
        :for="input.name"
        class="ml-2 mb-1 block text-sm font-medium text-gray-700 dark:text-gray-300"
      >
        {{ input.label }}
      </label>
      <Motion
        :initial="{ opacity: 0, y: 20 }"
        :while-in-view="{ opacity: 1, y: 0 }"
        :transition="{ delay: 0.1 * index, duration: 0.5 }"
      >
        <IInput
          v-model="form[input.name]"
          :id="input.name"
          variant="hover"
          :type="input.type"
          :placeholder="input.placeholder"
          container-class="w-full"
        />
      </Motion>
    </div>

    <div>
      <label
        for="message"
        class="ml-2 mb-1 block text-sm font-medium text-gray-700 dark:text-gray-300"
      >
        Your Message
      </label>
      <textarea
        v-model="form.message"
        rows="4"
        class="w-full rounded-lg border border-gray-300 bg-transparent px-4 py-3 text-sm text-gray-800 dark:text-white dark:border-gray-600 focus:border-green-500 focus:ring-green-500"
        placeholder="Type your message here..."
        required
      ></textarea>
    </div>

    <button
      type="submit"
      class="inline-flex items-center justify-center rounded-lg bg-green-600 px-6 py-3 text-sm font-semibold text-white transition hover:bg-green-700"
    >
      Send Message ✉️
    </button>
  </Motion>
</template>

<script setup lang="ts">
import { Motion } from "motion-v";
import { IInput } from "@/components/ui/input";
import { reactive } from "vue";

const form: { name: string; email: string; phone: string; message: string } =
  reactive({
    name: "",
    email: "",
    phone: "",
    message: "",
  });

const fields = [
  { label: "Your Name", name: "name", type: "text" },
  { label: "Your Email", name: "email", type: "email" },
  { label: "Phone Number", name: "phone", type: "tel" },
];

const handleSubmit = () => {
  console.log("Form submitted:", { ...form });
  alert("Message sent! (Not yet connected to backend)");
};
</script>

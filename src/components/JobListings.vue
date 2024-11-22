<script setup lang="ts">
import { onMounted, ref } from "vue";
import JobListing from "@/components/JobListing.vue";
import axios from "axios";

interface Job {
  title: string;
  description: string;
  type: string;
  salary: string;
  location: string;
  id: number;
}

defineProps({
  limit: Number,
  showButton: {
    type: Boolean,
    default: false,
  },
});

const jobs = ref<Job[]>([]);

onMounted(async () => {
  try {
    const response = await axios.get<Job[]>("http://localhost:3001/jobs");
    jobs.value = response.data;
  } catch (e) {
    console.error("Error fetching jobs", e);
  }
});
</script>

<template>
  <section class="bg-green-50 px-4 py-10">
    <div class="container-xl lg:container m-auto">
      <h2 class="text-3xl font-bold text-green-500 mb-6 text-center">Browse Jobs</h2>
      <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
        <!-- Job Listings -->
        <JobListing v-for="job in jobs.slice(0, limit || jobs.length)" :key="job.id" :job="job" />
      </div>
    </div>
  </section>

  <section v-if="showButton" class="m-auto max-w-lg my-10 px-6">
    <RouterLink
      to="/jobs"
      class="block bg-black text-white text-center py-4 px-6 rounded-xl hover:bg-gray-700"
      >View All Jobs</RouterLink
    >
  </section>
</template>

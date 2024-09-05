<script setup lang="ts">
import { h, onMounted, ref } from "vue"

const data = ref<any>([]);

function generateRandomData(numObjects: any) {
  const statuses = ["pending", "processing", "completed"];
  const emails = [
    "example@gmail.com",
    "m@example.com",
    "test@example.com",
    "user@example.com",
  ];

  const randomData: any[] = [];

  for (let i = 0; i < numObjects; i++) {
    const id = Math.random().toString(36).substr(2, 8);
    const amount = Math.floor(Math.random() * 500) + 50; // Random amount between 50 and 550
    const status = statuses[Math.floor(Math.random() * statuses.length)];
    const email = emails[Math.floor(Math.random() * emails.length)];

    randomData.push({ id, amount, status, email });
  }

  return (data.value = randomData);
}

onMounted(() => {
    generateRandomData(100);
  });

</script>

<template>
  <div class="grid w-full gap-4">
    <header class="flex items-start justify-between">
      <div class="grow">
        <p>All your transactions</p>
        <h1>Transactions</h1>
      </div>
    </header>
    <DataTable :data="data" />
  </div>
</template>

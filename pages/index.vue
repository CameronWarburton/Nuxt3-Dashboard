<script setup>
import { Tabs, TabsContent, TabsList, TabsTrigger } from "@/components/ui/tabs";
import Chart from "~/components/Chart.vue";
const loading = ref(false);
let data = ref([]);
const list = [
  {
    title: "Today",
  },
  {
    title: "Week",
  },
  {
    title: "Month",
  },
  {
    title: "Year",
  },
];

// the current category
let currentCategory = ref("today");
// function to generate random values depending on current category
function generateRandomValue(number = 7) {
  let values = [];
  for (let j = 0; j < number + 1; j++) {
    values.push(Math.floor(Math.random() * 100));
  }
  data.value = values;
  return values;
}

// a function to catch shadcn tab change + set category
const setCategory = (e) => {
  let v = e.target.innerText.toLowerCase();
  currentCategory.value = v;
  if (v === "today") generateRandomValue(24);
  if (v === "week") generateRandomValue(6);
  if (v === "month") generateRandomValue(31);
  if (v === "year") generateRandomValue(11);
  }

onMounted(() => {
  generateRandomValue(24);
});
</script>

<template>
  <div class="grid w-full gap-4">
    <header class="flex items-start justify-between">
      <div class="grow">
        <p>Hi, Welcome back Cameron!</p>
        <h1>Dashboard</h1>
      </div>
      <div class="bg-neutral-200 h-[36px] w-[120px]"></div>
    </header>
    <main class="grid gap-4">
      <Tabs default-value="Today" @click="setCategory">
        <TabsList class="max-w-[400px]">
          <TabsTrigger
            v-for="(item, index) in list"
            :key="index"
            :value="item.title"
          >
            {{ item.title }}
          </TabsTrigger>
        </TabsList>
        <TabsContent
          class="w-[100%]"
          v-for="(item, index) in list"
          :key="index"
          :value="item.title"
        >
          <Chart
            v-if="data.length > 0"
            :currentCategory="currentCategory"
            :data="data"
          />
        </TabsContent>
      </Tabs>
    </main>
    <footer>
      <div class="flex items-center gap-4">
        <div
          v-for="(item, index) in 3"
          :key="index"
          class="w-full h-[260px] bg-neutral-200"
        ></div>
      </div>
    </footer>
  </div>
</template>

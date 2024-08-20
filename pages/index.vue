<script setup>
import { Tabs, TabsContent, TabsList, TabsTrigger } from "@/components/ui/tabs";
const loading = ref(false);
const list = [
  {
    title: "Today",
    component: resolveComponent("TabsToday"), // custom component relative to Today
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
let categories = ref({
  'today': [],
  'week': [],
  'month': [],
  'year': [],
});
let currentCategory = ref([
  "Jan",
  "Feb",
  "Mar",
  "Apr",
  "May",
  "Jun",
  "Jul",
  "Aug",
  "Sep",
  "Oct",
  "Nov",
  "Dec",
]);
const options = computed(() => ({
  chart: {
    type: "line",
    animation: {
      enable: false,
    },
  },
  title: {
    text: "",
  },
  xAxis: {
    gridLineColor: 'transparent',
    categories: currentCategory,
  },
  yAxis: {
    gridLineColor: 'transparent',
    title: {
      text: "Temperature (°C)",
    },
  },
  plotOptions: {
    line: {
      dataLabels: {
        enabled: true,
      },
      enableMouseTracking: false,
    },
  },
  series: [
    {
      name: "Reggane",
      data: [
        16.0, 18.2, 23.1, 27.9, 32.2, 36.4, 39.8, 38.4, 35.5, 29.2, 22.0, 17.8,
      ],
    },
    {
      name: "Tallinn",
      data: [
        -2.9, -3.6, -0.6, 4.8, 10.2, 14.5, 17.6, 16.5, 12.0, 6.5, 2.0, -0.9,
      ],
    },
  ],
}));
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
      <Tabs default-value="Today" class="w-[400px]">
        <TabsList>
          <TabsTrigger
            v-for="(item, index) in list"
            :key="index"
            :value="item.title"
          >
            {{ item.title }}
          </TabsTrigger>
        </TabsList>
        <TabsContent
          v-for="(item, index) in list"
          :key="index"
          :value="item.title"
        >
          <highchart :options="options" />
        </TabsContent>
      </Tabs>
      <!-- <div class="flex items-center gap-3">
        <div
          v-for="(item, index) in 3"
          :key="index"
          class="w-[120px] h-[36px] bg-neutral-200"
        ></div>
      </div>
      <section>
        <div class="w-full h-[360px] bg-neutral-200"></div>
      </section> -->
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

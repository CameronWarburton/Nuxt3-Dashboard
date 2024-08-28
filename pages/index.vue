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

// make categories
let categories = ref({
  today: [
    "00:00",
    "01:00",
    "02:00",
    "03:00",
    "04:00",
    "05:00",
    "06:00",
    "07:00",
    "08:00",
    "09:00",
    "10:00",
    "11:00",
    "12:00",
    "13:00",
    "14:00",
    "15:00",
    "16:00",
    "17:00",
    "18:00",
    "19:00",
    "20:00",
    "21:00",
    "22:00",
    "23:00",
  ],
  week: [
    "Sunday",
    "Monday",
    "Tuesday",
    "Wednesday",
    "Thursday",
    "Friday",
    "Saturday",
  ],
  year: [
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
  ],
});

// where we are going to save the data
let data = ref([]);
// the current category
let currentCategory = ref("today");

// options of the charts
const options = computed(() => ({
  chart: {
    type: "line",
    animation: {
      enable: false,
    },
  },
  legend: {
    enabled: false,
  },
  title: {
    text: "",
  },
  xAxis: {
    gridLineColor: "transparent", // remove line
    categories: categories.value[currentCategory.value],
  },
  yAxis: {
    gridLineColor: "transparent",
    title: {
      // remove title
      text: "",
    },
  },
  plotOptions: {
    line: {
      marker: {
        // remove points
        enabled: false,
      },
      dataLabels: {
        enabled: false,
      },
      enableMouseTracking: true,
    },
  },
  series: [
    {
      name: "line",
      lineWidth: "4px",
      color: {
        linearGradient: {},
        stops: [
          [0, "rgba(252, 176, 69, 1)"],
          [0.33, "rgba(253, 29, 29, 1)"],
          [0.66, "rgba(131, 58, 180, 1)"],
          [1, "rgba(29, 217, 83, 1)"],
        ],
      },
      data: data.value,
    },
  ],
}));

// function to generate current month
function generateMonth() {
  let currentDate = new Date();
  let currentMonth = currentDate.getMonth() + 1; // Current month (1 for January, 2 for February etc.)
  let currentYear = currentDate.getFullYear(); //Current year

  function generateMonthDates() {
    let monthDates = [];
    let daysInMonth = new Date(currentYear, currentMonth, 0).getDate();

    for (let i = 1; i <= daysInMonth; i++) {
      let dayString = ("0" + i).slice(-2); // Format day with 2 digits (01, 02 etc.)
      let monthString = ("0" + currentMonth).slice(-2); // Format month with two digits (01, 02, ..., 12)
      monthDates.push(monthString + "/" + dayString);
    }

    return monthDates;
  }

  let month = generateMonthDates();
  categories.value = { ...categories.value, month };
  return month;
}

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
  switch (v) {
    case "today":
      generateRandomValue(24);
      break;
    case "week":
      generateRandomValue(6);
      break;
    case "month":
      generateRandomValue(31);
      break;
    case "year":
      generateRandomValue(11);
      break;
  }
};

// on mounted we generate month and random value
onMounted(() => {
  generateMonth();
  generateRandomValue(7);
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
          <highchart v-if="data.length > 0" :options="options" />
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

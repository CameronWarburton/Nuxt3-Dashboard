<script setup>
const loading = ref(false);
import { Tabs, TabsContent, TabsList, TabsTrigger } from '@/components/ui/tabs'
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
  <Tabs default-value="today" class="w-[400px]">
    <TabsList>
      <TabsTrigger value="today">
        Today
      </TabsTrigger>
      <TabsTrigger value="week">
        This week
      </TabsTrigger>
      <TabsTrigger value="month">
        This month
      </TabsTrigger>
      <TabsTrigger value="year">
        This year
      </TabsTrigger>
    </TabsList>
    <TabsContent value="today">
      Today
    </TabsContent>
    <TabsContent value="week">
      This week
    </TabsContent>
    <TabsContent value="month">
      This month
    </TabsContent>
    <TabsContent value="year">
      This year
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

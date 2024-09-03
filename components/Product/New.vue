<script setup lang="ts">
import {
  AlertDialog,
  AlertDialogAction,
  AlertDialogCancel,
  AlertDialogContent,
  AlertDialogDescription,
  AlertDialogFooter,
  AlertDialogHeader,
  AlertDialogTitle,
  AlertDialogTrigger,
} from "@/components/ui/alert-dialog";

const loading = ref(false);

const createNewProduct = async () => {
  try {
    loading.value = true;
    // all the business logic 
  } catch (error) {

  } finally {
    loading.value = false;
  }
};
</script>

<template>
  <AlertDialog>
    <AlertDialogTrigger>
      <Button>Add a new product</Button>
    </AlertDialogTrigger>
    <AlertDialogContent>
      <AlertDialogHeader> </AlertDialogHeader>
      <AlertDialogFooter>
        <AlertDialogCancel>Cancel</AlertDialogCancel>
        <AlertDialogAction @click="createNewProduct()"
          >Create</AlertDialogAction
        >
      </AlertDialogFooter>
    </AlertDialogContent>
  </AlertDialog>
</template>

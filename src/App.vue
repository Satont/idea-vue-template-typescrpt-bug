<script setup lang="ts">
import {ref, Ref} from "vue";

type FreakyFunction<T> = () => T

const returnSomeData = (): string[] => ['hello world']

const createEvent = <F extends FreakyFunction<any>>(f: F) => {
  return {
    getAll(): Ref<ReturnType<typeof f>> {
      const dataFromFunction = f()
      const dataRef = ref(dataFromFunction)

      return dataRef
    }
  }
}

export const useTest = () => createEvent(returnSomeData)

const manager = useTest()
const data = manager.getAll()
</script>

<template>
  <div v-for="item of data" :key="item">
    {{ item }}
  </div>
</template>
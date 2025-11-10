<script setup lang="ts">
import { RouterLink } from 'vue-router'
import { supabase} from '@/lib/supabaseClient'
import { ref } from 'vue'
import type { Tables } from '../../../database/types.ts'

const tasks = ref<Tables<'tasks'>[] | null>()

;(async () => {
  const {data, error} = await supabase.from('tasks').select()
  if (error) console.error(error)
  tasks.value = data
  console.log('tasks:', tasks.value)
})()


</script>

<template>
  <div>
    <h1>Tasks Page</h1>
    <ul>
      <li v-for="task in tasks" :key="task.id">
        {{ task.name }}
      </li>
    </ul>
    <RouterLink to="/">Go to home</RouterLink>
  </div>
</template>

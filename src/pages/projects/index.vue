<script setup lang="ts">
import { RouterLink } from 'vue-router'
import { supabase} from '@/lib/supabaseClient'
import { ref } from 'vue'
import type { Tables } from '../../../database/types.ts'

const projects = ref<Tables<'projects'>[] | null>()

  ;(async () => {
  const {data, error} = await supabase.from('projects').select()
  if (error) console.error(error)
  projects.value = data
  console.log('projects:', projects.value)
})()


</script>

<template>
  <div>
    <h1>Projects Page</h1>
    <ul>
      <li v-for="project in projects" :key="project.id">
        {{ project.name }}
      </li>
    </ul>
    <RouterLink to="/">Go to home</RouterLink>
  </div>
</template>

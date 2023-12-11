<template>
    <main style="min-height: 50vh; margin-top: 2rem;">
        <div class="container">
            <div class="row">
                <div class="col-md-8 offset-md-2">
                    <!-- Add new Task -->
                    <div class="relative">
                        <input type="text" class="form-control form-control-lg padding-right-lg"
                            placeholder="+ Add new task. Press enter to save." />
                    </div>
                    <!-- List of uncomplete tasks -->
                    <Taks :tasks="uncompleteTasks"/>


                    <Taks :tasks="completeTasks"/>
                    
                </div>
            </div>
        </div>
    </main>
</template>

<script setup>

import { computed, onMounted, ref } from "vue";
import { allTasks} from "../http/task-api"

import Task from "../components/tasks/Task.vue"

import Taks from "../components/tasks/Tasks.vue"

const tasks = ref([])

onMounted(async () => {
    const { data } = await allTasks()
    tasks.value = data.data
})

const  uncompleteTasks = computed(() => tasks.value.filter(task => !task.is_completed))
const  completeTasks = computed(() => tasks.value.filter(task => task.is_completed))
</script>
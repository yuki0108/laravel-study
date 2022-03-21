<script setup>
import BreezeAuthenticatedLayout from '@/Layouts/Authenticated.vue';
import { Head } from '@inertiajs/inertia-vue3';

const tasks = [
    {
        id: 1,
        taskName: "test",
        deadLine: "3/23",
        state: 1
    },
    {
        id: 2,
        taskName: "test2",
        deadLine: "3/25",
        state: 2
    },
    {
        id: 3,
        taskName: "task3",
        deadLine: "3/29",
        state: 0
    }
]
</script>

<template>
    <Head title="Dashboard" />

    <BreezeAuthenticatedLayout>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Dashboard
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">
                    <div class="p-6 bg-white border-b border-gray-200">
                        You're logged in!!
                    </div>
                    <div>
                        +++
                        {{ tasks }}
                        ----
                        <table>
                            <thead>
                            <tr>
                                <th>ID</th>
                                <th>タスク名</th>
                                <th>期限</th>
                                <th>状態</th>
                            </tr>
                            </thead>
                            <tbody>
                            <tr v-for="task in tasks">
                                <td>{{ task.id }}</td>
                                <td>{{ task.taskName }}</td>
                                <td>{{ task.deadLine }}</td>
                                <td>{{ task.state }}</td>
                            </tr>
                            </tbody>
                        </table>
                    </div>

                </div>
            </div>
        </div>
    </BreezeAuthenticatedLayout>
</template>

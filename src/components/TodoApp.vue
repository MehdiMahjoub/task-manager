<template>
    <v-card class="mx-auto" max-width="800">
        <v-text-field v-model="newTask" label="Nouvelle tâche" @keyup.enter="addTask"></v-text-field>
        <v-btn class="mt-2" type="submit" block @click="addTask" color="primary">Ajouter</v-btn>

        <v-list>
            <v-list-subheader>Tâches</v-list-subheader>

            <v-list-item v-for="(task, index) in tasks" :key="index" :value="task">
                <template v-slot:prepend>
                    <v-list-item-action start>
                        <v-checkbox-btn v-model="task.done" @click.stop="toggleTaskStatus(task)"></v-checkbox-btn>
                    </v-list-item-action>
                </template>

                <v-list-item-content :class="{ 'done': task.done }" @click="toggleTaskStatus(task)">
                    <v-list-item-title>{{ capitalize(task.text) }}</v-list-item-title>
                </v-list-item-content>

                <template v-slot:append>
                    <v-list-item-action>
                        <v-btn @click="deleteTask(index)" icon>
                            <v-btn color="red" icon="mdi-delete"></v-btn>
                        </v-btn>
                    </v-list-item-action>
                </template>
            </v-list-item>
        </v-list>
    </v-card>

</template>

<script>
export default {
    data() {
        return {
            newTask: '',
            tasks: [],
        };
    },
    methods: {
        addTask() {
            if (this.newTask.trim() !== '') {
                this.tasks.push({ text: this.newTask, done: false });
                this.newTask = '';
            }
        },
        deleteTask(index) {
            this.tasks.splice(index, 1);
        },
        toggleTaskStatus(task) {
            task.done = !task.done;
        },
        capitalize(value) {
            if (!value) return "";
            value = value.toString();
            return value.charAt(0).toUpperCase() + value.slice(1);
        }
    }
};
</script>

<style>
.done {
    text-decoration: line-through;
}
</style>
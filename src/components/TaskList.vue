<template>
    <div class="md-layout">
        <div class="md-layout-item md-size-15"></div>
        <div class="md-layout-item md-size-70 ">
            <md-card>
                <div class="md-layout md-gutter md-alignment-center-space-around">
                    <div class="md-layout-item md-size-20">
                        <md-button class="green" @click="awesome = true">
                            Add task
                        </md-button>
                    </div>
                    <div class="md-layout-item md-size-20">
                        <md-button class="red" @click="clearAll()">
                            Remove all tasks
                        </md-button>
                    </div>
                    <div class="md-layout-item md-size-60">

                    </div>
                </div>
                <div v-if="awesome">
                <div class="md-layout md-gutter md-alignment-space-around-center">
                        <div class="md-layout-item md-size-50">
                            <md-field  md-clearable >
                                <label>Type here to create new task</label>
                                <md-input
                                        v-model="newTask"
                                        @keyup.enter="addTask">
                                </md-input>

                            </md-field>

                        </div>
                        <div class="padding-top md-layout-item md-size-20">
                            <md-button class="red" @click="awesome = false">
                                close
                            </md-button>

                        </div>
                        <div class="padding-top md-layout-item md-size-20">
                            <md-button class="green" @click="addTask(); awesome = false">
                                Add task
                            </md-button>
                        </div>
                    </div>
                </div>
                <md-card-content>
                    <div>
                        <md-table v-model="searched" md-sort="title" md-sort-order="asc" md-card md-fixed-header>
                            <md-table-toolbar>
                                <div class="md-toolbar-section-start">
                                    <h1 class="md-title">TODOS</h1>
                                </div>

                                <md-field md-clearable class="md-toolbar-section-end">
                                    <md-input placeholder="Search..." v-model="search" />
                                </md-field>
                            </md-table-toolbar>

                            <md-table-empty-state
                                    md-label="No users found"
                                    :md-description="`No TODOS found for this '${search}' query. Try a different search term or create a new user.`">

                            </md-table-empty-state>

                            <md-table-row slot="md-table-row" slot-scope="{ item }">
                                <md-table-cell md-label="title" md-sort-by="title">
                                    <div class="md-layout md-gutter md-alignment-center-space-around">
                                        <div class="md-layout-item  md-size-70" >
                                            <md-field>
                                                <md-textarea :disabled="readonly"  v-model="item.title"></md-textarea>
                                            </md-field>
                                        </div>


                                        <div class="md-layout-item md-size-15 padding-bot">
                                            <md-button v-if="readonly" class="orange" @click="readonly = false">Edit</md-button>
                                            <md-button  class=" orange" v-else @click="readonly = true">Save</md-button>
                                        </div>
                                        <div class="md-layout-item md-size-15 padding-bot">
                                            <md-button @click="removeTask" class="red">Remove</md-button>
                                        </div>
                                    </div>
                                </md-table-cell>

                            </md-table-row>
                        </md-table>
                    </div>
                </md-card-content>
            </md-card>
        </div>
    </div>
</template>
<script>
    const toLower = text => {
        return text.toString().toLowerCase()
    }

    const searchByName = (items, term) => {
        if (term) {
            return items.filter(item => toLower(item.title).includes(toLower(term)))
        }

        return items
    }

    export default {
        name: "TaskList",
        components: {
        },
        data() {
            return {
                tasks: [
                    {
                        title: 'Make todo list',
                        completed: true
                    },
                    {
                        title: 'Go skydiving',
                        completed: false
                    }
                ],
                readonly: false,
                search: null,
                awesome: true,
                newTask: ''
            };
        },
        computed: {
            searched(){
                return searchByName(this.tasks, this.search);
            },
            incomplete() {
                return this.tasks.filter(this.inProgress).length;
            }
        },
        methods: {
            toggleEdit(task) {
                task.editable = !task.editable;
            },
            addTask() {
                if (this.newTask) {
                    this.tasks.push({
                        title: this.newTask,
                        completed: false,
                        editable: false
                    });
                    this.newTask = '';
                }
            },
            completeTask(task) {
                task.completed = ! task.completed;
            },
            removeTask(index) {
                this.tasks.splice(index, 1);
            },
            clearCompleted() {
                this.tasks = this.tasks.filter(this.inProgress);
            },
            clearAll() {
                this.tasks = [];

            },

            inProgress(task) {
                return ! this.isCompleted(task);
            },
            isCompleted(task) {
                return task.completed;
            },
        },
    }
</script>
<style lang="scss" scoped>
    .md-textarea{
    }
    .md-field {
        padding-top: 10px;
    }
    .padding-top{
        padding-top: 10px;
    }
    .padding-bot{
        padding-bottom: 25px;


    }
    .md-button{
        width: 100%;
    }
    .green{
        background-color: lawngreen;
    }
    .red{
        background-color: red;
    }
    .orange{
        background-color: darkorange;
    }

</style>
<template>

        <div class="md-layout md-alignment-center-space-around">
            <div class="md-layout-item">
                    <input
                            :class="className"
                            :disabled="readonly"
                            v-model="task.title"
                            @click.self="$emit('complete')">

            </div>
            <div class="md-layout-item md-size-10">
                <md-button v-if="readonly" @click="readonly = false">Edit</md-button>
                <md-button v-else @click="readonly = true">Save</md-button>
            </div>
            <div class="md-layout-item md-size-10 ">
                <md-button @click="$emit('remove')">Remove</md-button>
            </div>
        </div>

</template>

<script>
    export default {
        name: "task-item",
        props: ['task'],
        data(){
            return {
                readonly: false,
            }
        },
        computed: {
            className() {
                let classes = ['md-input', 'tasks__item__toggle'];
                if (this.task.completed) {
                    classes.push('tasks__item__toggle--completed');
                }
                return classes.join(' ');
            }
        }
    }
</script>
<style lang="scss" scoped>

    .fade-enter-active, .fade-leave-active {
        transition: opacity 0.5s;
    }
    .fade-enter,
    .fade-leave-active {
        opacity: 0;
    }
    .tasks {
        width: 100%;
        max-width: 45rem;
        padding: 1em;
        margin: 1em auto;
        overflow: auto;
        background-color: #fff;
        box-shadow: 0px 0.25rem 1rem rgba(0,0,0,0.25);
    }
    .tasks__list {
        clear: both;
    }
    .tasks__item {
        margin-bottom: 0.5em;
        position: relative;
    }
    .tasks__item__toggle {
        cursor: pointer;
        width: 100%;
        text-align: left;
        padding: 0.85em 2.25em 0.85em 1em;
        background-color: rgba(0,0,0,0.05);
        border: 1px solid rgba(0,0,0,0.1);
    }
    .tasks__item__toggle:hover {
        background-color: rgba(0,0,0,0.1);
        border-color: rgba(0,0,0,0.15);
    }
    .tasks__item__toggle--completed {
        background-color: rgba(0,128,0,0.15);
        border-color: rgba(0,128,0,0.2);
    }
    .tasks__item__toggle--completed:hover {
        background-color: rgba(0,128,0,0.25);
        border-color: rgba(0,128,0,0.3);
    }
    .tasks__item__remove {
        position: absolute;
        height: 100%;
        top: 50%;
        right: 0;
        -webkit-transform: translateY(-50%);
        transform: translateY(-50%);
    }


</style>
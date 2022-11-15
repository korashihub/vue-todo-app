<template>
    <div class="d-flex align-items-center">
        <div class="container d-flex flex-column align-items-center mt-5">
            <h3 class="text-white"><i>Vue 3 TODO App</i></h3>
            <div class="blur-card p-4 mt-3 shadow rounded d-flex gap-4">
                <input v-model="newTodo" @keyup.enter="addTodo" type="text" class="input-class shadow" id="todoInput"
                    placeholder="🤔 What are you going to do?">
                <button @click="addTodo" type="button" class="btn btn-dark shadow">📝 Add</button>
            </div>
            <div class="d-flex flex-column">
                <TransitionGroup name="list" appear>
                    <div v-for="(todo, index) in this.todoList" :key="index" style="min-width: 603px;"
                        class="blur-card p-4 mt-3 shadow rounded d-flex flex-column">
                        <span style="border-bottom: 1px solid;" :class="{ completed: todo.completed }">{{ todo.title
                        }}</span>
                        <div class="align-self-end d-flex gap-3 align-items-center mt-2">
                            <div class="form-check form-switch">
                                <input @click="completeTodo(todo)" class="form-check-input" type="checkbox" role="switch"
                                    :id="'checkbox' + index">
                                <label class="form-check-label" :for="'checkbox' + index">Completed</label>
                            </div>
                            <button @click="removeTodo(index)" class="btn btn-danger btn-sm">🗑️
                                Delete</button>
                        </div>
                    </div>
                </TransitionGroup>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'App',

    data() {
        return {
            newTodo: '',
            todoList: [{
                title: 'Iron the clothes immediately after waking up.',
                completed: false
            }, {
                title: 'Go out of the house for the market.',
                completed: false,
            }, {
                title: 'Return home at 8 o\'clock for dinner.',
                completed: false
            }]
        }
    },

    methods: {
        addTodo() {
            if (this.newTodo) {
                this.todoList.push({
                    title: this.newTodo,
                    completed: false
                });
                this.newTodo = '';
            }
        },
        completeTodo(todo) {
            todo.completed = !todo.completed;
        },
        removeTodo(index) {
            this.todoList.splice(index, 1)
        }
    }
}
</script>

<style>
.list-enter-active,
.list-leave-active {
    transition: all 0.5s ease;
}

.list-enter-from,
.list-leave-to {
    opacity: 0;
    transform: translateX(30px);
}

body {
    background: #141E30;
    background: -webkit-linear-gradient(to right, #243B55, #141E30);
    background: linear-gradient(to right, #243B55, #141E30);
    min-block-size: 100vh;
}

.blur-card {
    background: #abbaab;
    background: linear-gradient(to right, rgba(255, 255, 255, 0.5), rgba(178, 189, 178, 0.5));
    backdrop-filter: blur(4px);
}

.input-class {
    padding: 0.75rem;
    border-radius: 1rem;
    width: 450px;
    border: 0;
    transition: all ease 0.2s;
}

.input-class:focus {
    outline: none;
    transform: scale(1.05);
}

.completed {
    text-decoration: line-through;
}
</style>

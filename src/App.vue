<template>
    <div class="max-w-[700px] w-full m-auto p-6">
        <div class="w-full mb-8">
            <div class="w-full text-center mb-2">
                <h2 class="text-2xl font-semibold">Create New Todo</h2>
            </div>
            <div class="w-full m-auto form-group">
                <form @submit.prevent="submitTodo">
                    <div class="w-full form-item mb-2">
                        <input type="text" id="todo-txt" v-model="todo" placeholder="Write your todo" class="w-full border text-center border-slate-300 rounded-lg p-3 px-5 focus:outline-cyan-400 placeholder:opacity-45" />
                    </div>
                    <div class="w-full grid grid-cols-2 gap-2 form-item">
                        <button type="submit" class="col-span-1 duration-200 bg-green-300 hover:bg-green-400 p-3 rounded-lg text-[77%] font-medium text-green-900">Add Todo</button>
                        <button @click.prevent="clearInput" class="col-span-1 duration-200 bg-red-300 hover:bg-red-400 p-3 rounded-lg text-[77%] font-medium text-red-900">Clear</button>
                    </div>
                </form>
            </div>
        </div>
        <div class="w-full">
            <div class="w-full text-center mb-2">
                <h2 class="text-2xl font-semibold flex items-center justify-center">Todo List <small class="text-sm ml-2">({{ todos.length }})</small></h2>
            </div>
            <div class="todo-list">
                <span class="block text-center">{{ todos.length === 0 ? 'Henüz todo eklenmemiş' : '' }}</span>
                <ul>
                    <li v-for="todo in todos" v-bind:key="todo.id" class="mb-3 pb-3 border-b border-slate-200">
                        <h2 class="text-xl flex items-center justify-between">
                            <span>{{ todo.title }}</span>
                            <span @click="deleteTodo(todo.id)" class="text-red-400 cursor-pointer">
                                <i class="ri-close-large-line"></i>
                            </span>
                        </h2>
                    </li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
    import { uid } from 'uid';

    export default {
        data() {
            return {
                todo: '',
                todos: [],
                submitTodo: () => {
                    if(this.todo.length > 0) {
                        const newTodo = { id: uid(32), title: this.todo, completed: false }
                        const findTodo = (this.todos).find(todo => todo.title === newTodo.title)
                        if(findTodo) {
                            console.log('Bu todo daha önce eklenmiş')
                        } else {
                            this.todos.push(newTodo)
                            this.clearInput()
                        }
                    } else {
                        console.log('Boş alan bırakmayın')
                    }
                },
                clearInput: () => {
                    this.todo = ''
                },
                deleteTodo: (id) => {
                    this.todos = this.todos.filter(todo => todo.id !== id)
                }
            }
        }
    }
</script>

<style scoped>

</style>

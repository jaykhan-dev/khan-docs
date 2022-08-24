---
tags:
  - vue js
  - javascript
  - axios
  - rest
  - api
  - crud
  - http
  - web
  - server
---

# Axios

=== "axiosJSONServer"

    ```html
    <template>
    <div class="grid place-items-center border-b border-black py-20">
        <h1 class="text-4xl font-bold">AXIOS JSON Server</h1>
        <p>The following tasks have CRUD functionality</p>
        <!-- FORM -->
        <div class="flex space-x-4 my-8">
        <input
            type="text"
            v-model="todoName"
            @keyup.enter="addTodo()"
            aria-label="Add a new todo"
            placeholder="type task"
            class="border p-2 rounded border-black"
        />
        <button
            @click="addTodo()"
            type="submit"
            class="p-2 bg-green-500 hover:bg-blue-600"
        >
            Submit
        </button>
        </div>

        <!-- TASKS -->

        <div>
        <div class="flex space-x-2">
            <h1 class="text-2xl font-bold my-4">TODO</h1>
            <p v-for="todo in todos" :key="todo.id">{{ todoCount }}</p>
        </div>
        <ul class="space-y-2">
            <li
            v-for="todo of todos"
            :key="todo.id"
            :class="{ done: todo.done }"
            @click="doneTodo(todo.id)"
            class="p-2 rounded text-xl bg-gray-300"
            >
            {{ todo.name }}
            </li>
        </ul>
        </div>
    </div>
    </template>

    <script>
    import axios from "axios";
    const baseURL = "http://localhost:3001/todos";
    export default {
    name: "AxiosJSONServer",
    data() {
        return {
        todos: [],
        todoName: "",
        todoCount: "",
        };
    },
    async created() {
        try {
        const res = await axios.get(baseURL);
        this.todos = res.data;
        this.todoCount = res.data.count;
        } catch (e) {
        console.error(e);
        }
    },
    methods: {
        async addTodo() {
        try {
            const res = await axios.post(baseURL, { name: this.todoName });
            this.todos = [...this.todos, res.data];
            this.todoName = "";
        } catch (e) {
            console.error(e);
        }
        },
        async doneTodo(id) {
        try {
            await axios.patch(`${baseURL}/${id}`, {
            done: true,
            });
            this.todos = this.todos.map((todo) => {
            if (todo.id === id) {
                todo.done = true;
            }
            return todo;
            });
        } catch (e) {
            console.error(e);
        }
        },
        async deleteTodo(id) {},
    },
    };
    </script>

    <style scoped>
    .done {
    text-decoration: line-through;
    }
    </style>
    ```

=== "DjangoPrototypes"

    ```html
    <template>
    <div class="grid place-items-center py-20 border-b border-black">
        <h1 class="text-4xl font-bold my-4">Django Prototypes</h1>
        <p class="">The ultimate prize is figuring this out!</p>

        <!-- ADD TASK -->
        <div class="my-4 border border-black p-4">
        <h1 class="font-bold text-2xl my-4">POST</h1>
        <div class="flex flex-col space-y-2">
            <input
            type="text"
            class="p-2 border border-black"
            v-model="title"
            @keyup.enter="postTask()"
            placeholder="add task"
            />
            <!-- <input type="text" v-model="completed" name="" id="" /> -->
        </div>
        </div>
        <!-- TASKS -->
        <div
        class="my-4 flex space-x-2 items-center"
        v-for="task in tasks"
        :key="task.id"
        >
        <p class="text-xl font-bold">{{ task.id }}</p>
        <p class="text-xl">{{ task.title }}</p>

        <button class="p-2 bg-blue-500 text-white" @click="updateTask(task.id)">
            completed: {{ task.completed }}
        </button>
        <button class="p-2 bg-red-500 text-white" @click="deleteTask(task.id)">
            Delete
        </button>
        </div>
    </div>
    </template>

    <script>
    import axios from "axios";
    const localhost = "http://localhost:8000/api/";

    export default {
    name: "DjangoPrototypes",
    data() {
        return {
        tasks: [],
        title: "",
        //completed: false,
        };
    },
    async created() {
        try {
        const res = await axios.get(localhost + "task-list/");
        this.tasks = res.data;
        } catch (e) {
        console.error(e);
        }
    },
    methods: {
        async postTask() {
        try {
            const title = await axios.post(localhost + "task-create/", {
            title: this.title,
            completed: this.completed,
            });
            console.log(title);
            this.title = "";
        } catch (e) {
            console.error(e);
        }
        },
        async updateTask(id) {
        try {
            await axios.put(localhost + "task-update/" + id, {
            title: this.title,
            completed: this.completed,
            });
            this.tasks = this.tasks.map((task) => {
            if (task.id === id) {
                task.completed = true;
            }
            return task;
            });
        } catch (e) {
            console.error(e);
        }
        },
        async deleteTask(id) {
        let x = window.confirm("Delete task?");
        if (x) {
            const title = await axios.delete(localhost + "task-delete/" + id);
            console.log(title);
            alert("Task Deleted!");
        }
        },
    },
    };
    </script>

    <style></style>

    ```

=== "JSONPlaceholder"

    ```html
    <template>
    <div class="grid place-items-center py-20 border-b border-black">
        <div>
        <h1 class="text-4xl font-bold">JSON Placeholder</h1>
        <p>The following todos also have CRUD functionality</p>
        </div>
        <!-- FORM -->
        <div
        class="grid gap-4 place-items-center border border-black p-4 rounded my-4"
        >
        <!-- ADD USER -->
        <div>
            <h2 class="text-2xl">Add user</h2>
            <div class="flex flex-col space-y-2">
            <input
                type="text"
                v-model="name"
                class="border p-2 rounded border-black"
            />
            <input
                type="text"
                v-model="email"
                class="border p-2 rounded border-black"
            />
            </div>
            <button
            class="bg-purple-500 p-2 rounded my-4 text-white"
            @click="storeUser"
            >
            Add user
            </button>
        </div>
        </div>

        <!-- TODOS -->
        <div>
        <button
            @click="getUsers"
            class="p-2 bg-green-500 rounded my-4 text-white font-bold hover:bg-blue-500"
        >
            Get Users
        </button>
        <div v-for="user in users" :key="user.id">
            <h2 class="text-2xl my-4">{{ user.name }}</h2>
            <p>{{ user.email }}</p>
            <div class="flex flex-col space-y-2">
            <input
                type="text"
                v-model="user.name"
                class="p-2 border border-black rounded"
            />
            <input
                type="text"
                v-model="user.email"
                class="p-2 border border-black rounded"
            />
            </div>
            <div class="flex space-x-2">
            <button
                @click="editUser(user)"
                class="p-2 rounded bg-blue-500 text-white my-4"
            >
                Edit
            </button>
            <button
                @click="deleteUser(user.id)"
                class="p-2 rounded bg-red-500 text-white my-4"
            >
                Delete
            </button>
            </div>
        </div>
        </div>
    </div>
    </template>

    <script>
    import axios from "axios";
    const jsonURL = "https://jsonplaceholder.typicode.com/users/";

    export default {
    name: "JSONPlaceholder",
    data() {
        return {
        users: [],
        user: {},
        email: "",
        name: "",
        };
    },
    methods: {
        async getUsers() {
        try {
            const users = await axios.get(jsonURL);
            this.users = users.data;
        } catch (e) {
            console.log(e);
        }
        },
        async storeUser() {
        try {
            const user = await axios.post(jsonURL, {
            name: this.name,
            email: this.email,
            });
            console.log(user);
        } catch (e) {
            console.log(e);
        }
        },
        async updateUser() {
        try {
            const user = await axios.put(jsonURL + this.user.id, {
            name: this.user.name,
            email: this.user.email,
            });
            console.log(user.data);
            alert("User updated!");
        } catch (e) {
            console.log(e);
        }
        },
        async editUser(user) {
        this.user.name = user.name;
        this.user.email = user.email;
        this.user.id = user.id;
        },
        async deleteUser(id) {
        let x = window.confirm("you want to delete this user?!");
        if (x) {
            const user = await axios.delete(jsonURL + id);
            console.log(user);
            alert("User deleted!");
        }
        },
    },
    };
    </script>
    ```

=== "LogRocket"

    ```html
    <template>
    <div class="grid place-items-center">
        <h1 class="text-4xl my-4 font-bold">Log Rocket Tutorial</h1>
        <!-- CREATE -->
        <div class="">
        <form
            v-on:submit.prevent="submitForm"
            action=""
            class="grid place-items-center p-4 my-4 border border-black"
        >
            <div class="flex space-x-4 items-center my-4">
            <label for="title">Title</label>
            <input
                type="text"
                name=""
                id="title"
                class="p-2 border border-black"
                v-model="title"
            />
            </div>
            <button type="submit" class="p-2 bg-black text-white">Submit</button>
        </form>
        </div>
        <!-- LIST -->
        <div>
        <h1 class="text-2xl font-bold">Tasks</h1>
        <ul>
            <li
            v-for="task in tasks"
            :key="task.id"
            class="border space-x-2 p-2 my-2"
            >
            <h2 class="font-mono text-xl">{{ task.title }}</h2>
            <button @click="toggleTask(task)">
                {{ task.completed ? "Undo" : "Complete" }}
            </button>
            <button class="uppercase text-sm" @click="deleteTask(task)">
                delete
            </button>
            </li>
        </ul>
        </div>
    </div>
    </template>

    <script>
    import axios from "axios";
    const localhost = "http://localhost:8000/api/";

    export default {
    name: "LogRocket",
    data() {
        return {
        tasks: [],
        title: "",
        //completed: false,
        };
    },
    methods: {
        async getData() {
        try {
            const response = await axios.get(localhost + "task-list/");
            this.tasks = response.data;
        } catch (e) {
            console.error(e);
        }
        },
        async submitForm() {
        try {
            const response = await axios.post(localhost + "task-create/", {
            title: this.title,
            completed: false,
            });
            this.tasks.push(response.data);
            (this.title = ""), console.log(title);
        } catch (e) {
            console.error(e);
        }
        },
        async toggleTask(task) {
        try {
            const response = await axios.put(
            `http://localhost:8000/api/task-update/${task.id}`,
            {
                completed: !task.completed,
                title: task.title,
            }
            );
            let taskIndex = this.tasks.findIndex((t) => t.id === task.id);
            this.tasks = this.tasks.map((task) => {
            if (this.tasks.findIndex((t) => t.id === task.id) === taskIndex) {
                return response.data;
            }
            return task;
            });
            //console.log(task);
        } catch (e) {
            console.error(e);
        }
        },
        async deleteTask(task) {
        let confirmation = confirm("delete task?");
        if (confirmation) {
            try {
            await axios.delete(localhost + "task-delete/" + task.id);
            this.getData();
            } catch (e) {
            console.error(e);
            }
        }
        },
    },
    created() {
        this.getData();
    },
    };
    </script>
    ```

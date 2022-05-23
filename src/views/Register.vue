<template>
        <form @submit.prevent="submit">
        <h1 class="h3 mb-3 fw-normal">Please Register</h1>

        <input type="text" v-model="data.name" class="form-control" placeholder="Name">

        <input type="email" v-model="data.email" class="form-control" placeholder="Email">

        <input type="password" v-model="data.password" class="form-control" placeholder="Password">

        <button class="w-100 btn btn-lg btn-primary" type="submit">Sign in</button>
    </form>
</template>

<script lang="ts">
    import { reactive } from "vue"
import { useRouter } from "vue-router";
    export default {
        name: "Register",

        setup() {
            const data = reactive({
                name: '',
                email: '',
                password: ''
            });

            const router = useRouter();

            const submit = async () => {
                console.log('data', data)
                await fetch("http://localhost:8000/api/register", {
                    method: "POST",
                    headers: {'Content-Type': 'application/json'},
                    body: JSON.stringify(data)
                });

                await router.push("/login")
            }

            return {
                data,
                submit
            };
        }
    }
</script>
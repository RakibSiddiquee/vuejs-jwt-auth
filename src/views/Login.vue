<template>
    <form @submit.prevent="submit">
        <h1 class="h3 mb-3 fw-normal">Please sign in</h1>

        <input type="email" v-model="data.email" class="form-control" placeholder="Email">

        <input type="password" v-model="data.password" class="form-control" placeholder="Password">

        <span v-if="error" class="text-danger">{{ error }}</span>

        <button class="w-100 btn btn-lg btn-primary" type="submit">Sign in</button>
    </form>
</template>

<script lang="ts">
import { reactive, ref } from "vue"
import { useRouter } from "vue-router";

    export default {
        name: "Login",

        setup() {
            const error = ref('');

            const data = reactive({
                email: '',
                password: ''
            });

            const router = useRouter();

            const submit = async () => {
                const response = await fetch("http://localhost:8000/api/login", {
                    method: "POST",
                    headers: {'Content-Type': 'application/json'},
                    credentials: 'include',
                    body: JSON.stringify(data)
                });

                const content = await response.json();

                if (content.error) {
                    error.value = content.error;
                } else if (content.success) {
                    router.push("/");
                }
                
            }

            return {
                data,
                submit,
                error
            }
        }
    }
</script>
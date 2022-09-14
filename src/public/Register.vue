<template>
    <main class="form-signin w-100 m-auto">
        <form @submit.prevent="submit">
            <h1 class="h3 mb-3 fw-normal">Please register</h1>

            <div class="form-floating">
                <label for="first_name">First Name</label>
                <input type="text" class="form-control" id="first_name" placeholder="First Name" v-model="firstName">
            </div>

            <div class="form-floating">
                <label for="last_name">Last Name</label>
                <input type="text" class="form-control" id="last_name" placeholder="Last Name" v-model="lastName">
            </div>

            <div class="form-floating">
                <label for="role_id">Role Id</label>
                <input type="text" class="form-control" id="role_id" placeholder="Role Id" v-model="roleId">
            </div>

            <div class="form-floating">
                <label for="name">Name</label>
                <input type="text" class="form-control" id="name" placeholder="Name" v-model="name">
            </div>

            <div class="form-floating">
                <label for="floatingInput">Email address</label>
                <input type="email" class="form-control" id="floatingInput" placeholder="name@example.com"
                       v-model="email">
            </div>

            <div class="form-floating">
                <label for="floatingPassword">Password</label>
                <input type="password" class="form-control" id="floatingPassword" placeholder="Password"
                       v-model="password">
            </div>

            <div class="form-floating">
                <label for="passwordConfirm">Password Confirm</label>
                <input type="password" class="form-control" id="passwordConfirm" placeholder="Password"
                       v-model="passwordConfirm">
            </div>


            <button class="w-100 btn btn-lg btn-primary" type="submit">Register</button>
        </form>
    </main>
</template>

<script>
    /* eslint-disable */
    import {ref} from 'vue';
    import axios from 'axios';
    import {useRouter} from "vue-router";

    export default {
        name: "Register",
        setup() {
            const firstName = ref('');
            const lastName = ref('');
            const name = ref('');
            const email = ref('');
            const password = ref('');
            const passwordConfirm = ref('');
            const roleId = ref('');
            const router = useRouter();

            const submit = async () => {
                await axios.post('register',{
                    first_name: firstName.value,
                    last_name: lastName.value,
                    name: name.value,
                    email: email.value,
                    password: password.value,
                    password_confirm: passwordConfirm.value,
                    role_id: roleId.value,
                });

                await router.push('/login')
            }

            return {
                firstName,
                lastName,
                name,
                email,
                password,
                passwordConfirm,
                roleId,
                submit
            }
        }
    }
</script>

<style scoped>
    html,
    body {
        height: 100%;
    }

    body {
        display: flex;
        align-items: center;
        padding-top: 40px;
        padding-bottom: 40px;
        background-color: #f5f5f5;
    }

    .form-signin {
        max-width: 330px;
        padding: 15px;
    }

    .form-signin .form-floating:focus-within {
        z-index: 2;
    }

    .form-signin input[type="email"] {
        margin-bottom: -1px;
        border-bottom-right-radius: 0;
        border-bottom-left-radius: 0;
    }

    .form-signin input[type="password"] {
        margin-bottom: 10px;
        border-top-left-radius: 0;
        border-top-right-radius: 0;
    }
</style>
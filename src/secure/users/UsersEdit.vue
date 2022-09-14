<template>
    <form @submit.prevent="submit">
        <div class="form-group">
            <label>First Name</label>
            <input type="text" class="from-control" name="first_name" v-model="firstName">
        </div>
        <div class="form-group">
            <label>Last Name</label>
            <input type="text" class="from-control" name="last_name" v-model="lastName">
        </div>
        <div class="form-group">
            <label>Name</label>
            <input type="text" class="from-control" name="name" v-model="name">
        </div>
        <div class="form-group">
            <label>Email</label>
            <input type="text" class="from-control" name="email" v-model="email">
        </div>

        <div class="form-group">
            <label>Role</label>
            <select name="role_id" class="from-control" v-model="roleId">
                <option value="0">Select role</option>
                <option v-for="role in roles" :key="role.id" :value="role.id">
                    {{role.name}}
                </option>
            </select>
        </div>

        <button class="btn btn-outline-secondary">Save</button>
    </form>
</template>

<script lang="ts">
    import {ref, onMounted} from 'vue';
    import axios from 'axios';
    import {useRoute, useRouter} from "vue-router";
    import {User} from "@/classes/user";

    export default {
        name: "UsersEdit",
        setup() {
            const firstName = ref('');
            const lastName = ref('');
            const name = ref('');
            const email = ref('');
            const roleId = ref(0);
            const roles = ref([]);
            const router = useRouter();
            const {params} = useRoute();

            onMounted(async () => {
                const response = await axios.get('roles')

                roles.value = response.data.data;

                const userCall = await axios.get(`users/${params.id}`);

                const user: User = userCall.data.data;

                firstName.value = user.first_name;
                lastName.value = user.last_name;
                name.value = user.name;
                email.value = user.email;
                roleId.value = user.role.id;
            });

            const submit = async () => {
                await axios.put(`users/${params.id}`, {
                    first_name: firstName.value,
                    last_name: lastName.value,
                    name: name.value,
                    email: email.value,
                    role_id: roleId.value
                });

                await router.push('/users');
            }

            return {
                firstName,
                lastName,
                name,
                email,
                roleId,
                roles,
                submit
            }
        }
    }
</script>

<style scoped>

</style>
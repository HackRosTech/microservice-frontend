<template>
    <div class="table-responsive">
        <table class="table table-striped table-sm">
            <thead>
            <tr>
                <th scope="col">#</th>
                <th scope="col">Name</th>
                <th scope="col">Action</th>
            </tr>
            </thead>
            <tbody>
            <tr v-for="role in roles" :key="role.id">
                <td>{{role.id}}</td>
                <td>{{role.name}}</td>
                <td>
                    <div class="btn-group mr-2">
                        <router-link :to="`/roles/${role.id}/edit`" href="javascript:void(0)"
                                     class="btn btn-sm btn-outline-secondary">Edit
                        </router-link>
                        <a href="javascript:void(0)" class="btn btn-sm btn-outline-secondary" @click="del(role.id)">Delete</a>
                    </div>
                </td>
            </tr>
            </tbody>
        </table>
    </div>
</template>

<script lang="ts">
    import {ref, onMounted} from 'vue';
    import axios from 'axios';
    import {Entity} from "@/interfaces/entity";

    export default {
        name: "Roles",
        setup() {
            const roles = ref([]);

            onMounted(async () => {
                const response = await axios.get('roles');

                roles.value = response.data.data;
            });

            const del = async (id: number) => {
                if (confirm('Are ypu sure you want to delete this record?')) {
                    await axios.delete(`roles/${id}`);

                    roles.value = roles.value.filter((e: Entity) => e.id !== id);
                }
            }

            return {
                roles,
                del
            }
        }
    }
</script>

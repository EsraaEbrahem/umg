<template>
    <v-container>
        <v-row class="mb-5">
            <v-col cols="12" sm="6">
                <h2>Users</h2>
            </v-col>
        </v-row>
        <div>
            <EasyDataTable
                ref="dataTable"
                :headers="headers"
                :items="users"
                :rows-per-page="10"
            >
            </EasyDataTable>
        </div>
    </v-container>
</template>
<script>
import {getUsersApi} from "@/services/users-services.js";

export default {
    name: "users-index",
    data() {
        return {
            users: [],
            loading: false,
            user: {
                id: '',
                name: ''
            },
            headers: [
                {
                    text: "Id",
                    value: "id",
                    sortable: true
                },
                {
                    text: "Name",
                    value: "name",
                    sortable: true
                },
                {
                    text: "Email",
                    value: "email",
                    sortable: true
                }
            ],
        }
    },
    methods: {
        async getUsers() {
            this.loading = true;
            let response = await getUsersApi();
            if (response.status === 200)
                this.users = response.data;
            else
                this.$notify(response.statusText);
            this.loading = false;
        }
    },
    mounted() {
        this.getUsers();
    }
}
</script>



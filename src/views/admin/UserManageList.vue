<template>
    <div class="userMContainer">
        <h1 class="title text-center">User List</h1>
        <div class="tool d-flex justify-content-between align-items-center mb-3">
            <div class="sort d-flex align-items-center">
                <i class="bi bi-filter me-2"></i>
                <select class="form-select me-2" name="sort" v-model="sort">
                    <option value="">None</option>
                    <option value="sortname">Sort by name</option>
                    <option value="sortrole">Sort by role</option>
                </select>
                <button class="btn btn-primary" v-on:click="fetchUsers()">Apply</button>
            </div>
            <div class="search d-flex">
                <input type="text" name="search_val" value="" class="form-control me-2" placeholder="User Name" v-model="searchVal"/>
                <button class="btn btn-primary" v-on:click="fetchUsers()"><i class="bi bi-search"></i></button>
            </div>
        </div>
        <div class="list-container">
            <table class="table table-hover">
                <thead>
                    <tr class="table-primary">
                        <th scope="col">ID</th>
                        <th scope="col">Name</th>
                        <th scope="col">Email</th>
                        <th scope="col">Role</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-if="users.length === 0">
                        <td colspan="4" class="text-center">No user found.</td>
                    </tr>
                    <tr v-else v-for="user in users" :key="user.user_ID">
                        <td>{{ user.user_ID }}</td>
                        <td>{{ user.Username }}</td>
                        <td>{{ user.Email }}</td>
                        <td>{{ user.cRole }}</td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>
<script>
export default ({
    data(){
        return {
            sort: '',
            searchVal: '',
            users: [],
        }
    },
    methods: {
        async fetchUsers() {
            try {
                const response = await fetch(`http://localhost:8080/userManageList?search_val=${this.searchVal}&sort=${this.sort}`);
                this.users = await response.json();
            } catch (error) {
                console.error('Error fetching users:', error);
            }
        }
    },
    mounted() {
        this.fetchUsers();
    },
})
</script>


<style scoped>
.menuMContainer,
.orderMContainer,
.userMContainer {
    margin: 50px;
}

.addmenu {
    text-align: end;
    margin-bottom: 10px;
}

.addmenu .add img {
    width: 25px;
}

.title {
    font-size: 35px;
    text-align: center;
}

th:first-child {
    border-top-left-radius: 10px;
    padding-left: 20px;
}

th:last-child {
    border-top-right-radius: 10px;
    padding-right: 20px;
}

.tool {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.error {
    border: rgb(250, 145, 145) solid 2px;
    background-color: rgb(251, 161, 161);
}

.success {
    border: rgb(171, 255, 171) solid 2px;
    background-color: rgb(195, 255, 202);
}

.success,
.error {
    box-shadow: rgba(99, 99, 99, 0.2) 0px 2px 8px 0px;
    padding: 10px;
    width: fit-content;
    margin-left: 50px;
    position: fixed;
    animation: deleteAnimation 3s linear forwards;
    ;
    animation-fill-mode: forwards;
}

@keyframes deleteAnimation {
    0% {
        opacity: 1;
    }

    100% {
        opacity: 0;
        display: none;
    }
}

.success img,
.error img {
    margin-right: 10px;
}
</style>

<template>
<div class="vh-margin">
    <div class="v-margin">
        <transition>
            <loading class="loading"
                    :active.sync="loading"
                    :is-full-page=false
                    loader="bars"
                    color="#20b2aa"
                    :width="200"
                    :height="50"></loading>
        </transition>
    </div>
    <div class="v-margin">
        <template v-if="!loading">
            <transition mode="out-in" name="fade-in">
                <input v-model="filterText" type="text" name="searchQuery" placeholder="Enter Search" />
            </transition>
            <transition mode="out-in" name="fade-in">
                <button @click="filtered=!filtered" class="btn-primary">{{ filtered ? "Cancel Filter" : "Apply Filter" }}</button>
            </transition>
        </template>
    </div>
    <div class="v-margin">
        <transition mode="out-in" name="fade-in">
                <UserList class="user-list" v-if="!loading" :users="filteredUsers"></UserList>
        </transition>
    </div>
    <div>
        <nuxt-link :to="{name: 'users-add'}" tag="button" class="btn-primary">Add User</nuxt-link>
    </div>
</div>
</template>

<script>
import UserList from '~/components/users/UserList';
import Loading from 'vue-loading-overlay';
export default {
    data() {
        return {
            loading: true,
            filtered: false,
            filterText: "",
            users: [],
            searchQuery: ""
        }
    },
    computed: {
        maxHeight: function () {
            return this.users.length * 20 + "px";
        },

        filteredUsers: function () {
            if (!this.filtered) {
                return this.users;
            } else {
                const filterText = this.filterText.toLowerCase();
                return this.users.filter(u => {
                    const full = (u.firstName + " " + u.lastName).toLowerCase();
                    return full.includes(filterText);
                });
            }
        }
    },
    methods: {
        async getUsers() {
            const response = await this.$axios.$get('/api/users/?size=500');
            console.log(response);
            this.users= response._embedded.users;
            this.loading = false;
        },
    },
    mounted() {
        this.getUsers();
    },
    components: {
        UserList,
        Loading
    }
}
</script>

<style>
.loading {
    margin: 20px auto;
    width: 100%;
}

.fade-in-enter-active {
    transition: .5s ease-in;
}

.fade-in-enter {
    opacity: 0;
}
</style>

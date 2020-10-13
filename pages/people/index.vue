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
                <PeopleList class="people-list" v-if="!loading" :people="filteredPeople"></PeopleList>
        </transition>
    </div>
    <div>
        <nuxt-link :to="{name: 'people-add'}" tag="button" class="btn-primary">Add Person</nuxt-link>
    </div>
</div>
</template>

<script>
import PeopleList from '~/components/people/PeopleList';
import Loading from 'vue-loading-overlay';
export default {
    data() {
        return {
            loading: true,
            filtered: false,
            filterText: "",
            people: [],
            searchQuery: ""
        }
    },
    computed: {
        maxHeight: function () {
            return this.people.length * 20 + "px";
        },

        filteredPeople: function () {
            if (!this.filtered) {
                return this.people;
            } else {
                const filterText = this.filterText.toLowerCase();
                return this.people.filter(p => {
                    const full = (p.firstName + " " + p.lastName).toLowerCase();
                    return full.includes(filterText);
                });
            }
        }
    },
    methods: {
        async getPeople() {
            const response = await this.$axios.$get('/api/people');
            this.people = response._embedded.people;
            this.loading = false;
        },
    },
    mounted() {
        this.getPeople();
    },
    components: {
        PeopleList,
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

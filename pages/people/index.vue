<template>
<div>
    <div class="container">
        <transition>
            <loading class="loading"
                    :active.sync="loading"
                    :is-full-page=false
                    loader="bars"
                    color="#20b2aa"
                    :width="200"
                    :height="50"></loading>
        </transition>
        <transition mode="out-in" name="fade-in">
            <PeopleList class="people-list" v-if="!loading" :people="people"></PeopleList>
        </transition>
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
            people: []
        }
    },
    computed: {
        maxHeight: function () {
            return this.people.length * 20 + "px";
        }
    },
    methods: {
        async getPeople() {
            const response = await this.$axios.$get('/api/people');
            setTimeout(() => {
                this.people = response._embedded.people;
                this.loading = false;
            }, 1500);
        }
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
    transition: 1s ease-in;
}

.fade-in-enter {
    opacity: 0;
}
</style>

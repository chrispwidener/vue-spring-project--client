<template>
    <div class="vh-margin">
        <form name='person' action ='' method="post">
            <div class="form-group">
                <label for="first-name">First Name:</label>
                <input v-model="firstName" type="text" name="first-name" />
            </div>
            <div class="form-group">
                <label for="last-name">Last Name:</label>
                <input v-model="lastName" type="text" name="last-name" />
            </div>
            <button @click.prevent="createUser"
                    class="btn-primary" 
                    type="submit">Create User</button>
        </form>
    </div>
</template>

<script>
export default {
    data() {
        return {
            firstName: "",
            lastName: "",
        }
    },
    methods: {
        createUser() {
            this.$axios.$post('/api/users', {
                firstName: this.firstName,
                lastName: this.lastName
            });
            this.$router.push("/users")
        }
    }
}
</script>

<style scoped>
.form-group {
    margin: 10px 0;
}

label {
    display: block;
    font-weight: bold;
}
</style>

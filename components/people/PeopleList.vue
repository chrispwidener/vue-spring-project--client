<template>
<div>
    <table class="people-list">
        <thead>
            <th>#</th>
            <th>First Name</th>
            <th>Last name</th>
            <th>Options</th>
        </thead>
        <tbody>
            <tr v-for="(person, index) in people" :key="index">
                <td>{{ index + 1 }}</td>
                <td>{{ person.firstName }}</td>
                <td>{{ person.lastName }}</td>
                <td colspan='2'>Edit Delete</td>
            </tr>
        </tbody>
    </table>
</div>
</template>

<script>
export default {
    props: [
        'people'
    ]
}
</script>

<style scoped>
table.people-list {
    border: 1px solid lightseagreen;
}

thead {
    color: white;
    font-weight: bold;
    background-color: lightseagreen;
}

th {
    padding: 10px 30px;
}

td {
    padding: 3px;
    text-align: center;
}
</style>

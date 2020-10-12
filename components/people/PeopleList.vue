<template>
<table class="people-list">
    <thead>
        <th>First Name</th>
        <th>Last name</th>
        <th>Options</th>
    </thead>
    <tbody>
        <tr v-for="(person, index) in people" :key="index">
            <td>{{ person.firstName }}</td>
            <td>{{ person.lastName }}</td>
            <td colspan='2'>Edit Delete</td>
        </tr>
    </tbody>
</table>
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
    width: 100%;
    border: 1px solid lightseagreen;
    margin: 20px auto;
}

thead {
    color: white;
    font-weight: bold;
    background-color: lightseagreen;
}

th {
    padding: 10px;
}

td {
    padding: 3px;
    text-align: center;
}
</style>

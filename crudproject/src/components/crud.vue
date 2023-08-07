<script setup>

    const props = defineProps(["details"])
    
</script>

<template>
    <div>
        <table>
            <thead>
                <tr>
                    <td>First Name</td>
                    <td>Last Name</td>
                    <td>Company Name</td>
                </tr>
            </thead>
            <tbody>
                <tr v-for="detail in details" :key="detail.id">
                    <td>{{ detail.fname }}</td>
                    <td>{{ detail.lname }}</td>
                    <td>{{ detail.cname }}</td>
                    <td>
                        <button @click="$emit('editData', detail.id)">Edit</button>
                    </td>
                    <td>
                        <button @click="$emit('deleteData', detail.id)">Delete</button>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<style scoped>
 
</style>
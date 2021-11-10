<template>
    <div id="employee-table">
        <table>
            <thead>
                <tr>
                <th> Employee name </th>
                <th> Employee name </th>
                <th>Actions</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td>Dasso Ahmed</td>
                    <td>dassoahmed@gmail.com</td>
                </tr>
                 <tr>
                    <td>Night Crypt</td>
                    <td>loiclobe@gmail.com</td>
                </tr>
                 <tr>
                    <td>Kantin Fomekong</td>
                    <td>kantinfomekong@gmail.com</td>
                </tr>
                <tbody>
                    <tr v-for="employee in employees" :key="employee.id" >
                        <td v-if="editing === employee.id">
                        <input type="text" v-model="employee.name"/>
                        </td>
                        <td v-else> {{employee.name}}</td>
                        <td v-if="editing === employee.id">
                        <input type="text" v-model="employee.email"/>
                        </td>
                        <td v-else> {{employee.email}}</td>
                        <td v-if="editing === employee.id">
                        <button @click="ediEmployee(employee)">Save</button>
                        <button class="muted-button" @click="editing = null">Cancel</button>
                        </td>
                        <td v-else>
                            <button @click="editMode(employee.id)">Edit</button>
                            <button @click="$emit('delete:employee', employee.id)">Delete</button>
                        </td>
                        <td>{{employee.name }}</td>
                         <td>{{employee.name }}</td>
                         <td>
                        <button>Edit</button>
                        <button>Delete</button>
                        <button @click="editMode(employee.id)">Edit</button>
                        <button @click="$emit('delete:employee', employee.id)">Delete</button>
                        <p v-if="employees.length < 1" class="empty-table">No employees</p>
                        <table v-else>
                        ...
                        </table>
                        </td>
                        </tr>
                </tbody>
            </tbody>
        </table>
      
    </div>
</template>

<script>
  export default {
    name: 'employee-table',
    props: {
    employee: Array,
    data() {
    return {
    editing: null,
    }
    },
    methods: {
    editMode(id) {
    this.editing = id
    },

    editEmployee(employee) {
    if (employee.name === '' || employee.email === '') return
    this.$emit('edit:employee', employee.id, employee)
    this.editing = null
    }
    }
    }
  }
  
</script>

<style scoped>
 button {
    margin: 0 0.5rem 0 0;
  }
</style>
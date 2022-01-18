<template>
    <tr>
        <td>{{ statueItem.id }}</td>
        <td>{{ statueItem.person }}</td>
        <td>{{ statueItem.height }}</td>
        <td>{{ statueItem.price }}</td>
        <td>
            <button @click="deleteStatue(statueItem.id)">Delete</button>
            <button @click="editStatue(statueItem.id)">Edit</button>
        </td>
        <br />
        <td>
            <input type="hidden" v-model="statueItem.id">
        </td>
        <td>
            <input type="text" v-model="statueItem.person">
        </td>
        <td>
            <input type="number" v-model="statueItem.height">
        </td>
        <td>
            <input type="number" v-model="statueItem.price">
        </td>
        <td>
            
            <button v-if="!mod_new" @click="saveStatue" :disabled="saving">Save</button>
            <button v-if="!mod_new" @click="cancelEdit" :disabled="saving">Cancel</button>
        </td>
    </tr>
</template>

<script>
export default {
    props: ['statue'],
    data() {
        return {
            mod_new: true,
            saving: false,
            statueItem: {
                id: this.statue.id,
                person: this.statue.person,
                height: this.statue.height,
                price: this.statue.price
            },
            statues: []
        }
    },
    methods: {
        
    }
}
</script>

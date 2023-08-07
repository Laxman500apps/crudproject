<script setup>
    import crudVue from './crud.vue';
    import { ref } from 'vue'; 
    const fname = ref("") 
    const lname = ref("")
    const cname = ref("")
    const sId = ref(null)
    const details = ref([])
    const showData = ref(false)

    const emits = defineEmits(['editData', 'deleteData'])

    function addData(sId) {
        if(fname.value == '' | cname.value == '' | lname.value == '') {
            alert("Enter all details")
        }
        else if(sId) {
             const edata = details.value.filter((data) => data.id === sId)
             edata[0].fname = fname.value
             edata[0].lname = lname.value
             edata[0].cname = cname.value
        }
        else {
            details.value.push({
            id : Math.ceil(Math.random() * 100000),
            fname : fname.value,
            lname: lname.value,
            cname: cname.value
            })
        }
        showData.value = true
        fname.value = ''
        lname.value = ''
        cname.value = ''
    }

    function editData(id) { 
        sId.value = id
        const edata = details.value.filter((data) => data.id === id)
        fname.value = edata[0].fname
        lname.value = edata[0].lname
        cname.value = edata[0].cname
        
    }

    function deleteData(id) {
        const index  = details.value.findIndex((data) => data.id === id)
        details.value.splice(index,1)

    }

   

  
</script>

<template>
    <div class="container">
        <form @submit.prevent="addData(sId)">
            <div>
                <label for="fname">First Name</label>
                <input type="text" name="fname" id="fname" placeholder="enter your first name"  v-model="fname">
            </div>
            <div>
                <label for="lname">Last Name</label>
                <input type="text" name="lname" id="lname" placeholder="enter your last name" v-model="lname">
            </div>
            <div>
                <label for="cname">Company Name</label>
                <input type="text" name="cname" id="cname" placeholder="enter your company name" v-model="cname">
            </div>
            <div>
                <button type="submit">Add</button>
            </div>
        </form>
        <div v-if="showData">
            <crudVue :details="details" @editData="editData" @deleteData="deleteData"/>
        </div>
    </div>
</template>

<style scoped>
    form {
        display: flex;
    }

    .container {
        display: flex;
        flex-direction: column;
        justify-content: flex-start; 
        align-items: center;
    }
</style>
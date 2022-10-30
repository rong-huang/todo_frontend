<template>
    <div class="w-100 d-flex justify-content-center mt-3">
        <h1>All Schedule</h1>
    </div>
    <!-- eslint-disable -->
    <div class="w-100 mt-3 mb-3 d-flex flrx-column flex-wrap">
        <div class="card " style="margin-right: 1.5rem;margin-bottom: 2rem; margin-left: 1.5rem; width: 18rem;" v-for="(item) in allSchedulearrayData" :key="item.id">
            <div class="card-body" style="justify-content: baseline;">
                <h4 class="card-title" v-if="item.title == null">None title</h4>
                <h4 class="card-title" v-if="item.title != ''">{{item.title}}</h4>
                <p href="#" class="">ID: {{ item.id }}</p>
                <p href="#" class="">Create Time: {{ item.createdAt }}</p>
                <p href="#" class="">Update Time: {{ item.updatedAt }}</p>
            </div>
        </div>
    </div>
    <div class="w-100 d-flex justify-content-center mt-3">
        <h1>Select</h1>
    </div>
    <div class="w-100 mt-3 mb-3 d-flex flrx-column justify-content-center flex-wrap">
        <input class="me-2" type="text" style="border:solid border-color:darkgray" v-model="getScheduleId"> 
        <button type="button" class="btn btn-primary" @click="getScheduleApi()">Search</button>
    </div>
    <div class="w-100 mt-3 mb-3 d-flex flrx-column flex-wrap">
        <div class="card " style="margin-right: 1.5rem;margin-bottom: 2rem; margin-left: 1.5rem; width: 18rem;" v-for="(item) in SchedulearrayData" :key="item.id" v-if="this.SchedulearrayData!=null">
            <div class="card-body" style="justify-content: baseline;">
                <h4 class="card-title" v-if="item.title == null">None title</h4>
                <h4 class="card-title" v-if="item.title != ''">{{item.title}}</h4>
                <p href="#" class="">ID: {{ item.id }}</p>
                <p href="#" class="">Create Time: {{ item.createdAt }}</p>
                <p href="#" class="">Update Time: {{ item.updatedAt }}</p>
            </div>
        </div>
    </div>
    <div class="w-100 d-flex justify-content-center mt-3">
        <h1>Create Schedule</h1>
    </div>
    <div class="w-100 mt-3 mb-3 d-flex flrx-column justify-content-center flex-wrap">
        <input class="me-2" type="text" style="border:solid border-color:darkgray" v-model="addSchedule"> 
        <button type="button" class="btn btn-primary" @click="addScheduleApi()">Create</button>
    </div>
    <div class="w-100 d-flex justify-content-center mt-3">
        <h1>Update Schedule</h1>
    </div>
    <div class="w-100 mt-3 mb-3 d-flex flrx-column justify-content-center flex-wrap">
        <input class="me-2" type="text" style="border:solid border-color:darkgray" v-model="updateScheduleId">
        <input class="me-2" type="text" style="border:solid border-color:darkgray" v-model="updateScheduleTitle">
        <button type="button" class="btn btn-primary" @click="updateScheduleApi()">Update</button>
    </div>
    <div class="w-100 d-flex justify-content-center mt-3">
        <h1>Delete Schedule</h1>
    </div>
    <div class="w-100 mt-3 mb-3 d-flex flrx-column justify-content-center flex-wrap">
        <input class="me-2" type="text" style="border:solid border-color:darkgray" v-model="deleteScheduleId">
        <button type="button" class="btn btn-primary" @click="deleteScheduleApi()">Delete</button>
    </div>
    <!-- eslint-disable  -->
</template>

<script>
/* eslint-disable */
import axios from 'axios';
export default {
    data() {
        return {
            name: 'BoardView',
            getScheduleId:null,
            addSchedule:'',
            updateScheduleId:null,
            updateScheduleTitle:'',
            deleteScheduleId:null,
            allSchedulearrayData: [],
            SchedulearrayData:[],
            addSchedulearrayData:[],
            updateSchedulearrayData:[],
        }
    },
    methods: {
        getAllScheduleApi() {
            axios.get('http://localhost:3000/schedule')
                .then(res => {
                    console.log(res.status)
                    this.allSchedulearrayData = res.data.data;
                    console.log('arrayData', this.allSchedulearrayData)
                }) 
                .catch((error) => { console.error(error) })
        },
        getScheduleApi() {
            axios.get('http://localhost:3000/schedule/'+ this.getScheduleId)
                .then(res => {
                    console.log(res.data.data)
                    this.SchedulearrayData = res.data.data;
                    console.log('arrayData', this.SchedulearrayData)
                })
                .catch((error) => { console.error(error) })
        },
        addScheduleApi() {
            axios.post('http://localhost:3000/schedule/', { title: this.addSchedule })
                .then(res => {
                    console.log(res.data.data)
                    this.addSchedulearrayData = res.data.data;
                    console.log('arrayData', this.addSchedulearrayData)
                    
                })
                .catch((error) => { console.error(error) })
        },
        updateScheduleApi() {
            axios.patch('http://localhost:3000/schedule/'+this.updateScheduleId, { title: this.updateScheduleTitle })
                .then(res => {
                    if(res.status == 200){
                        console.log(res.data.data)
                        this.updateSchedulearrayData = res.data.data;
                        console.log('arrayData', this.updateSchedulearrayData)
                    }
                })
                .catch((error) => { console.error(error) })
        },
        deleteScheduleApi() {
            axios.delete('http://localhost:3000/schedule/'+this.deleteScheduleId)
                .then(res => {
                    if(res.status==200){
                        alert("Delete successful")
                    }
                })
                .catch((error) => { console.error(error) })
        }
    },
    // lifecycle 原件掛載完成時會啟用這個function
    mounted() {
        this.getAllScheduleApi();
    }
}
/* eslint-disable */
</script>

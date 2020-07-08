<template>
	<form @submit.prevent="addTask()"><input type="text" v-model="newTask" class="form-control bg-dark text-light mt-3" placeholder="Enter Task Name"></form>
</template>

<script>
export default {
	name: "NewTaskDialog",
	data(){
		return {
			newTask: ""
		}
	},
	props:{

	},
	methods:{
		addTask(){
			if(this.newTask.length>0){
				this.$emit("on-addTask", this.newTask);
				this.newTask = "";
			}else{
				alert("The Task name cannot be empty");
			}
		}
	}
}
</script>

<style>

</style>
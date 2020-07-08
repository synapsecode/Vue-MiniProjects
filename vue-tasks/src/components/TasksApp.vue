<template>
	<div id="todoAppContainer">
		<center><h5 class="display-4">Tasks App</h5></center>
		<TasksList/>
	</div>
</template>

<script>
import TasksList from './TasksList.vue';
export default {
	name: 'TasksApp',
	data(){
		return{
			
		}
	},
	props:{
	
	},
	methods:{
		
	},
	components:{
		TasksList
	}
}
</script>

<style>
#todoAppContainer{
	color: white;
    width: 420px; 
	height: 600px;   
    background-color: rgb(53, 53, 53);
    display: block;
    border-radius: 10px;
    margin: 0;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
	padding: 20px;
}
</style>
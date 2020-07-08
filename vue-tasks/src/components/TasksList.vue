<template>
	<div>
		<NewTaskDialog @on-addTask="addTask($event)"/>
		<div id="tasksList">
			<Task 
				v-for="(task, index) in tasks"
				:key="index"
				:taskName="task.taskName"
				:completed="task.completed"

				@on-delete="deleteTask(task)"
				@on-toggle="toggleTask(task)"
				@on-edit="editTask(task, $event)"
			/>
		</div>
	</div>
</template>

<script>
import Task from './Task.vue';
import NewTaskDialog from './NewTaskDialog.vue'
export default {
	name:"TasksList",
	props:{

	},
	mounted(){
		console.log("mounted")
		//console.log(type(localStorage.getItem('tasks'))
		if(JSON.parse(localStorage.getItem('tasks')).length > 0){
			console.log("Retrieving data from localStorage");
			this.tasks = JSON.parse(localStorage.getItem('tasks'));
		}else{
			console.log("LocalStorage Data is empty creating new tasksList!");
			this.tasks = [];
		}
	},
	methods:{
		addTask(newTask){
			let lastID = (this.tasks.length > 0) ? this.tasks[this.tasks.length - 1].id : -1;
			this.tasks.push({
				taskName: newTask,
				completed: false,
				id: ++lastID
			});
			console.log("Added new Task");
			this.saveTasks();
		},
		toggleTask(task){ 
			task.completed = !task.completed;
			console.log("Edit Toggled")
			this.saveTasks();
		},
		editTask(task, newTaskName){
			task.taskName = newTaskName;
			console.log("Editied Task");
			this.saveTasks();
		},
		deleteTask(deleteTask){
			this.tasks = this.tasks.filter( task => task.id !== deleteTask.id)
			console.log("Deleted Task");
			this.saveTasks();
		},
		saveTasks(){
			localStorage.setItem('tasks', JSON.stringify(this.tasks))
			console.log(localStorage);
		}
	},
	components:{
		Task,
		NewTaskDialog
	},
	data(){
		return{
			tasks: [
				// { taskName: "Make Angular Projects", completed: false, id:0},
				// { taskName: "Make ReactJS Projects", completed: false, id:1},
				// { taskName: "Make VueJS Projects", completed: false, id:2},
				// { taskName: "Make ML Projects", completed: false, id:3},
			]
		}
	}
}
</script>

<style>
#tasksList{
	margin-top:20px;
	border: 2px solid rgba(255, 255, 255, 0.089);
	height: 415px;
	width: 100%;
	overflow-y: auto;
	padding: 10px;
}

#tasksList::-webkit-scrollbar {
	background-color: rgba(0, 0, 0, 0.459);
	width: 1em;
}

#tasksList::-webkit-scrollbar-thumb {
  background-color: rgba(43, 43, 43, 0.911);
}
</style>
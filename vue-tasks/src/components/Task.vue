<template>
	<div class="task" :class="completed ? 'completed': 'incomplete'">
		<div id="checkgroup">
			<label class="chkcontainer">
				<input type="checkbox" id="chkbx" @click="$emit('on-toggle')" :checked="completed">
				<span class="checkmark"></span>
			</label>
		</div>
		<form @submit.prevent="endEditing()" class="taskNamegroup">
			<h2 id="tn" v-if="!isEditing">{{taskName}}</h2>
			<input v-else type="text" id="tn" v-model="newTaskName" @blur="startEditing()" class="form-control text-light" spellcheck="false">
		</form>
		<div class="ops">
			<button class="btn-danger ml-1 opb d">
				<img src="../assets/deleteicon.svg" class="ico" @click="$emit('on-delete')">
			</button>
			<button class="btn-primary ml-1 opb e" >
				<img src="../assets/editicon.svg" class="ico" @click="startEditing()">
			</button>
		</div>
	</div>
</template>

<script>
export default {
	name:"Task",
	props:{
		taskName: String,
		completed: Boolean
	},
	methods:{
		startEditing(){
			if(!this.isEditing){
				this.newTaskName = this.taskName;
				this.isEditing = true;
			}else{
				this.endEditing();
			}
		},
		endEditing(){
			this.isEditing = false;
			this.$emit('on-edit', this.newTaskName)
		}
	},
	data(){
		return {
			isEditing: false,
			newTaskName: "",
		}
	}
}
</script>

<style scoped>
.completed{
	background-color: rgba(58, 206, 66, 0.87); 
}

.incomplete{
	background-color: rgb(75, 75, 75);
}
.task{
	display: flex;
	border: 1px solid #666;
	width: 100%;
	height: 50px;
	border-radius: 5px;
	margin-bottom: 5px;
	padding: 10px;
}
#tn{
	height: 30px;
	margin-left: 22px;
	width: 90%;
	font-size: 20px;
	padding: 0 0 4px 10px;
	background-color: transparent;
}
.taskNamegroup{
	flex:9;
}
.ops{
	flex:3;
	margin-right: -8px;
	margin-top: -2px;
}
.opb{
	height: 32px;
	width: 32px;
	border-radius: 50%;
	padding: 0;
	background-color: rgb(39, 39, 39);
	border: 1px solid gray;
	outline: none;
}
.opb:focus{
	outline: none;
}
.d:hover{
	background-color: crimson;
}
.e:hover{
	background-color: rgb(27, 78, 187);
}	
.ico{
	width: 16px;
	height: 16px;
	margin-top: -4px;
}
/*--------------------Rounded Checkbox--------------------*/
#checkgroup{
	flex:1;
	margin-top: -7px;
	margin-left: -10px;

}
.chkcontainer {
	position: relative;
	display: block;
	cursor: pointer;
	margin: -27px 0px 5px 0;
}

/* Hide the browser's default checkbox */
.chkcontainer input {
	opacity: 0;
	cursor: pointer;
	height: 0;
	width: 0;
}

/* Create a custom checkbox */
.checkmark {
	position: absolute;
	top: 35px;
	left: 15px;
	height: 25px;
	width: 25px;
	background-color: transparent;
	border: 1px solid gray;;
	border-radius: 15px;
}

/* On mouse-over, add a grey background color */
.chkcontainer:hover input ~ .checkmark {
	background-color: rgb(68, 68, 68);
}

/* When the checkbox is checked, add a blue background */
.chkcontainer input:checked ~ .checkmark {
	background-color: #09a02ff6;
}

/* Create the checkmark/indicator (hidden when not checked) */
.checkmark:after {
	content: "";
	position: absolute;
	display: none;
}

/* Show the checkmark when checked */
.chkcontainer input:checked ~ .checkmark:after {
	display: block;
}

/* Style the checkmark/indicator */
.chkcontainer .checkmark:after {
	left: 6px;
	top: 7px;
	width: 12px;
	height: 6px;
	border: 2px solid white;
	border-top: none;
	border-right: none;
	transform: rotate(-45deg);
}
/*--------------------Rounded Checkbox--------------------*/
</style>
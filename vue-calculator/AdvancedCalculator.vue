<template>
	<div class="container">
		<div class="displaybar">
			<div class="display">{{this.displayValue}}</div>
			<!-- <div class="ans" :id="ans">= 0.0303</div> -->
		</div>
		<div class="calculator">
			<div @click="performOperation('invertTrig')" class="btn sml mt">&upsih;</div>
			<div @click="performOperation('pi')" class="btn sml mt">&#120587;</div>
			<div @click="performOperation('sin')" class="btn ce sml">sin</div>
			<div @click="performOperation('cos')" class="btn ce sml">cos</div>
			<div @click="performOperation('tan')" class="btn ce sml">tan</div>
			<div @click="performOperation('back')" class="btn sml mt">&larr;</div>
			<div @click="performOperation('log')" class="btn sml mt">lg</div>
			<div @click="performOperation('ln')" class="btn sml mt">ln</div>
			<div @click="performOperation('cbrt')" class="btn sml mt">&#8731;x</div>
			<div @click="performOperation('sqrt')" class="btn sml mt">&Sqrt;x</div>
			<div @click="performOperation('e')" class="btn sml mt">e</div>
			<div @click="performOperation('clear')" class="btn ce sml">AC</div>
			<div @click="performOperation('exp')" class="btn ce sml">x<sup style="font-size: 18px; margin-left:3px;">y</sup></div>
			<div @click="performOperation('percent')" class="btn ce sml">%</div>
			<div @click="performOperation('divide')" class="btn ce">÷</div>
			<div @click="performOperation('square')" class="btn sml mt">x<sup style="font-size: 16px; margin-left:3px;">2</sup></div>
			<div @click="append('7')" class="btn">7</div>
			<div @click="append('8')" class="btn">8</div>
			<div @click="append('9')" class="btn">9</div>
			<div @click="performOperation('multiply')" class="btn ce">x</div>
			<div @click="performOperation('factorial')" class="btn sml mt">x!</div>
			<div @click="append('4')" class="btn">4</div>
			<div @click="append('5')" class="btn">5</div>
			<div @click="append('6')" class="btn">6</div>
			<div @click="performOperation('subtract')" class="btn ce">-</div>
			<div @click="performOperation('reciprocal')" class="btn sml mt">x<sup style="font-size: 16px; margin-left:3px;">-1</sup></div>
			<div @click="append('1')" class="btn">1</div>
			<div @click="append('2')" class="btn">2</div>
			<div @click="append('3')" class="btn">3</div>
			<div @click="performOperation('add')" class="btn ce">+</div>
			<div @click="performOperation('lb')" class="btn mt sml">(</div>
			<div @click="performOperation('rb')" class="btn mt sml">)</div>
			<div @click="append('0')" class="btn">0</div>
			<div @click="performOperation('point')" class="btn">.</div>
			<div><center><div class="e" @click="calculate">=</div></center></div>
		</div>
	</div>
</template>

<script>
export default {
	data(){
		return{
			displayValue: "",
			trigInverted:false,
		}
	},
	methods: {
		fact(n){
			if(n==0) return 1;
			let s = "";
			for(let i=parseInt(n); i>0; i--) s+=`${i}*`;
			return eval(`(${s.substring(0, s.length-1)})`);
		},
		performOperation(op){
			console.log(op);
			switch(op){
				case "invertTrig":
					this.trigInverted = !(this.trigInverted);
					if(this.trigInverted){
						document.getElementById("s").innerHTML = `sin<sup style="font-size: 16px; margin-left:3px;">2</sup>`;
					}
					//changeTrigBehaviour
					
					break;
				case "pi":
					this.displayValue += "𝜋";
					break;
				case "sin":
					this.displayValue += (this.trigInverted) ? "ArcSin(" : "sin(";
					break;
				case "cos":
					this.displayValue += (this.trigInverted) ? "ArcCos(" : "cos(";
					break;
				case "tan":
					this.displayValue += (this.trigInverted) ? "ArcTan(" : "tan(";
					break;
				case "back":
					this.displayValue = this.displayValue.substring(0, this.displayValue.length-1);
					break;
				case "log":
					this.displayValue += "log(";
					break;
				case "ln":
					this.displayValue += "ln(";
					break;
				case "cbrt":
					this.displayValue += "∛(";
					break;
				case "sqrt":
					this.displayValue += "√(";
					break;
				case "e":
					this.displayValue += "e";
					break;
				case "clear":
					this.displayValue = "";
					break;
				case "exp":
					this.displayValue += "^(";
					break;
				case "percent":
					this.displayValue += "%";
					break;
				case "divide":
					this.displayValue += " ÷ ";
					break;
				case "square":
					this.displayValue += "^(2)";
					break;
				case "multiply":
					this.displayValue += " x ";
					break;
				case "factorial":
					this.displayValue += "fact(";
					break;
				case "subtract":
					this.displayValue += " - ";
					break;
				case "reciprocal":
					this.displayValue += "^(-1)";
					break;
				case "add":
					this.displayValue += " + ";
					break;
				case "lb":
					this.displayValue += "(";
					break;
				case "rb":	
					this.displayValue += ")";
					break;
				case "point":
					this.displayValue += ".";
					break;
				default:
					break;
			}
		},
		append(n){
			console.log(n);
			this.displayValue += `${n}`
		},
		calculate(){
			let s = this.displayValue.toString();
			s = s.replace(/x/g, "*")
				.replace(/÷/g, "/")
				.replace(/e/g, "Math.E")
				.replace(/𝜋/g, "Math.PI")
				.replace(/sin/g, "Math.sin")
				.replace(/cos/g, "Math.cos")
				.replace(/tan/g, "Math.tan")
				.replace(/ArcSin/g, "Math.asin")
				.replace(/ArcCos/g, "Math.acos")
				.replace(/ArcTan/g, "Math.atan")
				.replace(/√/g, "Math.sqrt")
				.replace(/∛/g, "Math.cbrt")
				.replace(/log/g, "Math.log10")
				.replace(/ln/g, "Math.log")
				.replace(/%/g, "*0.01")
				.replace(/\^/g, "**")
				.replace(/fact/g, "this.fact");
			console.log(s);
			this.displayValue = eval(s);
		}
	}
}
</script>

<style scoped>
	body{
		font-family: Avenir, Helvetica, Arial, sans-serif;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
		text-align: center;
	}
	.calculator{
		border: 1px solid rgb(29, 29, 29);
		background-color: rgb(22, 22, 22);
		color: white;
		font-size: 40px;
		display: grid;
		grid-template-columns: repeat(5, 1fr);
		grid-auto-rows: minmax(50px, auto);
		padding: 10px;
	}
	.displaybar{
		background-color: rgb(22, 22, 22);
		height: 60px;
		margin: 10px 0px 10px 0px;
		font-size: 30px;
		border: 1px solid #333;
		overflow-x: scroll;	
		overflow-y: hidden;
	}
	.display{
		padding: 12px 0 0 10px;
		width: 10000px;
		text-align: left;
		opacity:0.3;
	}

	/* #ans{
		font-size: 18px;
		opacity:0.5;
		float: right;
		margin-right:10px;
	} */

	.displaybar::-webkit-scrollbar{
		display: none;
	}

	.ce{
		color: rgb(255, 124, 2);
	}
	.e{
		cursor: default;
		background-color: rgb(255, 116, 2);
		border-radius: 50%;
		width: 46px;
		height: 46px;
	}
	.e:hover{
		background-color: rgb(255, 140, 0);
	}

	.btn{
		cursor: default;
	}
	.btn:hover{
		border: 1px solid #333;
		background-color: rgba(51, 51, 51, 0.562);
	}
	.sml{
		font-size: 30px;
		padding:10px;
	}
	.container{
		padding: 10px 10px 20px 10px;
		background-color: rgb(32,32,32);
		border-radius:5px;
		color: white;
		width: 350px;
		position: absolute;
		top: 50%;
		left: 50%;
		-ms-transform: translateX(-50%) translateY(-50%);
		-webkit-transform: translate(-50%,-50%);
		transform: translate(-50%,-50%);
	}
	.mt{
		opacity: 0.5;
	}
</style>
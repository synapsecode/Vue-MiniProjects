<template>
	<div class="container">
		<div class="displaybar">
			<input type="text" class="display" v-model="displayValue">
			<!-- <div class="ans" :id="ans">= 0.0303</div> -->
		</div>
		<div class="calculator">
			<div @click="performOperation('invert')" v-bind:class="['btn mt sml',  (this.inverted) ? 'inv': '']">&upsih;</div>
			<div @click="performOperation('pi')" class="btn sml mt">&#120587;</div>
			<div @click="performOperation('sin')" v-bind:class="['btn ce sml', (this.inverted) ? 't': '']">sin<sup v-if="(this.inverted)" style="font-size: 12px; margin-left:3px;">-1</sup></div>
			<div @click="performOperation('cos')" v-bind:class="['btn ce sml', (this.inverted) ? 't': '']">cos<sup v-if="(this.inverted)" style="font-size: 12px; margin-left:3px;">-1</sup></div>
			<div @click="performOperation('tan')" v-bind:class="['btn ce sml', (this.inverted) ? 't': '']">tan<sup v-if="(this.inverted)" style="font-size: 12px; margin-left:3px;">-1</sup></div>
			<div @click="performOperation('e')" class="btn sml mt">e</div>
			<div @click="performOperation('ln')" class="btn sml mt">{{naturallog}}<sup v-if="(this.inverted)" style="font-size: 16px; margin-left:3px;">x</sup></div>
			<div @click="performOperation('log')" class="btn sml mt">{{log10}}<sup v-if="(this.inverted)" style="font-size: 16px; margin-left:3px;">x</sup></div>
			<div @click="performOperation('sqrt')" class="btn sml mt">&Sqrt;x</div>
			<div @click="performOperation('cbrt')" class="btn sml mt">&#8731;x</div>
			<div @click="performOperation('back')" class="btn sml mt">&larr;</div>
			<div @click="performOperation('clear')" class="btn ce sml" style="font-size:24px; padding-top:13px;">AC</div>
			<div @click="performOperation('exp')" v-bind:class="['btn ce sml', (this.inverted) ? 'exp': '']">{{xp}}<sup v-if="(!this.inverted)" style="font-size: 18px; margin-left:3px;">y</sup><sup v-if="(this.inverted)" style="font-size: 18px; margin-left:-2px;">&macr;</sup></div>
			<div @click="performOperation('percent')" class="btn ce sml">%</div>
			<div @click="performOperation('divide')" class="btn ce">÷</div>
			<div @click="performOperation('reciprocal')" v-bind:class="['btn mt sml', (this.inverted) ? 'exp': '']">{{rp}}<sup v-if="(!this.inverted)" style="font-size: 16px; margin-left:3px;">-1</sup></div>
			<div @click="append('7')" class="btn tx">7</div>
			<div @click="append('8')" class="btn tx">8</div>
			<div @click="append('9')" class="btn tx">9</div>
			<div @click="performOperation('multiply')" class="btn ce">x</div>
			<div @click="performOperation('square')" class="btn sml mt">{{sq}}<sup v-if="(!this.inverted)" style="font-size: 16px; margin-left:3px;"> 2</sup></div>
			<div @click="append('4')" class="btn tx">4</div>
			<div @click="append('5')" class="btn tx">5</div>
			<div @click="append('6')" class="btn tx">6</div>
			<div @click="performOperation('subtract')" class="btn ce">-</div>
			<div @click="performOperation('factorial')" v-bind:class="['btn mt sml', (this.inverted) ? 'exp': '']">{{f}}</div>
			<div @click="append('1')" class="btn tx">1</div>
			<div @click="append('2')" class="btn tx">2</div>
			<div @click="append('3')" class="btn tx">3</div>
			<div @click="performOperation('add')" class="btn ce">+</div>
			<div @click="performOperation('lb')" class="btn mt sml">(</div>
			<div @click="performOperation('rb')" class="btn mt sml">)</div>
			<div @click="append('0')" class="btn tx">0</div>
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
			inverted:false,
			log10: 'lg',
			naturallog:'ln',
			sq: 'x',
			f:'x !',
			rp: 'x',
			xp:'x'
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
				case "invert":
					this.inverted = !(this.inverted);
					//changeTrigBehaviour
					if(this.inverted){
						this.log10 = "10";
						this.naturallog = "e";
						this.sq="|x|";
						this.f="exp";
						this.rp="rnd";
						this.xp="n√"
					}else{
						this.log10 = "lg";
						this.naturallog = "ln";
						this.sq="x";
						this.f="x !";
						this.rp="x"
						this.xp="x"
					}
					
					break;
				case "pi":
					this.displayValue += "𝜋";
					break;
				case "sin":
					this.displayValue += (this.inverted) ? "ArcSin(" : "sin(";
					break;
				case "cos":
					this.displayValue += (this.inverted) ? "ArcCos(" : "cos(";
					break;
				case "tan":
					this.displayValue += (this.inverted) ? "ArcTan(" : "tan(";
					break;
				case "back":
					this.displayValue = this.displayValue.substring(0, this.displayValue.length-1);
					break;
				case "log":
					this.displayValue += (this.inverted) ? "10^(" : "log(";
					break;
				case "ln":
					this.displayValue += (this.inverted) ? "e^(" : "ln(";
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
					this.displayValue += (this.inverted) ? "^(1/" : "^(";
					break;
				case "percent":
					this.displayValue += "%";
					break;
				case "divide":
					this.displayValue += " ÷ ";
					break;
				case "square":
					this.displayValue += (this.inverted) ? "abs(" : "^(2)";
					break;
				case "multiply":
					this.displayValue += " x ";
					break;
				case "factorial":
					this.displayValue += (this.inverted) ? "E+(" : "fact(";
					break;
				case "subtract":
					this.displayValue += "-";
					break;
				case "reciprocal":
					this.displayValue += (this.inverted) ? `${Math.random().toFixed(5)}` : "^(-1)";
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
			try {
				let s = this.displayValue.toString();
				if(s===""){ alert("Please Enter an expression before calculating"); return;}
				//-------------------------------------AUTO MULTIPLICATION-----------------------------------------------
				s=s.replace(/𝜋/g, "~");
				for(let i=0; i<s.length-1; i++){
					let ch = s.charAt(i);
					let nxt = s.charAt(i+1);
					if(ch==='0'||ch==='1'||ch==='2'||ch==='3'||ch==='4'||ch==='5'||ch==='6'||ch==='7'||ch==='8'||ch==='9'||ch==='~'){
						console.log(nxt)
						if(nxt==="(" || nxt==="~" || nxt==="e"){
							console.log("change")
							s = s.substring(0, i+1)+"*"+s.substring(i+1, s.length);
						}
					}
				}
				console.log(s);
				s=s.replace(/~/g, "𝜋");
				//------------------------------------- END AUTO MULTIPLICATION------------------------------------------
				console.log("Modified Expression: "+s);
				s = s.replace(/x/g, "*")
					.replace(/÷/g, "/")
					.replace(/abs/g, "Math.abs")
					.replace(/e/g, "Math.E")
					.replace(/E\+/g, "*10^")
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
				console.log("Replaced Expression: "+s);
				this.displayValue = eval(s);
			} catch (error) {
				alert(error);
				
			}
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
		background-color: rgba(22, 22, 22, 0.514);
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
		border: 1px solid #333;
		overflow-x: scroll;	
		overflow-y: hidden;
	}
	.display{
		padding: 0 20px 0 10px;
		width:100%;
		height: 100%;
		text-align: left;
		opacity:0.3;
		font-size: 30px;
		background-color: transparent;
		color: white;
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
		color: rgb(53, 151, 66);
	}
	.e{
		cursor: default;
		background-color: rgb(35, 107, 45);
		border-radius: 50%;
		margin-top: 10px;
		width: 46px;
		height: 46px;
	}
	.e:hover{
		
		background-color: rgb(57, 168, 72);
	}
	.inv{
		background-color: rgb(57, 168, 72);
	}
	
	.btn{
		cursor: default;
		border: 1px solid rgba(51, 51, 51, 0.253);
	}
	.btn:hover{
		border: 0.5px solid #333;
		background-color: rgba(51, 51, 51, 0.397);
		transition: background-color 0.2s ease;
	}
	.inv:hover{
		background-color: rgb(38, 105, 47);
	}
	.sml{
		font-size: 30px;
		padding:10px;
	}
	.tx{
		padding-top:5px;
	}
	.container{
		padding: 10px 10px 10px 10px;
		background-color: rgba(32, 32, 32, 0.596);
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
	.t{
		padding-top:17px;
		padding-left: 10px;
		font-size: 19px;
	}
	.exp{
		font-family: 'Courier New', Courier, monospace;
		font-size: 24px;
	}
</style>
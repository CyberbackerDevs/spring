<template>
	<div class="d-main-content" :style="{ backgroundImage: 'url(' + require('@/assets/bg.jpg') + ')' }">
		
		<div class="d-main-form">
			<div class="d-main-page-inner">
				<div class="d-main-header-image"><img src="@/assets/logo.png"/></div>
				<div class="d-main-header-presents">presents</div>
				<div class="d-main-header-spring">Spring</div>
				<div class="d-main-header-mastermind">Mastermind</div>
				<div class="d-main-header-date">2022</div>
			</div>	
			<div class="d-main-into">
				<div class="d-main-into-inner">
					<p>Cyberbacker is one of the leading providers of virtual support services across all industries. We are committed to freeing up your time to focus on your one thing—growth. Don’t hold your business back by wearing different hats. Fill out the form to get started!</p>
					<p>For audio, please fill out this form, stay near the tablet and i will call you</p>
				</div>
			</div>
			<div class="d-main-form">
				<div class="d-main-form-inner">
					<div class="d-form-item">
						<label for="">Full Name</label>
						<input type="text" >
					</div>
					<div class="d-form-item">
						<label for="">Mobile Number</label>
						<input type="text" >
					</div>
					<div class="d-form-item">
						<label for="">Email Address</label>
						<input type="text" >
					</div>
					<div class="d-form-item">
						<label for="">Job Title</label>
						<input type="text" >
					</div>
					<div class="d-form-item">
						<label for="">State</label>
						<select name="" id="">
							<option :value="state" v-for="state in states" :key="state">{{state}}</option>
						</select>
					</div>
					<div class="d-form-item">
						<label for="">County</label>
						<input type="text" >
					</div>
					<div class="d-form-item">
						<label for="">Country</label>
						<input type="text" >
					</div>
					<div class="d-form-item submitform">
						<button>Submit</button>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	name: 'IndexPage',
	layout: "base",
	data(){
		return {
			states: [
				'Alabama', 'Alaska', 'Arizona', 'Arkansas', 'California', 'Colorado', 'Connecticut',
				'Delaware', 'Florida', 'Georgia', 'Hawaii', 'Idaho', 'Illinois', 'Indiana', 'Iowa', 'Kansas',
				'Kentucky', 'Louisiana', 'Maine', 'Maryland', 'Massachusetts', 'Michigan', 'Minnesota', 
				'Mississippi', 'Missouri', 'Montana', 'Nebraska', 'Nevada', 'New Hampshire', 'New Jersey', 
				'New Mexico', 'New York', 'North Carolina', 'North Dakota', 'Ohio', 'Oklahoma', 'Oregon',
				'Pennsylvania', 'Rhode Island', 'South Carolina', 'South Dakota', 'Tennessee', 'Texas', 'Utah', 
				'Vermont', 'Virginia', 'Washington', 'West Virginia', 'Wisconsin', 'Wyoming'
			]
		}
	}
}
</script>

<style scoped>
.d-main-content {
	font-family: 'Nunito', sans-serif;
	height: 100%;
	background-size: cover;
	padding: 20px 0 50px;
}
.d-main-form {
	width: 680px;
    margin: 0px auto 0px;
}
.d-main-header-image img {
	width: 500px;
}
.d-main-header-image {
	text-align: center;
	padding-top: 60px;
}
.d-main-header-presents {
	text-align: center;
    font-weight: 600;
    font-size: 15px;
    margin-top: -5px;
    margin-bottom: 10px;
    color: #424362;
    text-transform: uppercase;
}
.d-main-header-spring {
	font-family: 'Square Peg', cursive;
	text-align: left;
    line-height: 1em;
    font-size: 117px;
    margin-bottom: -47px;
    position: relative;
    z-index: 2;
    color: #ffffff;
    text-shadow: 0 0 12px #434261;
    padding-left: 109px;
}
.d-main-header-mastermind {
	text-align: center;
    font-weight: 600;
    text-transform: uppercase;
    font-size: 88px;
    letter-spacing: -6px;
    color: #3e425f;
	line-height: 1em;
	transform: rotate(-4deg);
}
.d-main-header-date {
	font-family: 'Square Peg', cursive;
	text-align: right;
    line-height: 1em;
    font-size: 50px;
    margin-top: -42px;
    position: relative;
    z-index: 2;
    color: #ffffff;
    text-shadow: 0 0 12px #434261;
    padding-right: 108px;
    margin-bottom: 50px;
    font-weight: bold;
}
.d-main-form-inner {
	background: #fff;
    padding: 70px;
    border-radius: 20px;
    box-shadow: 0 0 12px #fcd9d3;
    width: 86%;
    margin: 0 auto;
}
.d-form-item {
	margin-bottom: 20px;
}
.d-main-form-inner label {
	display: block;
    font-size: 18px;
    line-height: 1em;
    font-weight: bold;
    margin-bottom: 5px;
}
.d-main-form-inner input {
	width: 100%;
    border: 1px solid #404b78;
    font-size: 16px;
    line-height: 1em;
    padding: 15px 15px;
    border-radius: 10px;
	box-shadow: 0 0 12px #d5b6d6;
}
.d-main-form-inner select {
	width: 100%;
    border: 1px solid #404b78;
    font-size: 16px;
    line-height: 1em;
    padding: 15px 15px;
    border-radius: 10px;
	box-shadow: 0 0 12px #d5b6d6;
}
.d-main-into {
	width: 86%;
    margin: 0 auto 30px;
	text-align: center;
}
.d-main-into p {
	font-size: 18px;
	line-height: 1.2em;
	margin-bottom: 10px;
}
.submitform button {
	font-size: 18px;
    text-align: center;
    display: block;
    width: 100%;
    text-transform: uppercase;
    background: #484467;
    color: #fff;
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 0 12px #8f8fc1;
}
</style>
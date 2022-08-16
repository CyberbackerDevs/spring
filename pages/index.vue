<template>
	<div class="d-main-content" :style="{ backgroundImage: 'url(' + require('@/assets/bgv.jpeg') + ')' }">
		
		<div class="d-main-form">
			<div class="d-main-page-inner">
				<div class="d-main-header-image"><img src="@/assets/logo.png"/></div>
				<!-- <div class="d-main-header-presents">presents</div> -->
				<!-- <div class="d-main-header-spring">Inman</div> -->
				<div class="d-main-header-mastermind">Inman Connect</div>
				<div class="d-main-header-date">Las Vegas</div>
			</div>	
			<div class="d-main-into">
				<div class="d-main-into-inner">
					<p>Six months down this 2022 and everything’s moving fast. Cyberbacker is ready to climb up towards success with you. Join us as we connect you with the best people from our company at the INMAN event in Las Vegas! We consistently convert transactions into relationships. Make great things happen with Cyberbacker!</p>
					<p>For audio, please fill out this form, stay near the tablet and i will call you</p>
				</div>
			</div>
			<div class="d-main-form">
				<div v-if="!show_thank_you" class="d-main-form-inner">
					<div class="d-form-item">
						<label for="">Full Name <span v-if="error_name" class="form-is-required">*required</span></label>
						<input type="text" v-model="form.name">
					</div>
					<div class="d-form-item">
						<label for="">Mobile Number <span v-if="error_mobile" class="form-is-required">*required</span></label>
						<input type="text" v-model="form.mobile">
					</div>
					<div class="d-form-item">
						<label for="">Email Address <span v-if="error_email" class="form-is-required">*required</span></label>
						<input type="text" v-model="form.email">
					</div>
					<div class="d-form-item">
						<label for="">Job Title</label>
						<input type="text" v-model="form.job_title">
					</div>
					<div class="d-form-item">
						<label for="">Industry <span v-if="error_email" class="form-is-required">*required</span></label>
						<select v-model="form.industry" @change="onIndustryChange($event)" name="" id="">
							<option value="Real estate agent">Real estate agent</option>
							<option value="Mortgage">Mortgage</option>
							<option value="Title">Title</option>
							<option value="CRM">CRM</option>
							<option value="Technology">Technology</option>
							<option value="Marketing/Social Media">Marketing/Social Media</option>
							<option value="Lead Generation">Lead Generation</option>
							<option value="Home Warranty">Home Warranty</option>
							<option value="Insurance">Insurance</option>
							<option value="E-commerce">E-commerce</option>
							<option value="Travel/Tourism">Travel/Tourism</option>
							<option value="Education">Education</option>
							<option value="Financial">Financial</option>
							<option value="Office/Administration">Office/Administration</option>
							<option value="Human Resources">Human Resources</option>
							<option value="Tax Consulting">Tax Consulting</option>
							<option value="Healthcare">Healthcare</option>
							<option value="Arts/Entertainment">Arts/Entertainment</option>
							<option value="Retail">Retail</option>
							<option value="Other">Other</option>
						</select>
						<!-- <input type="text" v-model="form.email"> -->
					</div>
					<div class="d-form-item" v-if="show_other_industry">
						<label for="">Other Industry</label>
						<input type="text" v-model="other_industry" placeholder="Enter other industry">
					</div>
					<div class="d-form-item">
						<label for="">State <span v-if="error_state" class="form-is-required">*required</span></label>
						<select name="" id="" v-model="form.state">
							<option :value="state" v-for="state in states" :key="state">{{state}}</option>
						</select>
					</div>
					<div class="d-form-item">
						<label for="">County <span v-if="error_county" class="form-is-required">*required</span></label>
						<input type="text" v-model="form.county">
					</div>
					<div class="d-form-item">
						<label for="">Country <span v-if="error_country" class="form-is-required">*required</span></label>
						<input type="text" v-model="form.country">
					</div>
					<div class="d-form-item submitform">
						<button v-on:click="submitForm();">Submit <span v-if="show_loading"><v-progress-circular indeterminate color="primary"></v-progress-circular></span></button>
						<div class="disclaimer-section">Disclaimer: Once you fill out this form, you are giving us permission to contact you and will send you emails about cyberbacker.</div>
					</div>
				</div>
				<div v-if="show_thank_you" class="d-main-form-inner thank-you-wrapper">
					<div class="d-thank-you-page">
						<h2>Congratulations for completing the first step!</h2>
						<div class="d-thank-you-content">
							<!-- <p>Please don't walk away from the tablet and expect a call shortly for your<br /><strong>Free Business Evaluation.</strong></p> -->
							<p>Please don't walk away from the tablet, one of our amazing growth backers will appear in the tablet shortly.</p>
						</div>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
import axios from 'axios'

export default {
	name: 'IndexPage',
	layout: "base",
	data(){
		return {
			show_other_industry: false,
			show_thank_you: false,
			show_loading: false,
			error_name: false,
			error_email: false,
			error_mobile: false,
			error_state: false,
			error_county: false,
			error_country: false,
			other_industry: '',
			form: {
				'name': '',
				'email': '',
				'mobile': '',
				'industry': '',
				'state': '',
				'county': '',
				'job_title': '',
				'country': '',
			},
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
	},
	methods: {
		submitForm(){
			console.log('process info -> ', this.form);
			this.show_loading = true;

			// validation
			let isHasError = false;
			this.error_name = false;
			this.error_email = false;
			this.error_mobile = false;
			this.error_state = false;
			this.error_county = false;
			this.error_country = false;

			if(this.form.name == ''){
				this.error_name = true;
				isHasError = true;
			}

			if(this.form.email == ''){
				this.error_email = true;
				isHasError = true;
			}

			if(this.form.mobile == ''){
				this.error_mobile = true;
				isHasError = true;
			}

			if(this.form.state == ''){
				this.error_state = true;
				isHasError = true;
			}

			if(this.form.county == ''){
				this.error_county = true;
				isHasError = true;
			}

			if(this.form.country == ''){
				this.error_country = true;
				isHasError = true;
			}

			if(isHasError){
				this.show_loading = false;
				return;
			}

			if(this.show_other_industry){
				this.form.industry = this.other_industry;
			}

			// console.log('all fields has been filled -> ', this.form);
			

			// get tab number
			let dselectedtab = this.$route.query.tablet;
			// console.log(dselectedtab);
			this.form.gsheet_id = "Tablet "+dselectedtab;

			axios.post("https://be2.applytocyberbacker.com/api/inman/savetogsheet", this.form)
    		.then((response) => {
				// console.log('saving response -> ', response);
				this.show_loading = false;
				this.show_thank_you = true;
			});
			
		},
		onIndustryChange(event){
			console.log(event.target.value)
			if(event.target.value == 'Other'){
				this.show_other_industry = true;
			} else {
				this.show_other_industry = false;
			}
		}
	},
	mounted() {  
		document.title = "Inman Connect Las Vegas 2022 | Cyberbacker";  
	}, 
}
</script>

<style scoped>
.d-main-content {
	font-family: 'Montserrat', sans-serif;
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
	margin-bottom: 40px;
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
    font-size: 130px;
    letter-spacing: -6px;
    line-height: .8em;
    transform: rotate(-4deg);
    text-shadow: 0 0 23px #a193fe;
    color: #e5e5e5;
}
.d-main-header-date {
	font-family: 'Square Peg', cursive;
	text-align: right;
    line-height: 1em;
    font-size: 85px;
    margin-top: -42px;
    position: relative;
    z-index: 2;
    color: #ffffff;
    text-shadow: 0 0 12px #434261;
    padding-right: 108px;
    margin-bottom: 50px;
    font-weight: bold;
	text-shadow: 0px 0px 9px #e010c5;
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
    /* font-weight: bold; */
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
	color: #fff;
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
.thank-you-wrapper {
	margin-bottom: 160px;
}
.d-thank-you-page h2 {
	text-align: center;
	font-size: 32px;
    margin-bottom: 30px;
}
.d-thank-you-content p {
	font-size: 22px;
    text-align: center;
    /* text-transform: capitalize; */
}
span.form-is-required {
    color: red;
    font-size: 14px;
    margin-left: 10px;
}
.disclaimer-section {
	font-size: 14px;
	margin-top: 20px;
}
@media only screen and (max-width: 690px) {
	.d-main-form {
		width: 100%;
	}
	.d-main-header-image img {
		width: 95%;
		margin: 0 auto;
	}
	.d-main-header-spring {
		padding: 0;
		text-align: center;
		font-size: 60px;
		margin-bottom: -15px;
	}
	.d-main-header-date {
		padding: 0;
		text-align: center;
		margin-top: -12px;
		font-size: 28px;
	}
	.d-main-header-mastermind {
		font-size: 54px;
	}
}
</style>
<template>
  <div>
  	<h1> Indian Place Geography</h1>
  	<div class="mainContainer">
  <input @input="changedValue" @keyup.enter="showDetail" v-model="zipCode" type="text" placeholder="Please enter area zip code">
  <p v-if="error">Could'nt get result, Please try again</p>
  <div v-if="state" class="container">
  	<div><span>Place Name -</span> {{placeName}}</div>
  	<div><span>State - </span>{{state}}</div>
  	<div><span>Longitude -</span> {{longitude}}</div>
  	<div><span>Latitude - </span>{{latitude}}</div>
  </div>
</div>
  </div>
</template>

<script>
export default {
  name: "Place",
  data:()=>({
  	zipCode:null,
  	placeName:null,
  	state:null,
  	longitude:null,
  	latitude:null, 
  	error:false,
  	



  }),
  methods:{
  	showDetail(){
  		var code = this.zipCode
  	
  		fetch(`http://api.zippopotam.us/IN/${code}`)
  		.then((response)=>{return response.json()})
  		.then((response) =>{
  			console.log(response)
        this.state = true
  			this.placeName = response.places[0]["place name"]
  			this.state = response.places[0].state
  			this.longitude = response.places[0].longitude
  			this.latitude = response.places[0].latitude

  		})
  		.catch((err)=>{
  			this.error = true
  			this.state = false
  		})
  	},
  	changedValue(){
  		this.error = false
  		this.state = false
  	}
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.mainContainer{
width:500px;
height: 500px;
background-color: white;
margin:auto;
}
.container>div{
	margin-bottom:  40px;
}
span{
	font-size: 20px;
	font-weight: bold;
}
p{
color:red;	
}
.container{
	margin-top: 40px;
}
input{
	width:200px;
	margin-top: 25px;
}




 
</style>

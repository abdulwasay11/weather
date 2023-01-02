<template>
<body>
  <div class="hello">
        <img id="img1" src="../assets/urlshort.jpg">
        <center>
          <h1>URL SHORTENER</h1>
        </center>
    <div>
     <div class="buttonIn">
       <div class="txt">
         <input type="text" id="enter" placeholder="Please Enter your Url..." v-model="api">
       </div>
       <div class="btn">
         <button  @click="shorturl()" id="clear">SHORT URL</button>
       </div>
    </div>
  </div>
  <br>
  <br>
  <center>
          <p>Your Short Url is:</p>
  </center>
   <a v-show="response" target="_blank" :href=response>{{response}}</a>
</div>
</body>

</template>

<script>
export default {
  name: 'HelloWorld',
  data(){
    return{
      api:'',
      response: ''
    }
  },
  props: {
    msg: String
  },


methods: {

  shorturl()
  {
    const url = new URL(
    "https://t.ly/api/v1/link/shorten"
);

const params = {
    "api_token": "bWe28hQGzcQraVsbs3cn2YP2Z9PJZgnzU4OaNDKR0rzMVNEmjqPhzGxHifpG",
};
Object.keys(params)
    .forEach(key => url.searchParams.append(key, params[key]));

const headers = {
    "Content-Type": "application/json",
    "Accept": "application/json",
};

let body = {
    "long_url": this.api,
    "include_qr_code": false
};

fetch(url, {
    method: "POST",
    headers,
    body: JSON.stringify(body),
}).then(response => response.json()).then((data)=>{ this.response=data.short_url})


}

}

};


</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>

body
{
  background-color: #8CAEEE;
}
	
	.buttonIn {
		width: 300px;
		position: relative;
	}
	
	input {
		margin-left: 215%;
    margin-top: 10%;
		padding: 0px;
		width: 100%;
		outline: none;
		height: 30px;
	}
  h1 {
    color: #36486b;
		padding: 0px;
		width: 100%;
		outline: none;
		height: 30px;
	}
	
	button {
    margin-right: -180%;
    margin-top: 25%;
		position: absolute;
		top: 0;
		border-radius: 5px;
		right: 0px;
		z-index: 2;
		border: none;
		top: 2px;
		height: 30px;
		cursor: pointer;
		color: white;
		background-color: #1e90ff;
		transform: translateX(2px);
	}

  a
  {
    border: 1px black solid;
    padding: 10px;
    border-radius: 10px;
    margin-left: 46%;
    margin-top: 50%;
    background-color: white;

  }
	
  #img1
  {
    margin-left: 40%;
  }

  p
  {
     color: #36486b;
     font-weight: bold;
  }


   #enter
  {
  
     font-weight: bold;
  }



  @media screen and (max-width: 1200px) {
     #img1
  {
    margin-left: 26%;
  }


}

</style>


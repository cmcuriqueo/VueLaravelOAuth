<template>
<div class="row">
	<div class="container">

      <form class="form-signin">
        <h2 class="form-signin-heading">Please sign in</h2>
        <label for="inputEmail" class="sr-only">Email address</label>
        <input v-model="email" type="email" id="inputEmail" class="form-control" placeholder="Email address" required autofocus>
        <label for="inputPassword" class="sr-only">Password</label>
        <input v-model="password" type="password" id="inputPassword" class="form-control" placeholder="Password" required>
        <div class="checkbox">
          <label>
            <input type="checkbox" value="remember-me"> Remember me
          </label>
        </div>
        <button @click = 'login' class="btn btn-lg btn-primary btn-block" type="submit">Sign in</button>
      </form>
    </div> <!-- /container -->
    
    </div>
</template>

<script>
	export default {
    data (){
      return {
        email: '',
        password: ''
      }
    },
    methods: {
      login () {
        var data = {
        client_id: 2,
        client_secret: 'wwuoZ8NutY73R2AvVB5oBdz3MUQke6SmnIN95Wzu',
        grant_type: 'password',
        username: this.email,
        password: this.password
      }

     this.$http.post("http://localhost:8000/oauth/token", data)
              .then(response => {
                this.$auth.setToken(response.body.access_token, response.body.expires_in + Date.now())
                this.$router.push("/feed")
              })
          // .then(function(response){
          //   console.log(response)
          // })
      }
    }
  }
</script>

<style></style>
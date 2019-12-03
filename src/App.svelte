<script>
  import Profile from "./Profile.svelte";

  import { auth } from "./firebase";
  import { authState } from "rxfire/auth";

  let user;
  const email = "emails@somecc.come";
  const password = "somepass";

  const unsubscribe = authState(auth).subscribe(u => (user = u));

  function register() {
    auth.createUserWithEmailAndPassword(email, password).catch(function(error) {
      // Handle Errors here.
      var errorCode = error.code;
      var errorMessage = error.message;
      // ...
    });
  }
</script>

<section>
  {#if user}
    <Profile />
    Now check your firebase for new user
    <hr />
  {:else}
    email: {email}
    <br />
    password: {password}
    <br />
    <button on:click={register}>Signup with Google</button>
  {/if}
</section>

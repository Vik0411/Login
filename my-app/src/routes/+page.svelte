<script>
      import user from '../user';
    let userCode ='';
    let password = '';
    let currentError = null;
    let errMsg = '';


// origin: 'http://10.2.2.10/AlbiScanner.stage/api/v1/login',

const login = ()=>{
    fetch('http://localhost:8010/proxy',{
        method: "POST",
        headers: {
    "Content-Type": "application/json",
  },
        body: JSON.stringify({userCode:userCode,password:password})
    })
    .then(res=>res.json())
    .then((data)=>{
        if((data?.messages?.length === 0) && !data?.errors){
            alert("U r logged in")
            console.log(data.user)
            user.update(val => val = {...data.user})

        }
            
            // we are handling an error with a message attribute, 
            // which only error object has (case when no entry is given)
            else if(data?.message){
            alert(data.errors[0].messages[0])
        } else {
        alert(data.messages[0].title + ". " + data.messages[0].content)
        }


        }
)
    .catch((error)=>{
        console.log("Error logging in:", error.message);
    })
}


// util to delete or use:

        // let dataMsg= data?.messages[0];
        // let dataErrs = data?.errors[0];

    //     if(dataMsg){
    //         alert(dataMsg.content)
    //     console.log(data.messages[0].content) // status 200
    // }else if(dataErrs) {
    //     errMsg = dataErrs.messages[0]
    //     console.log(data.errors[0].messages[0])  // status 401 or 422
    // } else {
    //     console.log("all ok") // status 200
    // }

</script>

<div style="display: flex; justify-content: center; flex-flow: column;">
<h3 style="text-align: center;">
    „Hra je jeden z nejefektivnějších způsobů, jak zjednodušit život.
  <br/>Přesně to jsme dělali jako děti, ale v dospělosti jsme si hrát
    zapomněli.“ A.E.
  </h3>
<form on:submit|preventDefault={login} style="text-align: center;">
    <div>
        <label for="userCode">Usercode</label>
        <input type="text" id="usercode" bind:value={userCode}/>
    </div>
    <div>
        <label for="password">Password</label>
        <input type="password" id="password" bind:value={password}/>
    </div>
    <button type='submit' style="text-align: center;">Submit</button>
</form>
</div>



<!-- <h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>
<p>hi</p> -->


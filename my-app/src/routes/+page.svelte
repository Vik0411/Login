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
    .then((res)=>{
        if(res.status < 299) return res.json()
        if(res.status > 299)
        return res.json()
    })
    .then((data)=>{
        if((data?.messages.length === 0) && !data?.errors){
            alert("U r logged in")}
            else if(data?.message){
            alert(data.errors[0].messages[0])
        } else {
        alert(data.messages[0].content)
        }
        }
        // if(data) user.update(val => val = {...data})
)
    .catch((error)=>{
        console.log("Error logging in:", error.message);
    })
}

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

<form on:submit|preventDefault={login}>
    <div>
        <label for="userCode">Usercode</label>
        <input type="text" id="usercode" bind:value={userCode}/>
    </div>
    <div>
        <label for="password">Password</label>
        <input type="password" id="password" bind:value={password}/>
    </div>
    <button type='submit'>Submit</button>

</form>


<!-- <h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>
<p>hi</p> -->


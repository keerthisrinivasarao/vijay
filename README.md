<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Signup Page</title>

<style>
*{
    margin:0;
    padding:0;
    box-sizing:border-box;
    font-family:Arial,sans-serif;
}

body{
    height:100vh;
    display:flex;
    justify-content:center;
    align-items:center;
    background:linear-gradient(135deg,#4facfe,#00f2fe);
}

.container{
    width:350px;
    background:#fff;
    padding:30px;
    border-radius:15px;
    box-shadow:0 5px 15px rgba(0,0,0,0.3);
}

h2{
    text-align:center;
    margin-bottom:20px;
    color:#333;
}

.input-box{
    margin-bottom:15px;
}

.input-box label{
    display:block;
    margin-bottom:5px;
    font-weight:bold;
}

.input-box input{
    width:100%;
    padding:12px;
    border:1px solid #ccc;
    border-radius:8px;
    outline:none;
}

.input-box input:focus{
    border-color:#4facfe;
}

button{
    width:100%;
    padding:12px;
    border:none;
    border-radius:8px;
    background:#4facfe;
    color:white;
    font-size:16px;
    cursor:pointer;
    transition:0.3s;
}

button:hover{
    background:#00c6fb;
}

#message{
    margin-top:15px;
    text-align:center;
    font-weight:bold;
}
</style>
</head>

<body>

<div class="container">

    <h2>Signup Form</h2>

    <div class="input-box">
        <label>Name</label>
        <input type="text" id="name" placeholder="Enter Name">
    </div>

    <div class="input-box">
        <label>Mobile Number</label>
        <input type="text" id="mobile" placeholder="Enter Mobile Number">
    </div>

    <div class="input-box">
        <label>Password</label>
        <input type="password" id="password" placeholder="Enter Password">
    </div>

    <button onclick="signup()">Signup</button>

    <div id="message"></div>

</div>

<script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js"></script>

<script>

const SUPABASE_URL = "https://paxhlgosqmjrbpualroy.supabase.co";
const SUPABASE_ANON_KEY = "sb_publishable_6JDa2H1RxowQaJhgI00YNQ_yCSiXPUK";

const supabaseClient = supabase.createClient(
    SUPABASE_URL,
    SUPABASE_ANON_KEY
);

async function signup(){

    let name = document.getElementById("name").value;
    let mobile = document.getElementById("mobile").value;
    let password = document.getElementById("password").value;

    if(name === "" || mobile === "" || password === ""){
        document.getElementById("message").innerHTML = "Fill all fields";
        document.getElementById("message").style.color = "red";
        return;
    }

    const { data, error } = await supabaseClient
    .from('users')
    .insert([
        {
            name: name,
            mobile: mobile,
            password: password
        }
    ]);

    if(error){
        document.getElementById("message").innerHTML = error.message;
        document.getElementById("message").style.color = "red";
    }
    else{
        document.getElementById("message").innerHTML = "Signup Successful";
        document.getElementById("message").style.color = "green";

        document.getElementById("name").value = "";
        document.getElementById("mobile").value = "";
        document.getElementById("password").value = "";
    }
}

</script>

</body>
</html>

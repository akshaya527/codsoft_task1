# codsoft_task1
This project is a multi-step Signup Flow UI for CodSoft internship. It uses HTML, CSS, and JavaScript to create a responsive and interactive registration experience with form validation, progress tracking, password strength indicator, and smooth step transitions. Includes clean UI design and mobile-friendly layout with modern styling and animations
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Mobile App Signup & Login Flow</title>

<style>
*{
    margin:0;
    padding:0;
    box-sizing:border-box;
    font-family:Arial, sans-serif;
}

body{
    background:#eef2ff;
    display:flex;
    justify-content:center;
    align-items:center;
    min-height:100vh;
}

.screen{
    display:none;
    width:380px;
    background:white;
    padding:30px;
    border-radius:20px;
    box-shadow:0 5px 15px rgba(0,0,0,0.15);
    text-align:center;
}

.active{
    display:block;
}

h1,h2{
    color:#6c63ff;
    margin-bottom:15px;
}

p{
    color:gray;
    margin-bottom:15px;
}

input{
    width:100%;
    padding:12px;
    margin:8px 0;
    border:1px solid #ddd;
    border-radius:8px;
    outline:none;
}

input:focus{
    border-color:#6c63ff;
}

button{
    width:100%;
    padding:12px;
    margin-top:10px;
    border:none;
    border-radius:8px;
    background:#6c63ff;
    color:white;
    font-size:16px;
    cursor:pointer;
}

button:hover{
    opacity:0.9;
}

.link{
    display:block;
    margin-top:15px;
    color:#6c63ff;
    cursor:pointer;
}

.rules{
    text-align:left;
    font-size:12px;
    color:#555;
    margin-top:10px;
    padding:10px;
    background:#f8f8f8;
    border-radius:8px;
}

.dashboard-btn{
    margin:8px 0;
}
</style>
</head>
<body>

<!-- Welcome Screen -->
<div class="screen active" id="welcome">
    <h1>Welcome</h1>
    <p>Create an account or login to continue.</p>

    <button onclick="showScreen('signup')">Sign Up</button>
    <button onclick="showScreen('login')">Login</button>
</div>

<!-- Signup Screen -->
<div class="screen" id="signup">
    <h2>Create Account</h2>

    <input type="text" id="signupName" placeholder="Full Name">

    <input type="email" id="signupEmail" placeholder="example@gmail.com">

    <input type="password" id="signupPassword" placeholder="Create Password">

    <div class="rules">
        <b>Password Requirements:</b><br>
        ✓ Minimum 8 characters<br>
        ✓ One uppercase letter (A-Z)<br>
        ✓ One lowercase letter (a-z)<br>
        ✓ One number (0-9)<br>
        ✓ One special character (@$!%*?&)
    </div>

    <button onclick="signUp()">Sign Up</button>

    <span class="link" onclick="showScreen('login')">
        Already have an account? Login
    </span>
</div>

<!-- Login Screen -->
<div class="screen" id="login">
    <h2>Login</h2>

    <input type="email" id="loginEmail" placeholder="Enter Email">

    <input type="password" id="loginPassword" placeholder="Enter Password">

    <button onclick="login()">Login</button>

    <span class="link" onclick="showScreen('signup')">
        Create New Account
    </span>
</div>

<!-- Dashboard Screen -->
<div class="screen" id="dashboard">
    <h2>Dashboard</h2>
    <p>Login Successful!</p>

    <button class="dashboard-btn">👤 Profile</button>
    <button class="dashboard-btn">📚 Courses</button>
    <button class="dashboard-btn">⚙️ Settings</button>
    <button class="dashboard-btn">🏆 Certificates</button>

    <button onclick="logout()">Logout</button>
</div>

<script>

// Screen Navigation
function showScreen(screenId){
    document.querySelectorAll('.screen').forEach(screen=>{
        screen.classList.remove('active');
    });

    document.getElementById(screenId).classList.add('active');
}

// Signup Function
function signUp(){

    let name = document.getElementById("signupName").value.trim();
    let email = document.getElementById("signupEmail").value.trim();
    let password = document.getElementById("signupPassword").value;

    let emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;

    let passwordPattern =
    /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[@$!%*?&]).{8,}$/;

    if(name === "" || email === "" || password === ""){
        alert("Please fill all fields.");
        return;
    }

    if(!emailPattern.test(email)){
        alert("Please enter a valid email address.");
        return;
    }

    if(!email.endsWith("@gmail.com")){
        alert("Only Gmail addresses are allowed.");
        return;
    }

    if(!passwordPattern.test(password)){
        alert(
            "Password must contain:\n\n" +
            "• Minimum 8 characters\n" +
            "• One uppercase letter\n" +
            "• One lowercase letter\n" +
            "• One number\n" +
            "• One special character (@$!%*?&)"
        );
        return;
    }

    localStorage.setItem("name", name);
    localStorage.setItem("email", email);
    localStorage.setItem("password", password);

    alert("Account Created Successfully!");
    showScreen("dashboard");
}

// Login Function
function login(){

    let email = document.getElementById("loginEmail").value.trim();
    let password = document.getElementById("loginPassword").value;

    let savedEmail = localStorage.getItem("email");
    let savedPassword = localStorage.getItem("password");

    if(email === savedEmail && password === savedPassword){
        alert("Login Successful!");
        showScreen("dashboard");
    }
    else{
        alert("Invalid Email or Password.");
    }
}

// Logout
function logout(){
    showScreen("welcome");
}

</script>

</body>
</html>

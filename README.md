<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>My Login Website</title>
  <style>
    * { box-sizing: border-box; }
    body {
      font-family: Arial, sans-serif;
      background: linear-gradient(to right, lightblue, black); /* ✅ light blue + black */
      margin: 0;
      display: flex;
      flex-direction: column;
      align-items: center;
      height: 100vh;
      overflow: hidden;
      color: white;
    }
    header {
      width: 100%;
      padding: 15px;
      text-align: center;
      background: #222;
      color: #00d4ff; /* ✅ cyan */
      font-size: 22px;
      font-weight: bold;
      letter-spacing: 1px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.7);
      position: fixed;
      top: 0;
      left: 0;
      z-index: 1000;
    }
    .container {
      background: #1e1e1e;
      border-radius: 10px;
      box-shadow: 0 14px 28px rgba(0,0,0,0.25),
                  0 10px 10px rgba(0,0,0,0.22);
      position: relative;
      overflow: hidden;
      width: 800px;
      max-width: 100%;
      min-height: 480px;
      margin-top: 80px;
    }
    .form-container {
      position: absolute;
      top: 0;
      height: 100%;
      transition: all 0.6s ease-in-out;
      width: 50%;
      background: #1e1e1e;
      display: flex;
      align-items: center;
      justify-content: center;
      color: white;
    }
    form {
      display: flex;
      flex-direction: column;
      padding: 0 50px;
      width: 100%;
      text-align: center;
    }
    input {
      background: #2c2c2c;
      border: none;
      padding: 12px 15px;
      margin: 8px 0;
      border-radius: 6px;
      color: white;
      font-size: 15px;
    }
    input::placeholder { color: #bbb; }

    /* ✅ Buttons */
    button {
      border-radius: 20px;
      border: none;
      font-size: 12px;
      font-weight: bold;
      padding: 12px 45px;
      margin-top: 10px;
      cursor: pointer;
      transition: background 0.3s;
    }
    /* Sign In / Sign Up buttons → Green */
    .form-container button {
      background: #28a745;
      color: white;
    }
    .form-container button:hover { background: #218838; }

    /* Logout button → Light Red */
    #home button {
      background: #ff6666;
      color: white;
    }
    #home button:hover { background: #e05555; }

    /* Error messages → Red */
    .message { color: red; font-size: 14px; }

    .sign-in-container { left: 0; z-index: 2; }
    .container.right-panel-active .sign-in-container { transform: translateX(100%); }
    .sign-up-container { left: 0; opacity: 0; z-index: 1; }
    .container.right-panel-active .sign-up-container {
      transform: translateX(100%);
      opacity: 1;
      z-index: 5;
      animation: show 0.6s;
    }
    @keyframes show {
      0%,49.99% { opacity: 0; z-index: 1; }
      50%,100% { opacity: 1; z-index: 5; }
    }
    .overlay-container {
      position: absolute;
      top: 0; left: 50%;
      width: 50%; height: 100%;
      overflow: hidden;
      transition: transform 0.6s ease-in-out;
      z-index: 100;
    }
    .container.right-panel-active .overlay-container { transform: translateX(-100%); }
    .overlay {
      background: linear-gradient(to right, lightblue, black); /* ✅ updated overlay colors */
      color: #fff;
      position: relative;
      left: -100%; height: 100%; width: 200%;
      transform: translateX(0);
      transition: transform 0.6s ease-in-out;
    }
    .container.right-panel-active .overlay { transform: translateX(50%); }
    .overlay-panel {
      position: absolute;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      padding: 0 40px;
      text-align: center;
      top: 0; height: 100%; width: 50%;
    }
    .overlay-left { transform: translateX(-20%); left: 0; }
    .container.right-panel-active .overlay-left { transform: translateX(0); }
    .overlay-right { right: 0; }
    .container.right-panel-active .overlay-right { transform: translateX(20%); }

    #home {
      background: #1e1e1e;
      text-align: center;
      border-radius: 10px;
      padding: 20px;
      margin-top: 80px;
      width: 800px;
      display: none;
    }
    iframe {
      width: 100%;
      height: 400px;
      border: none;
      border-radius: 8px;
      margin-top: 15px;
    }
  </style>
</head>
<body>
<header>🌐 Login For Website</header>

<div class="container" id="container">
  <!-- Sign Up -->
  <div class="form-container sign-up-container">
    <form id="signupForm">
      <h1>Create Account</h1>
      <input type="text" placeholder="Full Name" id="name">
      <input type="email" placeholder="Email" id="email">
      <input type="text" placeholder="Phone Number" id="number">
      <input type="password" placeholder="Create Password" id="password">
      <input type="password" placeholder="Re-enter Password" id="confirm">
      <p class="message" id="msg1"></p>
      <button type="button" onclick="signup()">Sign Up</button>
    </form>
  </div>

  <!-- Sign In -->
  <div class="form-container sign-in-container">
    <form id="signinForm">
      <h1>Sign in</h1>
      <input type="text" placeholder="Full Name" id="loginName">
      <input type="text" placeholder="Phone Number" id="loginNumber">
      <input type="password" placeholder="Password" id="loginPass">
      <p class="message" id="msg2"></p>
      <button type="button" onclick="signin()">Sign In</button>
    </form>
  </div>

  <!-- Overlay -->
  <div class="overlay-container">
    <div class="overlay">
      <div class="overlay-panel overlay-left">
        <h1>Welcome Back!</h1>
        <p>To keep connected with us please login with your personal info</p>
        <button class="ghost" id="signIn">Sign In</button>
      </div>
      <div class="overlay-panel overlay-right">
        <h1>Hello, Friend!</h1>
        <p>Enter your details and start journey with us</p>
        <button class="ghost" id="signUp">Sign Up</button>
      </div>
    </div>
  </div>
</div>

<!-- Home Screen -->
<div id="home">
  <h2>✅ Logged in successfully!</h2>
  <p id="welcomeUser"></p>
  <iframe src="https://www.wikipedia.org"></iframe>
  <button onclick="logout()">Logout</button>
</div>

<script>
  const signUpButton = document.getElementById('signUp');
  const signInButton = document.getElementById('signIn');
  const container = document.getElementById('container');

  signUpButton.addEventListener('click', () => container.classList.add("right-panel-active"));
  signInButton.addEventListener('click', () => container.classList.remove("right-panel-active"));

  // Auto-login check
  window.onload = function() {
    if (localStorage.getItem("isLoggedIn") === "true") {
      showHome();
    }
  };

  function signup() {
    const name = document.getElementById("name").value.trim();
    const number = document.getElementById("number").value.trim();
    const email = document.getElementById("email").value.trim();
    const pass = document.getElementById("password").value;
    const confirm = document.getElementById("confirm").value;
    const msg = document.getElementById("msg1");

    const phonePattern = /^\d{10}$/;
    const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;

    if (!name || !number || !email || !pass || !confirm) {
      msg.textContent = "All fields are required!";
    } else if (!phonePattern.test(number)) {
      msg.textContent = "Enter valid 10-digit number!";
    } else if (!emailPattern.test(email)) {
      msg.textContent = "Enter a valid email address!";
    } else if (pass !== confirm) {
      msg.textContent = "Passwords do not match!";
    } else {
      localStorage.setItem("name", name);
      localStorage.setItem("number", number);
      localStorage.setItem("email", email);
      localStorage.setItem("pass", pass);
      msg.textContent = "";
      alert("Sign Up successful! Please Sign In.");
      container.classList.remove("right-panel-active"); // go to sign in
    }
  }

  function signin() {
    const name = document.getElementById("loginName").value.trim();
    const number = document.getElementById("loginNumber").value.trim();
    const pass = document.getElementById("loginPass").value;
    const msg = document.getElementById("msg2");

    if (name === localStorage.getItem("name") &&
        number === localStorage.getItem("number") &&
        pass === localStorage.getItem("pass")) {
      msg.textContent = "";
      localStorage.setItem("isLoggedIn", "true");
      showHome();
    } else {
      msg.textContent = "Something is Invalid!";
    }
  }

  function showHome() {
    document.getElementById("container").style.display = "none";
    document.getElementById("home").style.display = "block";
    document.getElementById("welcomeUser").textContent =
      "Welcome, " + localStorage.getItem("name") + "!";
  }

  function logout() {
    localStorage.setItem("isLoggedIn", "false");
    document.getElementById("home").style.display = "none";
    document.getElementById("container").style.display = "block";
    document.getElementById("signinForm").reset();
  }
</script>
</body>
</html>
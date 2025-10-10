<!DOCTYPE html>
<html>
<head>
  <title>Pay & Park - Kolhapur</title>
  <style>
    body {
      background-color: #f0f8ff;
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      text-align: center;
    }
    h2 { color: #333; }

    /* Cards */
    .card, .parking-card {
      background-color: white;
      padding: 20px;
      border-radius: 12px;
      box-shadow: 0px 4px 8px rgba(0,0,0,0.2);
      margin: 15px auto;
      width: 320px;
      text-align: left;
    }
    .parking-card h3 { margin: 0 0 10px; color: #4CAF50; }
    .parking-card p { margin: 5px 0; color: #555; }

    /* Parking slots */
    .slot-container {
      display: grid;
      grid-template-columns: repeat(10, 1fr);
      gap: 10px;
      justify-content: center;
      margin-top: 20px;
    }
    .slot {
      width: 50px;
      height: 50px;
      border-radius: 8px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 14px;
      cursor: pointer;
      background-color: #4CAF50;
      color: white;
      transition: 0.3s;
    }
    .slot.booked { background-color: #f44336; }
    .slot.selected { background-color: #2196F3; }

    /* Legend */
    .legend {
      margin-top: 15px;
      font-size: 15px;
      background: #fff;
      border-radius: 8px;
      padding: 10px;
      width: fit-content;
      margin-left: auto;
      margin-right: auto;
      box-shadow: 0px 4px 6px rgba(0,0,0,0.2);
    }
    .legend div { margin: 5px; text-align: left; }
    .legend span {
      display: inline-block;
      width: 20px;
      height: 20px;
      border-radius: 4px;
      margin-right: 8px;
    }
    .green { background-color: #4CAF50; }
    .red { background-color: #f44336; }
    .blue { background-color: #2196F3; }

    /* Login Page */
    .login-container {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      background: linear-gradient(135deg, #4CAF50, #2196F3);
    }
    .login-card {
      background: #fff;
      padding: 30px;
      border-radius: 16px;
      box-shadow: 0px 8px 20px rgba(0,0,0,0.25);
      width: 350px;
      text-align: center;
      animation: fadeIn 1s ease-in-out;
    }
    .login-card h2 { margin-bottom: 10px; color: #333; }
    .login-card .subtitle { margin-bottom: 20px; font-size: 14px; color: #666; }
    .input-group {
      display: flex;
      align-items: center;
      background: #f1f1f1;
      border-radius: 8px;
      padding: 10px;
      margin-bottom: 15px;
    }
    .input-group span { font-size: 18px; margin-right: 8px; }
    .input-group input {
      border: none;
      outline: none;
      background: transparent;
      flex: 1;
      font-size: 14px;
    }
    input[type="submit"], input[type="reset"], button {
      padding: 12px;
      width: 48%;
      margin: 5px 1%;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      font-size: 15px;
      transition: 0.3s;
      color: white;
    }
    input[type="submit"] { background-color: #4CAF50; }
    input[type="submit"]:hover { background-color: #45a049; transform: scale(1.05); }
    input[type="reset"] { background-color: #f44336; }
    input[type="reset"]:hover { background-color: #d32f2f; transform: scale(1.05); }

    /* Dashboard */
    .dashboard {
      margin: 30px auto;
      width: 350px;
      background: white;
      padding: 20px;
      border-radius: 15px;
      box-shadow: 0 4px 8px rgba(0,0,0,0.2);
    }
    .dashboard h2 { margin-bottom: 20px; }
    .detail { text-align: left; margin: 10px 0; font-size: 16px; }
    .detail span { font-weight: bold; color: #0077b6; }

    /* Animation */
    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(-20px); }
      to { opacity: 1; transform: translateY(0); }
    }
  </style>
</head>
<body>

<!-- Login -->
<div id="loginPage" class="login-container">
  <div class="login-card">
    <h2>🚗 Pay & Park - Kolhapur</h2>
    <p class="subtitle">Login to manage your parking</p>
    <form onsubmit="return loginUser()">
      <div class="input-group">
        <span>👤</span>
        <input type="text" id="username" placeholder="Enter Username" required>
      </div>
      <div class="input-group">
        <span>🔑</span>
        <input type="password" id="password" placeholder="Enter Password" required>
      </div>
      <input type="submit" value="Login">
      <input type="reset" value="Clear">
    </form>
  </div>
</div>

<!-- Parking Page -->
<div id="parkingPage" style="display: none;">
  <h2>Welcome, <span id="currentUser"></span></h2>
  <h3>Pay & Park Locations in Kolhapur</h3>
  <div class="parking-card" onclick="openSlots('Shahu Market Pay & Park')">
    <h3>Shahu Market Pay & Park</h3>
    <p>📍 Near Central Bus Stand</p>
    <p>💰 ₹20 per hour</p>
  </div>
  <div class="parking-card" onclick="openSlots('Rankala Lake Parking')">
    <h3>Rankala Lake Parking</h3>
    <p>📍 Rankala Lake Main Gate</p>
    <p>💰 ₹30 for 2 hours</p>
  </div>
  <div class="parking-card" onclick="openSlots('DYP Mall Parking')">
    <h3>DYP Mall Parking</h3>
    <p>📍 Shahupuri</p>
    <p>💰 ₹40 for 3 hours</p>
  </div>
  <div class="parking-card" onclick="openSlots('Kolhapur Railway Station Parking')">
    <h3>Kolhapur Railway Station Parking</h3>
    <p>📍 Near Railway Station</p>
    <p>💰 ₹25 per hour</p>
  </div>
  <button onclick="logoutUser()">Logout</button>
</div>

<!-- Slot Page -->
<div id="slotPage" style="display: none;">
  <h2 id="parkingTitle"></h2>
  <div class="slot-container" id="slots"></div>
  <div class="legend">
    <div><span class="green"></span> 🟢 Available</div>
    <div><span class="red"></span> 🔴 Booked</div>
    <div><span class="blue"></span> 🔵 Selected</div>
  </div>
  <br>
  <button onclick="backToParking()">⬅ Back</button>
  <button onclick="logoutUser()">Logout</button>
</div>

<!-- Dashboard -->
<div id="dashboardPage" style="display: none;">
  <div class="dashboard">
    <h2>User Booking Details</h2>
    <div class="detail">Name: <span id="dashName"></span></div>
    <div class="detail">Car Number: <span id="dashCar"></span></div>
    <div class="detail">Booked Slot No: <span id="dashSlot"></span></div>
    <button onclick="backToParking()">⬅ Back</button>
    <button onclick="logoutUser()">Logout</button>
  </div>
</div>

<script>
  const users = {
    "Parth": "parth@123",
    "Kshitija": "kshitija@123",
    "Shravan": "shravan@123",
    "Samiksha": "Samiksha@123",
    "Arpita": "arpita@1234",
    "admin": "1234"
  };

  let currentUser = "";
  let bookedSlots = JSON.parse(localStorage.getItem("bookedSlots")) || {
    "Shahu Market Pay & Park": [],
    "Rankala Lake Parking": [],
    "DYP Mall Parking": [],
    "Kolhapur Railway Station Parking": []
  };

  function saveBookings() {
    localStorage.setItem("bookedSlots", JSON.stringify(bookedSlots));
  }

  function loginUser() {
    let user = document.getElementById("username").value.trim();
    let pass = document.getElementById("password").value.trim();

    if(users[user] && users[user] === pass) {
      currentUser = user;
      document.getElementById("loginPage").style.display = "none";
      document.getElementById("parkingPage").style.display = "block";
      document.getElementById("currentUser").innerText = user;
    } else {
      alert("Invalid username or password!");
    }
    return false;
  }

  function logoutUser() {
    currentUser = "";
    document.getElementById("slotPage").style.display = "none";
    document.getElementById("parkingPage").style.display = "none";
    document.getElementById("dashboardPage").style.display = "none";
    document.getElementById("loginPage").style.display = "flex";
  }

  function openSlots(parkingName) {
    document.getElementById("parkingPage").style.display = "none";
    document.getElementById("slotPage").style.display = "block";
    document.getElementById("parkingTitle").innerText = parkingName + " - Select a Slot";

    let container = document.getElementById("slots");
    container.innerHTML = "";

    for(let i=1; i<=100; i++) {
      let div = document.createElement("div");
      div.className = "slot";
      div.innerText = i;

      if(bookedSlots[parkingName].includes(i)) {
        div.classList.add("booked");
      }

      div.onclick = function() {
        if(div.classList.contains("booked")) {
          if(confirm("Un-book slot " + i + " at " + parkingName + "?")) {
            div.classList.remove("booked");
            bookedSlots[parkingName] = bookedSlots[parkingName].filter(slot => slot !== i);
            saveBookings();
            alert("Slot " + i + " has been un-booked.");
          }
        } else {
          let carNumber = prompt("Enter your Car Number:");
          if(carNumber) {
            div.classList.add("booked");
            bookedSlots[parkingName].push(i);
            saveBookings();
            showDashboard(currentUser, carNumber, i);
            alert("Slot " + i + " booked successfully!");
          }
        }
      }
      container.appendChild(div);
    }
  }

  function showDashboard(name, car, slot) {
    document.getElementById("slotPage").style.display = "none";
    document.getElementById("dashboardPage").style.display = "block";
    document.getElementById("dashName").innerText = name;
    document.getElementById("dashCar").innerText = car;
    document.getElementById("dashSlot").innerText = slot;
  }

  function backToParking() {
    document.getElementById("slotPage").style.display = "none";
    document.getElementById("dashboardPage").style.display = "none";
    document.getElementById("parkingPage").style.display = "block";
  }
</script>
</body>
</html>

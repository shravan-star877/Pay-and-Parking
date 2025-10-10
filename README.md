<!DOCTYPE html>
<html>
<head>
  <title>Pay & Park - Kolhapur</title>
  <style>
    body {
      margin: 0;
      font-family: 'Arial', sans-serif;
      background-color: #f0f8ff;
    }

    h2, h3 { color: #333; }

    /* ✨ LOGIN PAGE with background slideshow */
    .login-container {
      position: relative;
      height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      overflow: hidden;
    }

    /* Background Slideshow */
    .bg-slideshow {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-size: cover;
      background-position: center;
      animation: slideShow 25s infinite;
      z-index: -2;
    }

    @keyframes slideShow {
      0% {
        background-image: url('https://images.unsplash.com/photo-1525609004556-c46c7d6cf023?auto=format&fit=crop&w=1600&q=80');
      }
      25% {
        background-image: url('https://images.unsplash.com/photo-1503376780353-7e6692767b70?auto=format&fit=crop&w=1600&q=80');
      }
      50% {
        background-image: url('https://images.unsplash.com/photo-1502877338535-766e1452684a?auto=format&fit=crop&w=1600&q=80');
      }
      75% {
        background-image: url('https://images.unsplash.com/photo-1525609004556-c46c7d6cf023?auto=format&fit=crop&w=1600&q=80');
      }
      100% {
        background-image: url('https://images.unsplash.com/photo-1503376780353-7e6692767b70?auto=format&fit=crop&w=1600&q=80');
      }
    }

    /* Dark overlay */
    .login-overlay {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: linear-gradient(rgba(0, 0, 0, 0.6), rgba(0, 0, 0, 0.5));
      backdrop-filter: blur(4px);
      z-index: -1;
    }

    /* Login card - glass effect */
    .login-card {
      background: rgba(255, 255, 255, 0.15);
      backdrop-filter: blur(14px);
      padding: 35px 25px;
      border-radius: 20px;
      width: 330px;
      text-align: center;
      color: white;
      box-shadow: 0 8px 25px rgba(0,0,0,0.4);
      animation: fadeIn 1.2s ease-in-out;
    }
    .login-card h2 {
      margin-bottom: 10px;
      font-size: 24px;
    }
    .login-card .subtitle {
      font-size: 14px;
      margin-bottom: 20px;
      color: #ddd;
    }

    .input-group {
      display: flex;
      align-items: center;
      background: rgba(255,255,255,0.2);
      border-radius: 8px;
      padding: 10px;
      margin-bottom: 15px;
    }
    .input-group span {
      font-size: 18px;
      margin-right: 8px;
    }
    .input-group input {
      border: none;
      outline: none;
      background: transparent;
      flex: 1;
      font-size: 14px;
      color: white;
    }
    .input-group input::placeholder {
      color: #eee;
    }

    input[type="submit"], input[type="reset"] {
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
    input[type="submit"] {
      background: linear-gradient(135deg, #4CAF50, #2196F3);
    }
    input[type="submit"]:hover {
      transform: scale(1.05);
    }
    input[type="reset"] {
      background: rgba(255,255,255,0.3);
    }
    input[type="reset"]:hover {
      background: rgba(255,255,255,0.5);
      transform: scale(1.05);
    }

    /* Parking Header */
    .parking-header {
      background: linear-gradient(135deg, #2196F3, #4CAF50);
      color: white;
      text-align: center;
      padding: 30px 10px;
      border-bottom-left-radius: 50px;
      border-bottom-right-radius: 50px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.2);
    }

    /* Parking Cards Grid */
    .parking-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
      gap: 20px;
      padding: 30px;
      max-width: 1000px;
      margin: 0 auto;
    }
    .parking-card {
      background-color: white;
      border-radius: 15px;
      box-shadow: 0 4px 8px rgba(0,0,0,0.2);
      cursor: pointer;
      overflow: hidden;
      transition: transform 0.3s, box-shadow 0.3s;
    }
    .parking-card:hover {
      transform: translateY(-8px);
      box-shadow: 0 10px 15px rgba(0,0,0,0.3);
    }
    .parking-card img {
      width: 100%;
      height: 180px;
      object-fit: cover;
    }
    .parking-card .info {
      padding: 15px;
      text-align: left;
    }
    .parking-card .info h3 {
      margin: 0 0 8px;
      color: #4CAF50;
    }
    .parking-card .info p {
      margin: 4px 0;
      color: #555;
      font-size: 14px;
    }

    /* Slot Page */
    .slot-container {
      display: grid;
      grid-template-columns: repeat(10, 1fr);
      gap: 10px;
      justify-content: center;
      margin-top: 20px;
      padding: 0 20px;
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

    /* Dashboard */
    .dashboard {
      margin: 30px auto;
      width: 350px;
      background: white;
      padding: 20px;
      border-radius: 15px;
      box-shadow: 0 4px 8px rgba(0,0,0,0.2);
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(-20px); }
      to { opacity: 1; transform: translateY(0); }
    }
  </style>
</head>
<body>

<!-- LOGIN PAGE -->
<div id="loginPage" class="login-container">
  <div class="bg-slideshow"></div>
  <div class="login-overlay"></div>

  <div class="login-card">
    <h2>🚗 Pay & Park - Kolhapur</h2>
    <p class="subtitle">Login to manage your parking easily</p>
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

<!-- PARKING PAGE -->
<div id="parkingPage" style="display: none;">
  <div class="parking-header">
    <h2>Welcome, <span id="currentUser"></span> 👋</h2>
    <p>Select a Pay & Park location below to book your slot.</p>
  </div>

  <div class="parking-grid">
    <div class="parking-card" onclick="openSlots('Shahu Market Pay & Park')">
      <img src="https://images.unsplash.com/photo-1517142089942-ba376ce32a2e?auto=format&fit=crop&w=800&q=60" alt="Shahu Market Parking">
      <div class="info">
        <h3>Shahu Market Pay & Park</h3>
        <p>📍 Near Central Bus Stand</p>
        <p>💰 ₹20 per hour</p>
      </div>
    </div>

    <div class="parking-card" onclick="openSlots('Rankala Lake Parking')">
      <img src="https://images.unsplash.com/photo-1525609004556-c46c7d6cf023?auto=format&fit=crop&w=800&q=60" alt="Rankala Lake Parking">
      <div class="info">
        <h3>Rankala Lake Parking</h3>
        <p>📍 Rankala Lake Main Gate</p>
        <p>💰 ₹30 for 2 hours</p>
      </div>
    </div>

    <div class="parking-card" onclick="openSlots('DYP Mall Parking')">
      <img src="https://images.unsplash.com/photo-1503376780353-7e6692767b70?auto=format&fit=crop&w=800&q=60" alt="DYP Mall Parking">
      <div class="info">
        <h3>DYP Mall Parking</h3>
        <p>📍 Shahupuri</p>
        <p>💰 ₹40 for 3 hours</p>
      </div>
    </div>
  </div>

  <div style="text-align:center; margin-bottom:30px;">
    <button onclick="logoutUser()">Logout</button>
  </div>
</div>

<!-- SLOT PAGE -->
<div id="slotPage" style="display: none;">
  <h2 id="parkingTitle" style="text-align:center; margin-top:20px;"></h2>
  <div class="slot-container" id="slots"></div>
  <div class="legend">
    <div><span class="green"></span> 🟢 Available</div>
    <div><span class="red"></span> 🔴 Booked</div>
    <div><span class="blue"></span> 🔵 Selected</div>
  </div>
  <br>
  <div style="text-align:center;">
    <button onclick="backToParking()">⬅ Back</button>
    <button onclick="logoutUser()">Logout</button>
  </div>
</div>

<!-- DASHBOARD -->
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
    "DYP Mall Parking": []
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

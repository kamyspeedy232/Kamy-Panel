<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>GameZone - UPI Payment</title>
  <link rel="stylesheet" href="style.css" />
  <script src="https://cdn.jsdelivr.net/npm/qrcode/build/qrcode.min.js"></script>
</head>
<body>
  <div class="panel">
    <header>
      <h1>GameZone</h1>
      <div class="user-info">
        <img src="https://via.placeholder.com/40" alt="Avatar" />
        <span>Player123</span>
      </div>
    </header>

    <section class="store">
      <h2>Buy In-Game Items</h2>
      <div class="items">
        <div class="item" onclick="selectItem('Gold Pack', 49)">
          <h3>Gold Pack</h3>
          <p>500 Gold</p>
          <span>₹49</span>
        </div>
        <div class="item" onclick="selectItem('Battle Pass', 99)">
          <h3>Battle Pass</h3>
          <p>Seasonal Access</p>
          <span>₹99</span>
        </div>
        <div class="item" onclick="selectItem('Mega Bundle', 149)">
          <h3>Mega Bundle</h3>
          <p>1000 Gold + Skins</p>
          <span>₹149</span>
        </div>
      </div>
    </section>

    <section class="payment">
      <h2>Pay via UPI</h2>
      <p id="selectedItem">No item selected</p>
      <div id="qrCodeContainer" class="qr-container"></div>
      <small>Scan with Google Pay, PhonePe, Paytm, or any UPI app</small>
    </section>

    <footer>
      <small>Need help? <a href="#">Contact Support</a></small>
    </footer>
  </div>

  <script src="script.js"></script>
</body>
</html>
body {
  font-family: Arial, sans-serif;
  background-color: #111;
  color: #fff;
  margin: 0;
  padding: 0;
}

.panel {
  max-width: 600px;
  margin: auto;
  padding: 20px;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.user-info {
  display: flex;
  align-items: center;
}

.user-info img {
  border-radius: 50%;
  margin-right: 10px;
}

.store .items {
  display: flex;
  flex-direction: column;
  gap: 15px;
  margin-top: 20px;
}

.item {
  background-color: #222;
  padding: 15px;
  border: 1px solid #444;
  cursor: pointer;
  transition: background 0.3s;
}

.item:hover {
  background-color: #333;
}

.payment {
  margin-top: 30px;
}

.qr-container canvas {
  margin-top: 15px;
  width: 200px;
  height: 200px;
  border: 2px solid #444;
}

footer {
  text-align: center;
  margin-top: 40px;
  font-size: 0.9em;
}
let selectedItem = null;
let selectedPrice = 0;

function selectItem(name, price) {
  selectedItem = name;
  selectedPrice = price;
  document.getElementById("selectedItem").innerText = `${name} - ₹${price}`;

  const upiId = "8887979276@ptsbi"; // <-- Replace with your real UPI ID
  const upiUrl = `upi://pay?pa=${upiId}&pn=GameZone&am=${price}&cu=INR&tn=Purchase%20of%20${encodeURIComponent(name)}`;

  QRCode.toCanvas(document.createElement("canvas"), upiUrl, function (err, canvas) {
    if (err) {
      console.error(err);
      return;
    }
    const qrContainer = document.getElementById("qrCodeContainer");
    qrContainer.innerHTML = "";
    qrContainer.appendChild(canvas);
  });
}

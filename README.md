<!DOCTYPE html>
<html>
<head>
<title>Top Up Game</title>
<script src="https://app.sandbox.midtrans.com/snap/snap.js"
data-client-key="ISI_CLIENT_KEY_KAMU"></script>
</head>
<body>

<input id="user_id" placeholder="ID Game">
<input id="server" placeholder="Server">
<button onclick="cekID()">Cek ID</button>
<p id="nick"></p>

<button onclick="bayar()">Bayar</button>

<script>
function cekID(){
 fetch("api/cek_id.php?user_id="+user_id.value)
 .then(r=>r.json())
 .then(d=>{
   nick.innerText = d.status ? "Nick: "+d.nickname : "ID Salah";
 });
}

function bayar(){
 fetch("api/create_transaction.php",{
  method:"POST",
  headers:{'Content-Type':'application/json'},
  body:JSON.stringify({
    game:"Mobile Legends",
    user_id:user_id.value,
    server:server.value,
    nominal:"86 Diamond",
    harga:20000
  })
 })
 .then(r=>r.json())
 .then(d=>{
   snap.pay(d.token);
 });
}
</script>

</body>
</html>

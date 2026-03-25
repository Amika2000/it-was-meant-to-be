<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>It was meant to be...</title>

<style>
body {
  background: white;
  font-family: "Georgia", serif;
  text-align: center;
  margin-top: 80px;
  color: black;
}

h1 {
  font-size: 36px;
  margin-bottom: 10px;
}

input {
  padding: 15px;
  width: 300px;
  font-size: 18px;
  border: 1px solid black;
}

.result {
  margin-top: 30px;
  font-size: 22px;
}
</style>
</head>

<body>

<h1>Find Your Table</h1>
<p>Please enter your name below</p>

<input type="text" id="search" placeholder="Type your name here">

<div class="result" id="result"></div>

<script>
fetch("guests.csv")
.then(res => res.text())
.then(data => {
  const rows = data.split("\n").slice(1);
  const guests = rows.map(r => {
    const [name, table] = r.split(",");
    return {name: name.toLowerCase(), table};
  });

  document.getElementById("search").addEventListener("input", e => {
    const value = e.target.value.toLowerCase();

    const match = guests.find(g => g.name.includes(value));

    if(match){
      document.getElementById("result").innerHTML =
        match.name.toUpperCase() + "<br>Table " + match.table;
    } else {
      document.getElementById("result").innerHTML = "";
    }
  });
});
</script>

</body>
</html>

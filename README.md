<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Blox Fruits - Wiki Complet Mobile</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap');

body {
  font-family: 'Press Start 2P', cursive;
  background: url('https://i.imgur.com/ZXqKXkL.jpg') no-repeat center center fixed;
  background-size: cover;
  margin: 0;
  padding: 0;
  color: #fff;
}

header {
  background: rgba(0,0,0,0.7);
  padding: 20px;
  text-align: center;
  font-size: 1.5em;
  color: #ffcc00;
  text-shadow: 2px 2px 6px #000;
}

main {
  padding: 10px;
  max-width: 100%;
  margin: auto;
  backdrop-filter: blur(6px);
  background: rgba(0,0,0,0.5);
  border-radius: 10px;
  overflow-x: auto;
  -webkit-overflow-scrolling: touch;
}

input, select {
  width: 100%;
  padding: 8px;
  margin: 5px 0;
  border-radius: 5px;
  border: none;
  font-family: inherit;
  font-size: 0.7em;
}

table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 10px;
  font-size: 0.75em;
}

th, td {
  padding: 8px;
  text-align: left;
  border-bottom: 1px solid #444;
  transition: all 0.2s ease;
}

th {
  background-color: rgba(30,30,30,0.9);
  cursor: pointer;
}

td img {
  width: 40px;
  height: 40px;
  vertical-align: middle;
  margin-right: 10px;
  transition: transform 0.2s ease;
}

td img:hover {
  transform: scale(1.15) rotate(10deg);
}

/* Glow selon rareté */
.rare { color: #ff4d4d; font-weight: bold; }
.legendary { color: #00e5ff; font-weight: bold; text-shadow: 0 0 10px #00e5ff; }
.mythical { color: #ffcc00; font-weight: bold; text-shadow: 0 0 8px #ffcc00; }

/* Fond type */
.Combat { background: linear-gradient(90deg, rgba(255,100,100,0.2), rgba(255,50,50,0.2)); }
.Défense { background: linear-gradient(90deg, rgba(100,150,255,0.2), rgba(50,100,255,0.2)); }
.Soutien { background: linear-gradient(90deg, rgba(100,255,100,0.2), rgba(50,200,50,0.2)); }
.Élémentaire { background: linear-gradient(90deg, rgba(255,180,100,0.2), rgba(255,150,50,0.2)); }
.Bête { background: linear-gradient(90deg, rgba(165,105,50,0.2), rgba(120,70,30,0.2)); }
.Naturel { background: linear-gradient(90deg, rgba(200,200,200,0.2), rgba(150,150,150,0.2)); }

/* Optimisation mobile */
@media (max-width: 768px){
  td img { display: none; }
  table { font-size: 0.65em; }
}
</style>
</head>
<body>

<header>Blox Fruits - Wiki Mobile</header>

<main>
<input type="text" id="searchInput" placeholder="Rechercher un fruit...">
<select id="typeFilter">
  <option value="all">Tous les types</option>
  <option value="Combat">Combat</option>
  <option value="Défense">Défense</option>
  <option value="Soutien">Soutien</option>
  <option value="Élémentaire">Élémentaire</option>
  <option value="Bête">Bête</option>
  <option value="Naturel">Naturel</option>
</select>

<table id="fruitsTable">
<thead>
<tr>
  <th onclick="sortTable(0)">Fruit ⬍</th>
  <th onclick="sortTable(1)">Type ⬍</th>
  <th onclick="sortTable(2)">Prix (Robux) ⬍</th>
</tr>
</thead>
<tbody>
<!-- Exemple fruits (tu peux ajouter les 39+ fruits officiels) -->
<tr class="Combat rare"><td><img src="https://i.imgur.com/abcd123.png" alt="Rocket" loading="lazy">🍏 Rocket</td><td>Combat</td><td>10</td></tr>
<tr class="Naturel rare"><td><img src="https://i.imgur.com/abcd124.png" alt="Spin" loading="lazy">🌪️ Spin</td><td>Naturel</td><td>15</td></tr>
<tr class="Élémentaire rare"><td><img src="https://i.imgur.com/abcd125.png" alt="Smoke" loading="lazy">💨 Smoke</td><td>Élémentaire</td><td>25</td></tr>
<tr class="Bête legendary"><td><img src="https://i.imgur.com/abcd126.png" alt="Phoenix" loading="lazy">🔥 Phoenix</td><td>Bête</td><td>550</td></tr>
<tr class="Naturel mythical"><td><img src="https://i.imgur.com/abcd127.png" alt="Gravity" loading="lazy">🪐 Gravity</td><td>Naturel</td><td>1200</td></tr>
<!-- Continue à ajouter les autres fruits ici de la même manière -->
</tbody>
</table>
</main>

<script>
const searchInput = document.getElementById('searchInput');
const typeFilter = document.getElementById('typeFilter');
const table = document.getElementById('fruitsTable').getElementsByTagName('tbody')[0];

function filterTable() {
  const filterText = searchInput.value.toLowerCase();
  const filterType = typeFilter.value;
  const rows = table.getElementsByTagName('tr');
  for (let i = 0; i < rows.length; i++) {
    const cells = rows[i].getElementsByTagName('td');
    const fruitName = cells[0].textContent.toLowerCase();
    const fruitType = cells[1].textContent;
    if (fruitName.includes(filterText) && (filterType === 'all' || fruitType === filterType)) {
      rows[i].style.display = '';
    } else {
      rows[i].style.display = 'none';
    }
  }
}

searchInput.addEventListener('keyup', filterTable);
typeFilter.addEventListener('change', filterTable);

function sortTable(n) {
  let switching = true;
  const tableElement = document.getElementById("fruitsTable");
  let dir = "asc";
  let switchcount = 0;
  while (switching) {
    switching = false;
    const rows = tableElement.rows;
    for (let i = 1; i < (rows.length - 1); i++) {
      let shouldSwitch = false;
      const x = rows[i].getElementsByTagName("TD")[n];
      const y = rows[i + 1].getElementsByTagName("TD")[n];
      let xContent = x.textContent || x.innerText;
      let yContent = y.textContent || y.innerText;
      if(n === 2){
        xContent = parseInt(xContent.replace(/[^0-9]/g,""));
        yContent = parseInt(yContent.replace(/[^0-9]/g,""));
      }
      if (dir === "asc") {
        if (xContent > yContent) { shouldSwitch = true; break; }
      } else {
        if (xContent < yContent) { shouldSwitch = true; break; }
      }
    }
    if (shouldSwitch) {
      rows[i].parentNode.insertBefore(rows[i + 1], rows[i]);
      switching = true;
      switchcount++;
    } else {
      if (switchcount === 0 && dir === "asc") {
        dir = "desc";
        switching = true;
      }
    }
  }
}
</script>

</body>
</html>

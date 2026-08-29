<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tournoi des 4 Équipes</title>
  <style>
    body { font-family: system-ui, sans-serif; margin: 0; padding: 20px; background-color: #f1f5f9; color: #1e293b; }
    .container { max-width: 800px; margin: 0 auto; background: white; padding: 20px; border-radius: 12px; box-shadow: 0 4px 6px rgba(0,0,0,0.1); }
    h1, h2 { text-align: center; color: #0f172a; }
    table { width: 100%; border-collapse: collapse; margin-top: 15px; }
    th, td { border: 1px solid #cbd5e1; padding: 12px; text-align: center; }
    th { background-color: #2563eb; color: white; }
    .card { background: #f8fafc; border: 1px solid #e2e8f0; padding: 15px; border-radius: 8px; margin-bottom: 20px; }
    .form-group { margin-bottom: 12px; display: flex; flex-direction: column; gap: 5px; }
    select, input, button { padding: 10px; border: 1px solid #cbd5e1; border-radius: 6px; font-size: 16px; }
    button { background-color: #2563eb; color: white; border: none; font-weight: bold; cursor: pointer; }
    .team-badge { display: inline-block; padding: 4px 10px; border-radius: 20px; font-weight: bold; color: white; }
    .vodka { background-color: #2563eb; }
    .ginto { background-color: #16a34a; }
    .teq { background-color: #ea580c; }
    .punch { background-color: #dc2626; }
  </style>
</head>
<body>
  <div class="container">
    <h1>🏆 Tournoi des 4 Équipes</h1>

    <div class="card">
      <h2>📝 Saisir un résultat</h2>
      <div class="form-group">
        <label>Épreuve :</label>
        <select id="epreuve">
          <option>🎯 Fléchettes</option>
          <option>🌽 Cornhole</option>
          <option>🪵 Palet Breton</option>
          <option>🏓 Ping-Pong</option>
        </select>
      </div>
      <div class="form-group">
        <label>Équipe :</label>
        <select id="equipe">
          <option value="Vodka Get">Vodka Get</option>
          <option value="Ginto">Ginto</option>
          <option value="Teq'Paf">Teq'Paf</option>
          <option value="Ti'Punch">Ti'Punch</option>
        </select>
      </div>
      <div class="form-group">
        <label>Points :</label>
        <input type="number" id="points" min="0" value="0">
      </div>
      <button onclick="ajouterPoints()">Valider les points</button>
    </div>

    <h2>📊 Classement Général</h2>
    <table>
      <thead>
        <tr>
          <th>Rang</th>
          <th>Équipe</th>
          <th>Points</th>
        </tr>
      </thead>
      <tbody id="tableau-classement"></tbody>
    </table>
  </div>

  <script>
    const scores = { "Vodka Get": 0, "Ginto": 0, "Teq'Paf": 0, "Ti'Punch": 0 };
    const classes = { "Vodka Get": "vodka", "Ginto": "ginto", "Teq'Paf": "teq", "Ti'Punch": "punch" };

    function updateTable() {
      const tbody = document.getElementById("tableau-classement");
      tbody.innerHTML = "";
      const sorted = Object.keys(scores).sort((a, b) => scores[b] - scores[a]);
      sorted.forEach((team, index) => {
        tbody.innerHTML += `<tr>
          <td><strong>${index + 1}</strong></td>
          <td><span class="team-badge ${classes[team]}">${team}</span></td>
          <td><strong>${scores[team]} pts</strong></td>
        </tr>`;
      });
    }

    function ajouterPoints() {
      const equipe = document.getElementById("equipe").value;
      const pts = parseInt(document.getElementById("points").value, 10) || 0;
      scores[equipe] += pts;
      updateTable();
    }

    updateTable();
  </script>
</body>
</html>

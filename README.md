<!DOCTYPE html>
<html lang="zh">
<head>
  <meta charset="UTF-8" />
  <title>电竞鹰眼</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <style>
    body { background: #0f0f0f; color: #fff; font-family: sans-serif; padding: 10px; }
    h1 { color: #4fc3f7; text-align: center; }
    .match { background: #1f1f1f; margin: 10px 0; padding: 10px; border-radius: 6px; }
  </style>
</head>
<body>
  <h1>电竞鹰眼 - 实时比赛展示</h1>
  <div id="matches">加载中...</div>
  <script>
    const API_KEY = "JP8nq0y_Or4M5q1qwTDXVDS3fKwaZoBmwKJFhuUxwEu0_yfsQXQ";
    fetch("https://api.pandascore.co/lol/matches/upcoming?per_page=3", {
      headers: { Authorization: `Bearer ${API_KEY}` }
    })
    .then(res => res.json())
    .then(data => {
      document.getElementById("matches").innerHTML = data.map(m => {
        const t1 = m.opponents[0]?.opponent?.name || "待定";
        const t2 = m.opponents[1]?.opponent?.name || "待定";
        const time = new Date(m.begin_at).toLocaleString();
        return `<div class="match">${t1} vs ${t2}<br>开始时间：${time}</div>`;
      }).join("");
    })
    .catch(() => {
      document.getElementById("matches").innerHTML = "加载失败，检查网络或API KEY。";
    });
  </script>
</body>
</html>

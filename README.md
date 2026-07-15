<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <title>ベストスノボマップ</title>
    
    <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
    
    <style>
        body, html {
            margin: 0;
            padding: 0;
            height: 100%;
            width: 100%;
            font-family: sans-serif;
        }
        #map {
            height: 100vh; /* 画面全体の高さを指定 */
            width: 100vw;  /* 画面全体の幅を指定 */
        }
        /* タイトルのスタイル */
        .header {
            position: absolute;
            top: 15px;
            left: 50%;
            transform: translateX(-50%);
            z-index: 1000; /* 地図の上に表示 */
            background: rgba(255, 255, 255, 0.9);
            padding: 10px 20px;
            border-radius: 8px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.3);
            font-weight: bold;
            color: #333;
            pointer-events: none; /* タイトル部分のタッチを下の地図に透過 */
        }
    </style>
</head>
<body>

    <div class="header">🏂 ベストスノボマップ</div>
    <div id="map"></div>

    <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>
    <script>
        // 1. 地図の初期化（日本の中心付近の座標とズームレベルを設定）
        const map = L.map('map').setView([36.5, 138.0], 5);

        // 2. OpenStreetMapのタイルレイヤーを読み込み
        L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
            maxZoom: 18,
            attribution: '© <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
        }).addTo(map);

        // 3. スノボスポットのデータ（緯度、経度、説明）
        const snowboardSpots = [
            { name: "ニセコマウンテンリゾート グラン・ヒラフ", lat: 42.863, lng: 140.700, desc: "極上のパウダースノーが楽しめる世界的な聖地。" },
            { name: "白馬八方尾根スキー場", lat: 36.702, lng: 137.836, desc: "日本最大級のスケールと絶景が魅力。" },
            { name: "GALA湯沢スノーリゾート", lat: 36.953, lng: 138.799, desc: "新幹線の駅直結でアクセス抜群。" }
        ];

        // 4. マーカー（ピン）を地図上に追加
        snowboardSpots.forEach(spot => {
            const marker = L.marker([spot.lat, spot.lng]).addTo(map);
            // ピンをタップしたときに吹き出しを表示
            marker.bindPopup(`<b>${spot.name}</b><br>${spot.desc}`);
        });
    </script>
</body>
</html>

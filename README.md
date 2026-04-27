<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>MOA合同会社 大阪府全域 営業アプリ</title>

<style>
*{
  box-sizing:border-box;
}

body{
  margin:0;
  font-family:-apple-system,BlinkMacSystemFont,"Hiragino Sans","Yu Gothic",sans-serif;
  background:#f4f6f8;
  color:#222;
}

header{
  background:linear-gradient(135deg,#0d47a1,#1976d2);
  color:#fff;
  padding:18px 14px;
  text-align:center;
}

header h1{
  margin:0;
  font-size:21px;
}

header p{
  margin:8px 0 0;
  font-size:13px;
  line-height:1.6;
}

.container{
  padding:12px;
  max-width:1100px;
  margin:auto;
}

.box{
  background:#fff;
  border-radius:14px;
  padding:14px;
  margin-bottom:12px;
  box-shadow:0 3px 10px rgba(0,0,0,0.08);
}

h2{
  font-size:17px;
  margin:0 0 10px;
  color:#0d47a1;
}

input,select,textarea{
  width:100%;
  padding:11px;
  margin:5px 0;
  border:1px solid #ccc;
  border-radius:9px;
  font-size:15px;
}

textarea{
  min-height:70px;
}

button,a.btn{
  display:inline-block;
  width:100%;
  padding:12px;
  margin:5px 0;
  border:none;
  border-radius:10px;
  font-size:15px;
  font-weight:bold;
  text-align:center;
  text-decoration:none;
  cursor:pointer;
}

.primary{background:#1976d2;color:#fff;}
.green{background:#2e7d32;color:#fff;}
.orange{background:#ef6c00;color:#fff;}
.gray{background:#607d8b;color:#fff;}
.red{background:#c62828;color:#fff;}
.purple{background:#6a1b9a;color:#fff;}

.grid{
  display:grid;
  grid-template-columns:1fr;
  gap:8px;
}

@media(min-width:700px){
  .grid{
    grid-template-columns:1fr 1fr 1fr;
  }
}

.card{
  background:#fff;
  border-radius:14px;
  padding:14px;
  margin-bottom:10px;
  box-shadow:0 3px 10px rgba(0,0,0,0.08);
  border-left:6px solid #1976d2;
}

.card h3{
  margin:0 0 6px;
  font-size:17px;
}

.tag{
  display:inline-block;
  padding:4px 8px;
  border-radius:999px;
  font-size:12px;
  margin:3px 3px 5px 0;
  color:#fff;
}

.tag-area{background:#1565c0;}
.tag-type{background:#6a1b9a;}
.tag-priority{background:#ef6c00;}

.small{
  font-size:13px;
  line-height:1.7;
  color:#555;
}

.memo{
  background:#fff8e1;
  border-radius:8px;
  padding:8px;
  font-size:13px;
  margin-top:8px;
}

.notice{
  background:#fffde7;
  border-left:5px solid #fbc02d;
  padding:10px;
  border-radius:10px;
  font-size:13px;
  line-height:1.7;
}

.count{
  font-weight:bold;
  color:#c62828;
}

.footer{
  text-align:center;
  color:#777;
  font-size:12px;
  padding:20px 10px;
}
</style>
</head>

<body>

<header>
  <h1>MOA合同会社 大阪府全域 営業アプリ</h1>
  <p>
    老人ホーム紹介・地域連携営業用<br>
    地域包括支援センター／居宅介護支援事業所／病院／施設を管理
  </p>
</header>

<div class="container">

  <div class="box">
    <h2>公式情報確認</h2>

    <a class="btn primary" href="https://www.kaigokensaku.mhlw.go.jp/27/index.php" target="_blank">
      厚生労働省 介護サービス情報公表システム 大阪府版
    </a>

    <a class="btn green" href="https://www.pref.osaka.lg.jp/o090100/jigyoshido/kaigo/data.html" target="_blank">
      大阪府 介護保険事業所台帳情報
    </a>

    <div class="notice">
      ※このアプリの情報は営業管理用です。  
      最新の指定状況、所在地、電話番号、サービス内容は、必ず厚生労働省・大阪府・各市町村の公式情報で確認してください。  
      ※MOA合同会社は法律相談・医療判断・介護認定の判断は行わず、必要に応じて専門機関へ確認する案内を行います。
    </div>
  </div>

  <div class="box">
    <h2>検索・絞り込み</h2>

    <div class="grid">
      <input type="text" id="keyword" placeholder="名称・住所・メモで検索 例：本町、北区、病院">

      <select id="areaFilter">
        <option value="">エリアすべて</option>
        <option value="大阪市北区">大阪市北区</option>
        <option value="大阪市中央区">大阪市中央区</option>
        <option value="大阪市天王寺区">大阪市天王寺区</option>
        <option value="大阪市阿倍野区">大阪市阿倍野区</option>
        <option value="大阪市淀川区">大阪市淀川区</option>
        <option value="大阪市都島区">大阪市都島区</option>
        <option value="大阪市福島区">大阪市福島区</option>
        <option value="大阪市此花区">大阪市此花区</option>
        <option value="大阪市西区">大阪市西区</option>
        <option value="大阪市港区">大阪市港区</option>
        <option value="大阪市大正区">大阪市大正区</option>
        <option value="大阪市浪速区">大阪市浪速区</option>
        <option value="大阪市西淀川区">大阪市西淀川区</option>
        <option value="大阪市東淀川区">大阪市東淀川区</option>
        <option value="大阪市東成区">大阪市東成区</option>
        <option value="大阪市生野区">大阪市生野区</option>
        <option value="大阪市旭区">大阪市旭区</option>
        <option value="大阪市城東区">大阪市城東区</option>
        <option value="大阪市鶴見区">大阪市鶴見区</option>
        <option value="大阪市住之江区">大阪市住之江区</option>
        <option value="大阪市住吉区">大阪市住吉区</option>
        <option value="大阪市東住吉区">大阪市東住吉区</option>
        <option value="大阪市平野区">大阪市平野区</option>
        <option value="大阪市西成区">大阪市西成区</option>
        <option value="豊中市">豊中市</option>
        <option value="池田市">池田市</option>
        <option value="箕面市">箕面市</option>
        <option value="吹田市">吹田市</option>
        <option value="茨木市">茨木市</option>
      </select>

      <select id="typeFilter">
        <option value="">種別すべて</option>
        <option value="地域包括支援センター">地域包括支援センター</option>
        <option value="居宅介護支援事業所">居宅介護支援事業所</option>
        <option value="病院">病院</option>
        <option value="老人ホーム">老人ホーム</option>
        <option value="士業">士業</option>
        <option value="保証会社">保証会社</option>
        <option value="その他">その他</option>
      </select>
    </div>

    <button class="primary" onclick="renderList()">検索する</button>
    <button class="gray" onclick="resetSearch()">検索リセット</button>

    <p class="small">
      表示件数：<span class="count" id="count">0</span>件
    </p>
  </div>

  <div class="box">
    <h2>CSV読み込み</h2>

    <p class="small">
      CSVの列はこの順番で作ってください。<br>
      <b>名称,種別,エリア,住所,電話番号,優先度,メモ</b>
    </p>

    <input type="file" id="csvFile" accept=".csv">
    <button class="orange" onclick="importCSV()">CSVを読み込む</button>

    <button class="purple" onclick="downloadSampleCSV()">CSVひな形をダウンロード</button>

    <div class="notice">
      CSVを読み込むと、現在のリストに追加されます。  
      文字化けする場合は、Excelで保存するときに「CSV UTF-8」を選んでください。
    </div>
  </div>

  <div class="box">
    <h2>手動で営業先を追加</h2>

    <input type="text" id="newName" placeholder="名称">
    <select id="newType">
      <option value="地域包括支援センター">地域包括支援センター</option>
      <option value="居宅介護支援事業所">居宅介護支援事業所</option>
      <option value="病院">病院</option>
      <option value="老人ホーム">老人ホーム</option>
      <option value="士業">士業</option>
      <option value="保証会社">保証会社</option>
      <option value="その他">その他</option>
    </select>
    <input type="text" id="newArea" placeholder="エリア 例：大阪市中央区">
    <input type="text" id="newAddress" placeholder="住所">
    <input type="tel" id="newTel" placeholder="電話番号">
    <select id="newPriority">
      <option value="高">優先度：高</option>
      <option value="中">優先度：中</option>
      <option value="低">優先度：低</option>
    </select>
    <textarea id="newMemo" placeholder="メモ 例：ケアマネ多数、病院連携あり、紹介可能性あり"></textarea>

    <button class="green" onclick="addOffice()">追加する</button>
  </div>

  <div class="box">
    <h2>営業リスト</h2>
    <div id="list"></div>
  </div>

</div>

<div class="footer">
  MOA合同会社｜老人ホーム紹介 ぬくもり｜大阪府全域 営業管理アプリ
</div>

<script>
let offices = [
  {
    name:"大阪市北区 地域包括支援センター 確認用",
    type:"地域包括支援センター",
    area:"大阪市北区",
    address:"大阪市北区",
    tel:"",
    priority:"高",
    memo:"公式サイトで最新情報を確認してから訪問。"
  },
  {
    name:"大阪市中央区 居宅介護支援事業所 確認用",
    type:"居宅介護支援事業所",
    area:"大阪市中央区",
    address:"大阪市中央区本町周辺",
    tel:"",
    priority:"高",
    memo:"本町・堺筋本町・谷町四丁目周辺の営業起点。"
  },
  {
    name:"大阪市天王寺区 地域包括・居宅 確認用",
    type:"地域包括支援センター",
    area:"大阪市天王寺区",
    address:"大阪市天王寺区",
    tel:"",
    priority:"中",
    memo:"徒歩営業ルート用。"
  },
  {
    name:"豊中市 居宅介護支援事業所 確認用",
    type:"居宅介護支援事業所",
    area:"豊中市",
    address:"豊中市",
    tel:"",
    priority:"中",
    memo:"北摂エリア連携候補。"
  },
  {
    name:"池田市 居宅介護支援事業所 確認用",
    type:"居宅介護支援事業所",
    area:"池田市",
    address:"池田市",
    tel:"",
    priority:"中",
    memo:"池田市内の紹介連携候補。"
  },
  {
    name:"箕面市 居宅介護支援事業所 確認用",
    type:"居宅介護支援事業所",
    area:"箕面市",
    address:"箕面市",
    tel:"",
    priority:"中",
    memo:"箕面市内の紹介連携候補。"
  }
];

function saveData(){
  localStorage.setItem("moaSalesOffices", JSON.stringify(offices));
}

function loadData(){
  const saved = localStorage.getItem("moaSalesOffices");
  if(saved){
    offices = JSON.parse(saved);
  }
}

function renderList(){
  const keyword = document.getElementById("keyword").value.trim();
  const area = document.getElementById("areaFilter").value;
  const type = document.getElementById("typeFilter").value;

  const list = document.getElementById("list");
  list.innerHTML = "";

  let filtered = offices.filter(o=>{
    const text = `${o.name} ${o.type} ${o.area} ${o.address} ${o.tel} ${o.memo}`;
    const matchKeyword = keyword === "" || text.includes(keyword);
    const matchArea = area === "" || o.area === area;
    const matchType = type === "" || o.type === type;
    return matchKeyword && matchArea && matchType;
  });

  document.getElementById("count").innerText = filtered.length;

  if(filtered.length === 0){
    list.innerHTML = `
      <div class="notice">
        該当する営業先がありません。  
        CSVを読み込むか、手動追加してください。
      </div>
    `;
    return;
  }

  filtered.forEach((o,index)=>{
    const realIndex = offices.indexOf(o);
    const telButton = o.tel 
      ? `<a class="btn green" href="tel:${o.tel}">電話する</a>`
      : `<button class="gray">電話番号なし</button>`;

    const mapUrl = "https://www.google.com/maps/search/?api=1&query=" + encodeURIComponent(o.address || o.name);

    const card = document.createElement("div");
    card.className = "card";
    card.innerHTML = `
      <h3>${escapeHTML(o.name)}</h3>

      <span class="tag tag-type">${escapeHTML(o.type)}</span>
      <span class="tag tag-area">${escapeHTML(o.area)}</span>
      <span class="tag tag-priority">優先度：${escapeHTML(o.priority)}</span>

      <p class="small">
        <b>住所：</b>${escapeHTML(o.address || "未登録")}<br>
        <b>電話：</b>${escapeHTML(o.tel || "未登録")}
      </p>

      <div class="memo">
        <b>営業メモ：</b><br>
        ${escapeHTML(o.memo || "未登録")}
      </div>

      ${telButton}

      <a class="btn primary" href="${mapUrl}" target="_blank">Googleマップで開く</a>

      <button class="orange" onclick="editMemo(${realIndex})">メモを編集</button>
      <button class="red" onclick="deleteOffice(${realIndex})">削除</button>
    `;
    list.appendChild(card);
  });
}

function resetSearch(){
  document.getElementById("keyword").value = "";
  document.getElementById("areaFilter").value = "";
  document.getElementById("typeFilter").value = "";
  renderList();
}

function addOffice(){
  const name = document.getElementById("newName").value.trim();
  const type = document.getElementById("newType").value;
  const area = document.getElementById("newArea").value.trim();
  const address = document.getElementById("newAddress").value.trim();
  const tel = document.getElementById("newTel").value.trim();
  const priority = document.getElementById("newPriority").value;
  const memo = document.getElementById("newMemo").value.trim();

  if(!name){
    alert("名称を入力してください。");
    return;
  }

  offices.push({
    name,
    type,
    area,
    address,
    tel,
    priority,
    memo
  });

  saveData();
  clearAddForm();
  renderList();
  alert("追加しました。");
}

function clearAddForm(){
  document.getElementById("newName").value = "";
  document.getElementById("newArea").value = "";
  document.getElementById("newAddress").value = "";
  document.getElementById("newTel").value = "";
  document.getElementById("newMemo").value = "";
}

function deleteOffice(index){
  if(confirm("この営業先を削除しますか？")){
    offices.splice(index,1);
    saveData();
    renderList();
  }
}

function editMemo(index){
  const current = offices[index].memo || "";
  const newMemo = prompt("営業メモを入力してください", current);
  if(newMemo !== null){
    offices[index].memo = newMemo;
    saveData();
    renderList();
  }
}

function importCSV(){
  const fileInput = document.getElementById("csvFile");
  const file = fileInput.files[0];

  if(!file){
    alert("CSVファイルを選んでください。");
    return;
  }

  const reader = new FileReader();

  reader.onload = function(e){
    const text = e.target.result;
    const rows = parseCSV(text);

    let added = 0;

    rows.forEach((row,i)=>{
      if(i === 0 && row[0] && row[0].includes("名称")){
        return;
      }

      if(row.length < 1 || !row[0]) return;

      offices.push({
        name: row[0] || "",
        type: row[1] || "その他",
        area: row[2] || "",
        address: row[3] || "",
        tel: row[4] || "",
        priority: row[5] || "中",
        memo: row[6] || ""
      });

      added++;
    });

    saveData();
    renderList();
    alert(added + "件読み込みました。");
  };

  reader.readAsText(file, "UTF-8");
}

function parseCSV(text){
  const rows = [];
  let row = [];
  let cell = "";
  let inQuotes = false;

  for(let i=0; i<text.length; i++){
    const char = text[i];
    const next = text[i+1];

    if(char === '"' && inQuotes && next === '"'){
      cell += '"';
      i++;
    }else if(char === '"'){
      inQuotes = !inQuotes;
    }else if(char === "," && !inQuotes){
      row.push(cell.trim());
      cell = "";
    }else if((char === "\n" || char === "\r") && !inQuotes){
      if(cell || row.length){
        row.push(cell.trim());
        rows.push(row);
        row = [];
        cell = "";
      }
      if(char === "\r" && next === "\n") i++;
    }else{
      cell += char;
    }
  }

  if(cell || row.length){
    row.push(cell.trim());
    rows.push(row);
  }

  return rows;
}

function downloadSampleCSV(){
  const csv = 
`名称,種別,エリア,住所,電話番号,優先度,メモ
サンプル地域包括支援センター,地域包括支援センター,大阪市北区,大阪市北区,06-0000-0000,高,まず公式情報を確認
サンプル居宅介護支援事業所,居宅介護支援事業所,大阪市中央区,大阪市中央区本町,06-0000-0000,高,ケアマネ連携候補
サンプル病院,病院,大阪市天王寺区,大阪市天王寺区,06-0000-0000,中,退院支援室に確認`;

  const blob = new Blob(["\uFEFF" + csv], {type:"text/csv;charset=utf-8;"});
  const url = URL.createObjectURL(blob);
  const a = document.createElement("a");
  a.href = url;
  a.download = "moa_sales_sample.csv";
  document.body.appendChild(a);
  a.click();
  document.body.removeChild(a);
  URL.revokeObjectURL(url);
}

function escapeHTML(str){
  return String(str)
    .replaceAll("&","&amp;")
    .replaceAll("<","&lt;")
    .replaceAll(">","&gt;")
    .replaceAll('"',"&quot;")
    .replaceAll("'","&#039;");
}

document.getElementById("keyword").addEventListener("input", renderList);
document.getElementById("areaFilter").addEventListener("change", renderList);
document.getElementById("typeFilter").addEventListener("change", renderList);

loadData();
renderList();
</script>

</body>
</html>

<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>MOA大阪府全域営業アプリ</title>

<style>
*{box-sizing:border-box;}

body{
  margin:0;
  font-family:-apple-system,BlinkMacSystemFont,"Hiragino Sans","Yu Gothic",Meiryo,sans-serif;
  background:#f5f1ea;
  color:#2f2a25;
}

header{
  background:linear-gradient(135deg,#3f2d22,#9b7a4d);
  color:#fff;
  padding:18px 12px;
  text-align:center;
}

header h1{
  margin:0;
  font-size:21px;
  line-height:1.45;
}

header p{
  margin:8px 0 0;
  font-size:13px;
}

.wrap{
  max-width:1100px;
  margin:0 auto;
  padding:12px;
}

.notice{
  background:#fff8e8;
  border:1px solid #ead4a0;
  color:#5b4636;
  border-radius:14px;
  padding:12px;
  font-size:13px;
  line-height:1.7;
  margin-bottom:12px;
}

.box{
  background:#fff;
  border-radius:16px;
  padding:12px;
  box-shadow:0 4px 14px rgba(0,0,0,.08);
  margin-bottom:12px;
}

.row{
  display:flex;
  gap:8px;
  flex-wrap:wrap;
  margin-bottom:8px;
}

.col{
  flex:1 1 160px;
}

input,select,textarea{
  width:100%;
  padding:11px;
  border:1px solid #d8d0c6;
  border-radius:12px;
  font-size:15px;
  background:#fff;
}

textarea{
  min-height:110px;
  font-family:monospace;
}

button{
  border:none;
  border-radius:12px;
  padding:11px 12px;
  font-size:14px;
  font-weight:bold;
  cursor:pointer;
}

.btn-main{background:#5b4636;color:#fff;}
.btn-sub{background:#e7ddd0;color:#3c332b;}
.btn-green{background:#2f8f5b;color:#fff;}
.btn-blue{background:#2f6fbd;color:#fff;}
.btn-orange{background:#d9822b;color:#fff;}
.btn-red{background:#b94b4b;color:#fff;}
.btn-purple{background:#7157a8;color:#fff;}

.officials a{
  display:inline-block;
  text-decoration:none;
  color:#fff;
  background:#2f6fbd;
  padding:9px 10px;
  border-radius:10px;
  font-size:13px;
  margin:3px;
  font-weight:bold;
}

.summary{
  font-weight:bold;
  margin:8px 2px 10px;
  color:#5b4636;
}

.card{
  background:#fff;
  border-radius:16px;
  padding:14px;
  margin-bottom:12px;
  box-shadow:0 4px 14px rgba(0,0,0,.08);
  border-left:7px solid #9a7a54;
}

.card.kyotaku{border-left-color:#2f8f5b;}
.card.houkatsu{border-left-color:#2f6fbd;}
.card.facility{border-left-color:#8a5dbb;}
.card.hospital{border-left-color:#b94b4b;}
.card.other{border-left-color:#9a7a54;}

.tagline{
  display:flex;
  flex-wrap:wrap;
  gap:6px;
  margin-bottom:8px;
}

.tag{
  display:inline-block;
  padding:4px 8px;
  border-radius:999px;
  background:#f0ebe4;
  font-size:12px;
  color:#5b4636;
}

.tag.hot{background:#ffe6d1;color:#8b3f00;}
.tag.done{background:#dff3e8;color:#17633c;}
.tag.ng{background:#f5dada;color:#8b1f1f;}

.name{
  font-size:18px;
  font-weight:bold;
  margin:4px 0 8px;
  color:#2d2520;
}

.info{
  font-size:14px;
  line-height:1.7;
  margin:4px 0;
}

.memo{
  background:#f8f5ef;
  border-radius:10px;
  padding:9px;
  font-size:13px;
  line-height:1.7;
  margin-top:8px;
}

.actions{
  display:flex;
  gap:8px;
  flex-wrap:wrap;
  margin-top:12px;
}

.actions a,
.actions button{
  flex:1 1 110px;
  text-align:center;
  text-decoration:none;
  border-radius:12px;
  padding:11px 8px;
  color:#fff;
  font-weight:bold;
  font-size:14px;
}

.tel{background:#2f8f5b;}
.map{background:#2f6fbd;}
.route{background:#d9822b;}
.copy{background:#5b4636;}
.doneBtn{background:#2f8f5b;}
.hotBtn{background:#d9822b;}
.ngBtn{background:#b94b4b;}

.empty{
  background:#fff;
  border-radius:16px;
  padding:18px;
  text-align:center;
  color:#7a6b5f;
}

.small{
  font-size:12px;
  color:#7a6b5f;
  line-height:1.6;
}

.footer{
  text-align:center;
  font-size:12px;
  color:#7a6b5f;
  padding:20px 8px 30px;
  line-height:1.6;
}

@media(max-width:600px){
  header h1{font-size:18px;}
  .actions a,.actions button{flex:1 1 46%;font-size:13px;}
}
</style>
</head>

<body>

<header>
  <h1>MOA 大阪府全域営業アプリ</h1>
  <p>老人ホーム紹介 ぬくもり｜居宅・地域包括・施設・病院・営業先管理</p>
</header>

<div class="wrap">

  <div class="notice">
    このアプリは大阪府全域の営業先を管理するためのアプリです。<br>
    公式CSVやExcelからコピーしたデータを貼り付けて、区・市町村、種別、営業状況で検索できます。<br>
    電話番号・所在地・指定状況は変更される場合があるため、訪問前に必ず公式情報または電話で確認してください。
  </div>

  <div class="box officials">
    <strong>公式データ確認リンク</strong><br>
    <a href="https://www.pref.osaka.lg.jp/o090100/jigyoshido/kaigo/data.html" target="_blank">大阪府 介護保険事業所台帳CSV</a>
    <a href="https://www.kaigokensaku.mhlw.go.jp/27/index.php" target="_blank">大阪府 介護事業所検索</a>
    <a href="https://www.city.osaka.lg.jp/fukushi/page/0000370522.html" target="_blank">大阪市 地域包括一覧</a>
    <a href="https://www.kaigokensaku.mhlw.go.jp/27/index.php?action_kouhyou_pref_search_condition_index=true" target="_blank">条件から事業所検索</a>
  </div>

  <div class="box">
    <div class="row">
      <div class="col">
        <input id="keyword" type="text" placeholder="例：北区、豊中、池田、箕面、居宅、ケアプラン、病院、施設名">
      </div>
    </div>

    <div class="row">
      <div class="col">
        <select id="areaSelect"></select>
      </div>

      <div class="col">
        <select id="typeSelect">
          <option value="">種別：すべて</option>
          <option value="居宅介護支援事業所">居宅介護支援事業所</option>
          <option value="地域包括支援センター">地域包括支援センター</option>
          <option value="総合相談窓口・ブランチ">総合相談窓口・ブランチ</option>
          <option value="有料老人ホーム">有料老人ホーム</option>
          <option value="サービス付き高齢者向け住宅">サービス付き高齢者向け住宅</option>
          <option value="特別養護老人ホーム">特別養護老人ホーム</option>
          <option value="介護老人保健施設">介護老人保健施設</option>
          <option value="病院">病院</option>
          <option value="士業・保証会社">士業・保証会社</option>
          <option value="その他">その他</option>
        </select>
      </div>

      <div class="col">
        <select id="statusSelect">
          <option value="">営業状況：すべて</option>
          <option value="未訪問">未訪問</option>
          <option value="優先">優先</option>
          <option value="訪問済み">訪問済み</option>
          <option value="見込みあり">見込みあり</option>
          <option value="再訪問">再訪問</option>
          <option value="対象外">対象外</option>
        </select>
      </div>
    </div>

    <div class="row">
      <button class="btn-main" onclick="renderList()">検索する</button>
      <button class="btn-sub" onclick="resetSearch()">リセット</button>
      <button class="btn-orange" onclick="openRouteForVisible()">表示中ルート</button>
      <button class="btn-purple" onclick="downloadCsv()">CSV出力</button>
    </div>
  </div>

  <div class="box">
    <strong>営業先をCSVで追加</strong>
    <p class="small">
      使いやすい形式：<br>
      市区町村,種別,名前,住所,電話,FAX,メモ<br><br>
      例：豊中市,居宅介護支援事業所,〇〇ケアプランセンター,大阪府豊中市〇〇1-1-1,06-0000-0000,06-0000-0001,居宅営業先<br><br>
      大阪府公式CSVやExcelから貼る場合も、できるだけ「事業所名・住所・電話番号・サービス種類」が入るように貼ってください。
    </p>

    <textarea id="csvInput" placeholder="ここにCSV、またはExcelからコピーした表を貼り付け"></textarea>

    <div class="row">
      <button class="btn-green" onclick="importCsv()">CSVを追加する</button>
      <button class="btn-red" onclick="clearAllData()">保存データを全部消す</button>
    </div>
  </div>

  <div class="box">
    <strong>1件ずつ手入力で追加</strong>
    <div class="row">
      <div class="col"><select id="manualArea"></select></div>
      <div class="col">
        <select id="manualType">
          <option value="居宅介護支援事業所">居宅介護支援事業所</option>
          <option value="地域包括支援センター">地域包括支援センター</option>
          <option value="総合相談窓口・ブランチ">総合相談窓口・ブランチ</option>
          <option value="有料老人ホーム">有料老人ホーム</option>
          <option value="サービス付き高齢者向け住宅">サービス付き高齢者向け住宅</option>
          <option value="特別養護老人ホーム">特別養護老人ホーム</option>
          <option value="介護老人保健施設">介護老人保健施設</option>
          <option value="病院">病院</option>
          <option value="士業・保証会社">士業・保証会社</option>
          <option value="その他">その他</option>
        </select>
      </div>
    </div>

    <div class="row">
      <div class="col"><input id="manualName" placeholder="営業先名"></div>
      <div class="col"><input id="manualAddress" placeholder="住所"></div>
    </div>

    <div class="row">
      <div class="col"><input id="manualTel" placeholder="電話番号"></div>
      <div class="col"><input id="manualFax" placeholder="FAX"></div>
    </div>

    <div class="row">
      <div class="col"><input id="manualMemo" placeholder="営業メモ"></div>
    </div>

    <button class="btn-green" onclick="addManual()">手入力データを追加</button>
  </div>

  <div id="summary" class="summary"></div>
  <div id="list"></div>

  <div class="footer">
    MOA合同会社｜老人ホーム紹介 ぬくもり<br>
    大阪府全域対応版
  </div>

</div>

<script>
/* =====================================================
   大阪府全域 営業アプリ
   CSV読み込み・手入力・検索・電話・地図・ルート・営業状況保存
===================================================== */

const OSAKA_AREAS = [
  "大阪市北区","大阪市都島区","大阪市福島区","大阪市此花区","大阪市中央区",
  "大阪市西区","大阪市港区","大阪市大正区","大阪市天王寺区","大阪市浪速区",
  "大阪市西淀川区","大阪市淀川区","大阪市東淀川区","大阪市東成区","大阪市生野区",
  "大阪市旭区","大阪市城東区","大阪市鶴見区","大阪市阿倍野区","大阪市住之江区",
  "大阪市住吉区","大阪市東住吉区","大阪市平野区","大阪市西成区",
  "堺市堺区","堺市中区","堺市東区","堺市西区","堺市南区","堺市北区","堺市美原区",
  "岸和田市","豊中市","池田市","吹田市","泉大津市","高槻市","貝塚市","守口市",
  "枚方市","茨木市","八尾市","泉佐野市","富田林市","寝屋川市","河内長野市",
  "松原市","大東市","和泉市","箕面市","柏原市","羽曳野市","門真市","摂津市",
  "高石市","藤井寺市","東大阪市","泉南市","四條畷市","交野市","大阪狭山市",
  "阪南市","島本町","豊能町","能勢町","忠岡町","熊取町","田尻町","岬町",
  "太子町","河南町","千早赤阪村"
];

const INITIAL_DATA = [
  {
    area:"大阪市中央区",
    type:"地域包括支援センター",
    name:"中央区地域包括支援センター",
    address:"大阪市中央区上本町西2-5-25",
    tel:"06-6763-8139",
    fax:"06-6763-8151",
    memo:"中央区の地域包括支援センター。訪問前に公式情報確認。",
    status:"未訪問"
  },
  {
    area:"大阪市中央区",
    type:"地域包括支援センター",
    name:"中央区北部地域包括支援センター",
    address:"大阪市中央区農人橋3-1-3 ドミール堺筋本町1階",
    tel:"06-6944-2116",
    fax:"06-6944-2117",
    memo:"本町・堺筋本町方面の営業起点。",
    status:"未訪問"
  },
  {
    area:"大阪市北区",
    type:"地域包括支援センター",
    name:"北区地域包括支援センター",
    address:"大阪市北区神山町15-11",
    tel:"06-6313-5568",
    fax:"06-6314-6377",
    memo:"北区中心部の高齢者相談窓口。",
    status:"未訪問"
  },
  {
    area:"大阪市北区",
    type:"地域包括支援センター",
    name:"北区大淀地域包括支援センター",
    address:"大阪市北区長柄中1-1-21",
    tel:"06-6354-1165",
    fax:"06-6354-1175",
    memo:"長柄・豊崎・中津・大淀方面。",
    status:"未訪問"
  }
];

let salesData = JSON.parse(localStorage.getItem("moa_osaka_sales_data") || "null");

if(!salesData){
  salesData = INITIAL_DATA;
  saveData();
}

function saveData(){
  localStorage.setItem("moa_osaka_sales_data", JSON.stringify(salesData));
}

function setupAreaSelects(){
  const areaSelect = document.getElementById("areaSelect");
  const manualArea = document.getElementById("manualArea");

  areaSelect.innerHTML = `<option value="">市区町村：すべて</option>`;
  manualArea.innerHTML = ``;

  OSAKA_AREAS.forEach(area => {
    areaSelect.innerHTML += `<option value="${escapeHtml(area)}">${escapeHtml(area)}</option>`;
    manualArea.innerHTML += `<option value="${escapeHtml(area)}">${escapeHtml(area)}</option>`;
  });
}

function normalizeArea(address, fallback){
  const text = String(address || fallback || "");

  for(const area of OSAKA_AREAS){
    if(text.includes(area)) return area;
  }

  // 大阪市内で「北区」などだけ入っている場合の補正
  const osakaWards = OSAKA_AREAS.filter(x => x.startsWith("大阪市"));
  for(const area of osakaWards){
    const wardOnly = area.replace("大阪市","");
    if(text.includes(wardOnly)) return area;
  }

  return fallback || "未分類";
}

function normalizeType(typeText){
  const t = String(typeText || "");

  if(t.includes("居宅介護支援")) return "居宅介護支援事業所";
  if(t.includes("地域包括")) return "地域包括支援センター";
  if(t.includes("ブランチ") || t.includes("総合相談")) return "総合相談窓口・ブランチ";
  if(t.includes("有料老人")) return "有料老人ホーム";
  if(t.includes("サービス付き高齢者") || t.includes("サ高住")) return "サービス付き高齢者向け住宅";
  if(t.includes("特別養護") || t.includes("特養")) return "特別養護老人ホーム";
  if(t.includes("老人保健") || t.includes("老健")) return "介護老人保健施設";
  if(t.includes("病院")) return "病院";
  if(t.includes("司法書士") || t.includes("弁護士") || t.includes("行政書士") || t.includes("保証")) return "士業・保証会社";

  return t || "その他";
}

function mapUrl(address){
  return "https://www.google.com/maps/search/?api=1&query=" + encodeURIComponent(address);
}

function routeUrl(address){
  return "https://www.google.com/maps/dir/?api=1&destination=" + encodeURIComponent(address);
}

function telUrl(tel){
  if(!tel) return "#";
  return "tel:" + String(tel).replaceAll("-", "").replaceAll(" ", "");
}

function getFilteredData(){
  const keyword = document.getElementById("keyword").value.trim().toLowerCase();
  const area = document.getElementById("areaSelect").value;
  const type = document.getElementById("typeSelect").value;
  const status = document.getElementById("statusSelect").value;

  return salesData.filter(item => {
    const text = [
      item.area,item.type,item.name,item.address,item.tel,item.fax,item.memo,item.status
    ].join(" ").toLowerCase();

    return (!keyword || text.includes(keyword)) &&
           (!area || item.area === area) &&
           (!type || item.type === type) &&
           (!status || item.status === status);
  });
}

function renderList(){
  const data = getFilteredData();

  document.getElementById("summary").textContent =
    "表示件数：" + data.length + "件 ／ 登録総数：" + salesData.length + "件";

  const list = document.getElementById("list");

  if(data.length === 0){
    list.innerHTML = `<div class="empty">該当する営業先がありません。<br>検索条件を変えるか、CSVでデータを追加してください。</div>`;
    return;
  }

  list.innerHTML = data.map((item,index) => {
    const realIndex = salesData.indexOf(item);
    let cardClass = "card other";

    if(item.type === "居宅介護支援事業所") cardClass = "card kyotaku";
    if(item.type === "地域包括支援センター" || item.type === "総合相談窓口・ブランチ") cardClass = "card houkatsu";
    if(item.type.includes("老人ホーム") || item.type.includes("施設")) cardClass = "card facility";
    if(item.type === "病院") cardClass = "card hospital";

    let statusClass = "";
    if(item.status === "優先" || item.status === "見込みあり") statusClass = "hot";
    if(item.status === "訪問済み") statusClass = "done";
    if(item.status === "対象外") statusClass = "ng";

    return `
      <div class="${cardClass}">
        <div class="tagline">
          <span class="tag">${index + 1}</span>
          <span class="tag">${escapeHtml(item.area || "未分類")}</span>
          <span class="tag">${escapeHtml(item.type || "その他")}</span>
          <span class="tag ${statusClass}">${escapeHtml(item.status || "未訪問")}</span>
        </div>

        <div class="name">${escapeHtml(item.name)}</div>

        <div class="info">📍 <strong>住所：</strong>${escapeHtml(item.address || "")}</div>
        <div class="info">☎️ <strong>電話：</strong>${item.tel ? escapeHtml(item.tel) : "未入力"}</div>
        <div class="info">📠 <strong>FAX：</strong>${item.fax ? escapeHtml(item.fax) : "未入力"}</div>

        <div class="memo">
          <strong>営業メモ：</strong><br>
          ${escapeHtml(item.memo || "")}
        </div>

        <div class="actions">
          <a class="tel" href="${telUrl(item.tel)}">電話</a>
          <a class="map" href="${mapUrl(item.address)}" target="_blank">地図</a>
          <a class="route" href="${routeUrl(item.address)}" target="_blank">ルート</a>
          <button class="copy" onclick="copyInfo(${realIndex})">コピー</button>
          <button class="hotBtn" onclick="setStatus(${realIndex},'優先')">優先</button>
          <button class="doneBtn" onclick="setStatus(${realIndex},'訪問済み')">訪問済</button>
          <button class="ngBtn" onclick="setStatus(${realIndex},'対象外')">対象外</button>
        </div>
      </div>
    `;
  }).join("");
}

function resetSearch(){
  document.getElementById("keyword").value = "";
  document.getElementById("areaSelect").value = "";
  document.getElementById("typeSelect").value = "";
  document.getElementById("statusSelect").value = "";
  renderList();
}

function setStatus(index,status){
  salesData[index].status = status;
  saveData();
  renderList();
}

function copyInfo(index){
  const item = salesData[index];

  const text =
`【${item.area}】${item.type}
${item.name}

住所：${item.address}
電話：${item.tel || "未入力"}
FAX：${item.fax || "未入力"}
営業状況：${item.status || "未訪問"}
メモ：${item.memo || ""}
地図：${mapUrl(item.address)}`;

  navigator.clipboard.writeText(text).then(() => {
    alert("コピーしました。");
  }).catch(() => {
    alert("コピーできませんでした。");
  });
}

function openRouteForVisible(){
  const data = getFilteredData();

  if(data.length === 0){
    alert("表示中の営業先がありません。");
    return;
  }

  if(data.length > 10){
    alert("Googleマップの仕様上、ルートは10件以内に絞るのがおすすめです。市区町村や種別で絞ってください。");
  }

  const limited = data.slice(0,10);
  const destination = limited[limited.length - 1].address;
  const waypoints = limited.slice(0,-1).map(x => x.address).join("|");

  let url = "https://www.google.com/maps/dir/?api=1";
  url += "&destination=" + encodeURIComponent(destination);
  if(waypoints) url += "&waypoints=" + encodeURIComponent(waypoints);

  window.open(url,"_blank");
}

/* =========================
   CSV読み込み
========================= */

function parseCsvLine(line){
  const result = [];
  let current = "";
  let inQuotes = false;

  for(let i=0; i<line.length; i++){
    const char = line[i];
    const next = line[i+1];

    if(char === '"' && inQuotes && next === '"'){
      current += '"';
      i++;
    }else if(char === '"'){
      inQuotes = !inQuotes;
    }else if((char === "," || char === "\t") && !inQuotes){
      result.push(current.trim());
      current = "";
    }else{
      current += char;
    }
  }

  result.push(current.trim());
  return result;
}

function findCol(headers, candidates){
  for(const c of candidates){
    const idx = headers.findIndex(h => h.includes(c));
    if(idx !== -1) return idx;
  }
  return -1;
}

function importCsv(){
  const raw = document.getElementById("csvInput").value.trim();

  if(!raw){
    alert("CSVまたはExcelコピーを貼り付けてください。");
    return;
  }

  const lines = raw.split(/\r?\n/).filter(x => x.trim());
  if(lines.length === 0){
    alert("読み込める行がありません。");
    return;
  }

  const firstCols = parseCsvLine(lines[0]);
  const hasHeader = firstCols.some(x =>
    x.includes("事業所") ||
    x.includes("名称") ||
    x.includes("住所") ||
    x.includes("所在地") ||
    x.includes("電話") ||
    x.includes("サービス")
  );

  let startIndex = 0;
  let header = [];

  if(hasHeader){
    header = firstCols;
    startIndex = 1;
  }

  const newItems = [];

  if(hasHeader){
    const nameIdx = findCol(header,["事業所名","事業所の名称","名称","施設名"]);
    const addressIdx = findCol(header,["所在地","住所","事業所所在地"]);
    const telIdx = findCol(header,["電話番号","電話"]);
    const faxIdx = findCol(header,["FAX番号","ＦＡＸ","FAX"]);
    const typeIdx = findCol(header,["サービス種類","サービス名","種別"]);
    const areaIdx = findCol(header,["市区町村","市町村","区"]);

    for(let i=startIndex; i<lines.length; i++){
      const cols = parseCsvLine(lines[i]);

      const name = cols[nameIdx] || "";
      const address = cols[addressIdx] || "";
      const tel = cols[telIdx] || "";
      const fax = cols[faxIdx] || "";
      const typeRaw = cols[typeIdx] || "";
      const areaRaw = cols[areaIdx] || "";

      if(!name || !address) continue;

      const item = {
        area: normalizeArea(address, areaRaw),
        type: normalizeType(typeRaw),
        name:name,
        address:address,
        tel:tel,
        fax:fax,
        memo:"CSV取込データ",
        status:"未訪問"
      };

      newItems.push(item);
    }
  }else{
    for(let i=0; i<lines.length; i++){
      const cols = parseCsvLine(lines[i]);

      const area = cols[0] || "";
      const type = cols[1] || "その他";
      const name = cols[2] || "";
      const address = cols[3] || "";
      const tel = cols[4] || "";
      const fax = cols[5] || "";
      const memo = cols[6] || "手動CSV追加";

      if(!name || !address) continue;

      const item = {
        area: normalizeArea(address, area),
        type: normalizeType(type),
        name:name,
        address:address,
        tel:tel,
        fax:fax,
        memo:memo,
        status:"未訪問"
      };

      newItems.push(item);
    }
  }

  if(newItems.length === 0){
    alert("追加できるデータがありません。列の並びを確認してください。");
    return;
  }

  let addedCount = 0;

  newItems.forEach(item => {
    const exists = salesData.some(x => x.name === item.name && x.address === item.address);
    if(!exists){
      salesData.push(item);
      addedCount++;
    }
  });

  saveData();
  document.getElementById("csvInput").value = "";

  alert(addedCount + "件追加しました。重複は除外しました。");
  renderList();
}

function addManual(){
  const item = {
    area: document.getElementById("manualArea").value,
    type: document.getElementById("manualType").value,
    name: document.getElementById("manualName").value.trim(),
    address: document.getElementById("manualAddress").value.trim(),
    tel: document.getElementById("manualTel").value.trim(),
    fax: document.getElementById("manualFax").value.trim(),
    memo: document.getElementById("manualMemo").value.trim(),
    status:"未訪問"
  };

  if(!item.name || !item.address){
    alert("営業先名と住所は必須です。");
    return;
  }

  item.area = normalizeArea(item.address, item.area);

  salesData.push(item);
  saveData();

  document.getElementById("manualName").value = "";
  document.getElementById("manualAddress").value = "";
  document.getElementById("manualTel").value = "";
  document.getElementById("manualFax").value = "";
  document.getElementById("manualMemo").value = "";

  alert("追加しました。");
  renderList();
}

function clearAllData(){
  if(!confirm("保存した営業データを全部消して、初期データだけに戻します。よろしいですか？")) return;

  salesData = INITIAL_DATA;
  saveData();
  renderList();
}

function downloadCsv(){
  const rows = [
    ["市区町村","種別","名前","住所","電話","FAX","営業状況","メモ"]
  ];

  salesData.forEach(item => {
    rows.push([
      item.area || "",
      item.type || "",
      item.name || "",
      item.address || "",
      item.tel || "",
      item.fax || "",
      item.status || "",
      item.memo || ""
    ]);
  });

  const csv = rows.map(row => row.map(v => {
    const s = String(v).replaceAll('"','""');
    return `"${s}"`;
  }).join(",")).join("\n");

  const blob = new Blob(["\uFEFF" + csv], {type:"text/csv;charset=utf-8;"});
  const url = URL.createObjectURL(blob);

  const a = document.createElement("a");
  a.href = url;
  a.download = "moa_osaka_sales_list.csv";
  a.click();

  URL.revokeObjectURL(url);
}

function escapeHtml(str){
  if(!str) return "";
  return String(str)
    .replaceAll("&","&amp;")
    .replaceAll("<","&lt;")
    .replaceAll(">","&gt;")
    .replaceAll('"',"&quot;")
    .replaceAll("'","&#039;");
}

setupAreaSelects();
renderList();
</script>

</body>
</html>

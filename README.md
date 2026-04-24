<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>MOA営業アプリ｜中央区・北区 地域包括支援センター</title>

<style>
  *{
    box-sizing:border-box;
  }

  body{
    margin:0;
    font-family:-apple-system,BlinkMacSystemFont,"Hiragino Sans","Yu Gothic",Meiryo,sans-serif;
    background:#f4f1ec;
    color:#2f2a25;
  }

  header{
    background:linear-gradient(135deg,#5b4636,#9a7a54);
    color:#fff;
    padding:18px 14px;
    text-align:center;
  }

  header h1{
    margin:0;
    font-size:21px;
    line-height:1.4;
  }

  header p{
    margin:8px 0 0;
    font-size:13px;
    opacity:.95;
  }

  .wrap{
    max-width:980px;
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

  .controls{
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

  input,select{
    width:100%;
    padding:12px;
    border:1px solid #d8d0c6;
    border-radius:12px;
    font-size:15px;
    background:#fff;
  }

  .col{
    flex:1 1 160px;
  }

  button{
    border:none;
    border-radius:12px;
    padding:11px 12px;
    font-size:14px;
    font-weight:bold;
    cursor:pointer;
  }

  .btn-main{
    background:#5b4636;
    color:#fff;
  }

  .btn-sub{
    background:#e7ddd0;
    color:#3c332b;
  }

  .btn-green{
    background:#2f8f5b;
    color:#fff;
  }

  .btn-blue{
    background:#2f6fbd;
    color:#fff;
  }

  .btn-orange{
    background:#d9822b;
    color:#fff;
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

  .card.houkatsu{
    border-left-color:#2f6fbd;
  }

  .card.branch{
    border-left-color:#d9822b;
  }

  .card.kyotaku{
    border-left-color:#2f8f5b;
  }

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

  .tel{
    background:#2f8f5b;
  }

  .map{
    background:#2f6fbd;
  }

  .route{
    background:#d9822b;
  }

  .copy{
    background:#5b4636;
  }

  .footer{
    text-align:center;
    font-size:12px;
    color:#7a6b5f;
    padding:20px 8px 30px;
    line-height:1.6;
  }

  .empty{
    background:#fff;
    border-radius:16px;
    padding:18px;
    text-align:center;
    color:#7a6b5f;
  }

  @media(max-width:600px){
    header h1{
      font-size:18px;
    }

    .actions a,
    .actions button{
      flex:1 1 46%;
      font-size:13px;
    }
  }
</style>
</head>

<body>

<header>
  <h1>MOA営業アプリ<br>中央区・北区 地域包括支援センター</h1>
  <p>老人ホーム紹介 ぬくもり｜営業訪問・電話・地図確認用</p>
</header>

<div class="wrap">

  <div class="notice">
    ※このアプリは営業訪問の補助用です。電話番号・所在地・担当圏域は変更される場合があります。訪問前に必ず公式情報または電話で確認してください。<br>
    ※ケアマネ様・地域包括様への説明では「無料の老人ホーム紹介」「施設選びの情報提供」「見学同行・入居手続きサポート」として案内し、法律相談・契約判断の代行は行わない表現にしてください。
  </div>

  <div class="controls">
    <div class="row">
      <div class="col">
        <input id="keyword" type="text" placeholder="例：北区、中央区、本町、梅田、地域包括、ブランチ">
      </div>
    </div>

    <div class="row">
      <div class="col">
        <select id="ward">
          <option value="">区を選択：すべて</option>
          <option value="中央区">中央区</option>
          <option value="北区">北区</option>
        </select>
      </div>

      <div class="col">
        <select id="category">
          <option value="">種別：すべて</option>
          <option value="地域包括支援センター">地域包括支援センター</option>
          <option value="総合相談窓口・ブランチ">総合相談窓口・ブランチ</option>
          <option value="居宅介護支援事業所">居宅介護支援事業所</option>
        </select>
      </div>
    </div>

    <div class="row">
      <button class="btn-main" onclick="renderList()">検索する</button>
      <button class="btn-sub" onclick="resetSearch()">リセット</button>
      <button class="btn-orange" onclick="openAllRoute()">表示中ルートを開く</button>
    </div>
  </div>

  <div id="summary" class="summary"></div>
  <div id="list"></div>

  <div class="footer">
    MOA合同会社｜老人ホーム紹介 ぬくもり<br>
    大阪市・豊中市・池田市・箕面市対応
  </div>

</div>

<script>
/* =====================================================
   MOA営業アプリ 完全版
   中央区・北区 地域包括支援センター入り
   ここに居宅介護支援事業所も追加できます
===================================================== */

const facilities = [
  {
    ward:"中央区",
    category:"地域包括支援センター",
    name:"中央区地域包括支援センター",
    address:"大阪市中央区上本町西2丁目5番25号",
    tel:"06-6763-8139",
    fax:"06-6763-8153",
    hours:"平日 9:00〜19:00／土曜 9:00〜17:30",
    area:"桃園・桃谷・東平・金甌・渥美・芦池・御津・大宝・道仁・高津・精華・河原地域",
    memo:"中央区南部・上町方面の高齢者総合相談窓口。老人ホーム紹介の連携挨拶先として優先。",
    priority:1
  },
  {
    ward:"中央区",
    category:"地域包括支援センター",
    name:"中央区北部地域包括支援センター",
    address:"大阪市中央区農人橋3丁目1番3号 ドミール堺筋本町1階",
    tel:"06-6944-2116",
    fax:"06-6944-2117",
    hours:"平日 9:00〜19:00／土曜 9:00〜17:00",
    area:"愛日・集英・中大江・南大江・玉造地域",
    memo:"本町・堺筋本町・谷町四丁目方面から営業しやすい地域包括。MOA事務所から近い訪問先。",
    priority:2
  },
  {
    ward:"北区",
    category:"地域包括支援センター",
    name:"北区地域包括支援センター",
    address:"大阪市北区神山町15-11",
    tel:"06-6313-5568",
    fax:"06-6314-6377",
    hours:"平日 9:00〜19:00／土曜 9:00〜17:00",
    area:"滝川・堀川・西天満・菅南・梅田東・北天満・済美・菅北・曽根崎・北野・堂島・中之島方面",
    memo:"梅田・中崎町・扇町方面から回りやすい北区の中心的な地域包括。",
    priority:3
  },
  {
    ward:"北区",
    category:"地域包括支援センター",
    name:"北区大淀地域包括支援センター",
    address:"大阪市北区長柄中1丁目1番21号",
    tel:"06-6354-1165",
    fax:"06-6354-1175",
    hours:"平日・土曜の開館時間は訪問前に要確認",
    area:"豊仁・豊崎東・本庄・豊崎・中津・大淀東・大淀西方面",
    memo:"天六・長柄・中津・大淀方面を回るときの優先訪問先。",
    priority:4
  },
  {
    ward:"北区",
    category:"総合相談窓口・ブランチ",
    name:"梅田東地域総合相談窓口・ブランチ",
    address:"大阪市北区芝田2丁目10番39号",
    tel:"06-6372-0804",
    fax:"06-6105-1361",
    hours:"訪問前に要確認",
    area:"梅田東・北天満・済美・曽根崎・堂島・中之島方面",
    memo:"梅田周辺の相談窓口。梅田方面の営業時に一緒に回りやすい。",
    priority:5
  },
  {
    ward:"北区",
    category:"総合相談窓口・ブランチ",
    name:"豊崎地域総合相談窓口・ブランチ",
    address:"大阪市北区本庄西2丁目6番15号",
    tel:"06-6371-6233",
    fax:"06-6371-6244",
    hours:"訪問前に要確認",
    area:"豊崎・本庄・中津方面",
    memo:"豊崎・中津方面の地域相談窓口。北区大淀地域包括とセットで回りやすい。",
    priority:6
  },

  /* =====================================================
     居宅介護支援事業所を入れる場合は、
     この下に同じ形で追加してください。
     例：
  ===================================================== */

  {
    ward:"中央区",
    category:"居宅介護支援事業所",
    name:"【例】中央区 居宅介護支援事業所",
    address:"大阪市中央区本町周辺",
    tel:"",
    fax:"",
    hours:"訪問前に確認",
    area:"中央区",
    memo:"ここはサンプルです。実際の居宅名・住所・電話番号に書き換えてください。",
    priority:99
  }
];

/* ===== Google Maps用 ===== */

function mapUrl(address){
  return "https://www.google.com/maps/search/?api=1&query=" + encodeURIComponent(address);
}

function routeUrl(address){
  return "https://www.google.com/maps/dir/?api=1&destination=" + encodeURIComponent(address);
}

function telUrl(tel){
  if(!tel) return "#";
  return "tel:" + tel.replaceAll("-", "");
}

/* ===== 表示 ===== */

function renderList(){
  const keyword = document.getElementById("keyword").value.trim().toLowerCase();
  const ward = document.getElementById("ward").value;
  const category = document.getElementById("category").value;

  let data = facilities.filter(item => {
    const text = [
      item.ward,
      item.category,
      item.name,
      item.address,
      item.tel,
      item.fax,
      item.hours,
      item.area,
      item.memo
    ].join(" ").toLowerCase();

    const okKeyword = !keyword || text.includes(keyword);
    const okWard = !ward || item.ward === ward;
    const okCategory = !category || item.category === category;

    return okKeyword && okWard && okCategory;
  });

  data.sort((a,b) => a.priority - b.priority);

  const list = document.getElementById("list");
  const summary = document.getElementById("summary");

  summary.textContent = "表示件数：" + data.length + "件";

  if(data.length === 0){
    list.innerHTML = `
      <div class="empty">
        該当する営業先がありません。<br>
        「北区」「中央区」「地域包括」「ブランチ」などで検索してください。
      </div>
    `;
    return;
  }

  list.innerHTML = data.map((item,index) => {
    let cardClass = "card";
    if(item.category === "地域包括支援センター") cardClass += " houkatsu";
    if(item.category === "総合相談窓口・ブランチ") cardClass += " branch";
    if(item.category === "居宅介護支援事業所") cardClass += " kyotaku";

    return `
      <div class="${cardClass}">
        <div class="tagline">
          <span class="tag">${index + 1}</span>
          <span class="tag">${item.ward}</span>
          <span class="tag">${item.category}</span>
        </div>

        <div class="name">${escapeHtml(item.name)}</div>

        <div class="info">📍 <strong>住所：</strong>${escapeHtml(item.address)}</div>
        <div class="info">☎️ <strong>電話：</strong>${item.tel ? escapeHtml(item.tel) : "未入力"}</div>
        <div class="info">📠 <strong>FAX：</strong>${item.fax ? escapeHtml(item.fax) : "未入力"}</div>
        <div class="info">🕘 <strong>時間：</strong>${escapeHtml(item.hours || "訪問前に確認")}</div>
        <div class="info">🗺️ <strong>担当・対象：</strong>${escapeHtml(item.area || "")}</div>

        <div class="memo">
          <strong>営業メモ：</strong><br>
          ${escapeHtml(item.memo || "")}
        </div>

        <div class="actions">
          <a class="tel" href="${telUrl(item.tel)}">電話</a>
          <a class="map" href="${mapUrl(item.address)}" target="_blank">地図</a>
          <a class="route" href="${routeUrl(item.address)}" target="_blank">ルート</a>
          <button class="copy" onclick="copyInfo(${facilities.indexOf(item)})">コピー</button>
        </div>
      </div>
    `;
  }).join("");
}

/* ===== リセット ===== */

function resetSearch(){
  document.getElementById("keyword").value = "";
  document.getElementById("ward").value = "";
  document.getElementById("category").value = "";
  renderList();
}

/* ===== 表示中の全ルート ===== */

function openAllRoute(){
  const keyword = document.getElementById("keyword").value.trim().toLowerCase();
  const ward = document.getElementById("ward").value;
  const category = document.getElementById("category").value;

  let data = facilities.filter(item => {
    const text = [
      item.ward,
      item.category,
      item.name,
      item.address,
      item.tel,
      item.fax,
      item.hours,
      item.area,
      item.memo
    ].join(" ").toLowerCase();

    const okKeyword = !keyword || text.includes(keyword);
    const okWard = !ward || item.ward === ward;
    const okCategory = !category || item.category === category;

    return okKeyword && okWard && okCategory;
  });

  data.sort((a,b) => a.priority - b.priority);

  if(data.length === 0){
    alert("表示中の営業先がありません。");
    return;
  }

  const destination = data[data.length - 1].address;
  const waypoints = data.slice(0, -1).map(x => x.address).join("|");

  let url = "https://www.google.com/maps/dir/?api=1";
  url += "&destination=" + encodeURIComponent(destination);

  if(waypoints){
    url += "&waypoints=" + encodeURIComponent(waypoints);
  }

  window.open(url, "_blank");
}

/* ===== コピー ===== */

function copyInfo(index){
  const item = facilities[index];

  const text = `
【${item.ward}】${item.category}
${item.name}

住所：${item.address}
電話：${item.tel || "未入力"}
FAX：${item.fax || "未入力"}
時間：${item.hours || "訪問前に確認"}
担当・対象：${item.area || ""}
営業メモ：${item.memo || ""}
地図：${mapUrl(item.address)}
`;

  navigator.clipboard.writeText(text).then(() => {
    alert("コピーしました。営業メモやLINE・メールに貼れます。");
  }).catch(() => {
    alert("コピーできませんでした。");
  });
}

/* ===== 文字化け・HTML崩れ防止 ===== */

function escapeHtml(str){
  if(!str) return "";
  return String(str)
    .replaceAll("&","&amp;")
    .replaceAll("<","&lt;")
    .replaceAll(">","&gt;")
    .replaceAll('"',"&quot;")
    .replaceAll("'","&#039;");
}

/* ===== 最初に一覧表示 ===== */

renderList();
</script>

</body>
</html>

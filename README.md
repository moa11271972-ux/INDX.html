<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>北区 居宅介護支援事業者 営業アプリ</title>
<style>
body{
  font-family:-apple-system,BlinkMacSystemFont,"Yu Gothic",sans-serif;
  background:#f3f6fb;
  margin:0;
  padding:12px;
  color:#222;
}
h1{
  font-size:21px;
  color:#17406f;
  margin:10px 0 5px;
}
.sub{
  font-size:13px;
  color:#666;
  margin-bottom:10px;
}
.box{
  background:#fff;
  padding:12px;
  border-radius:14px;
  margin-bottom:12px;
  box-shadow:0 3px 10px rgba(0,0,0,0.08);
}
input,select,textarea{
  width:100%;
  box-sizing:border-box;
  padding:11px;
  margin:5px 0;
  border:1px solid #ccc;
  border-radius:10px;
  font-size:15px;
}
button{
  border:none;
  border-radius:10px;
  padding:10px 12px;
  margin:4px 2px;
  font-weight:bold;
  cursor:pointer;
}
.main{background:#1f6feb;color:white;}
.reset{background:#555;color:white;}
.routeAll{background:#7c3aed;color:white;}
.copy{background:#0f766e;color:white;}
.tel{background:#16a34a;color:white;}
.map{background:#2563eb;color:white;}
.route{background:#9333ea;color:white;}
.done{background:#facc15;color:#222;}
.card{
  background:white;
  padding:13px;
  margin-bottom:10px;
  border-radius:14px;
  border-left:6px solid #1f6feb;
  box-shadow:0 3px 10px rgba(0,0,0,0.08);
}
.card.doneCard{
  opacity:.55;
  border-left-color:#999;
}
.name{
  font-size:17px;
  font-weight:bold;
  margin-bottom:6px;
}
.info{
  font-size:14px;
  line-height:1.7;
}
.badge{
  display:inline-block;
  background:#e8f0ff;
  color:#17406f;
  border-radius:999px;
  padding:3px 8px;
  font-size:12px;
  margin:2px 2px 5px 0;
}
.notice{
  background:#fff8d7;
  font-size:13px;
  line-height:1.7;
}
#count{
  font-weight:bold;
  color:#17406f;
}
</style>
</head>

<body>

<h1>北区 居宅介護支援事業者 営業アプリ</h1>
<div class="sub">MOA合同会社｜老人ホーム紹介 ぬくもり｜営業用</div>

<div class="box notice">
表示されない時は、GitHubの index.html を全部このコードに上書きしてください。  
検索、電話、地図、巡回ルート、CSV追加ができます。
</div>

<div class="box">
  <input id="keyword" placeholder="検索：北区、天神橋、中崎、南森町、本庄、大淀、梅田など">

  <select id="area">
    <option value="">エリア指定なし</option>
    <option value="梅田・中津">梅田・中津</option>
    <option value="中崎・天六">中崎・天六</option>
    <option value="南森町・天満">南森町・天満</option>
    <option value="本庄・大淀">本庄・大淀</option>
  </select>

  <button class="main" onclick="showList()">検索</button>
  <button class="reset" onclick="resetSearch()">リセット</button>
  <button class="routeAll" onclick="openRouteAll()">表示中の巡回ルート</button>
  <button class="copy" onclick="copyCSV()">CSVコピー</button>
</div>

<div class="box">
  <b>CSV追加</b>
  <div class="sub">形式：事業所名,住所,電話番号,エリア</div>
  <textarea id="csvInput" rows="4" placeholder="例：
サンプルケアプランセンター,大阪市北区〇〇1-2-3,06-0000-0000,南森町・天満"></textarea>
  <button class="main" onclick="addCSV()">CSVを追加</button>
</div>

<div class="box">
  表示件数：<span id="count">0</span>件
</div>

<div id="list"></div>

<script>
var baseCSV = `
社会福祉法人恩賜財団済生会支部大阪府済生会中津病院,大阪市北区芝田二丁目10番39号,06-6372-0733,梅田・中津
有限会社介護ステーションヘイル,大阪市北区鶴野町4番11-903号 朝日プラザ梅田,06-4802-2084,梅田・中津
居宅介護支援事業所せいび,大阪市北区中崎西三丁目3番40号,06-6485-2283,中崎・天六
アリーケアプランセンター,大阪市北区中崎西一丁目4番22-305号 梅田東ビル,072-260-9486,中崎・天六
sfee,大阪市北区中崎西三丁目2番7号,06-6476-8255,中崎・天六
ケアプランセンター蓮,大阪市北区中崎西四丁目3番32-802号 ARCA梅田ビル8階,06-6131-7075,中崎・天六
医療福祉生協おおさかいきいきケアプランセンター,大阪市北区中崎一丁目6番20号,06-4802-4366,中崎・天六
社会医療法人行岡医学研究会行岡病院,大阪市北区浮田二丁目2番3号,06-6371-9921,中崎・天六
ケアプランセンタータオ,大阪市北区浪花町13番38号 千代田ビル北館6階B号室,06-6486-9618,中崎・天六
あいあいケアセンター中崎通り,大阪市北区浪花町5番7号,06-6292-4530,中崎・天六
あんじゅケアプランセンター,大阪市北区山崎町1番6号,06-6374-2170,中崎・天六
北区在宅サービスセンター いきいきネット,大阪市北区神山町15番11号,06-6313-1911,梅田・中津
医師会立北区訪問看護ステーション,大阪市北区神山町15番11号,06-6313-1415,梅田・中津
ケアセンターてんま,大阪市北区池田町12-10,06-6136-0200,南森町・天満
リンクケアプラン,大阪市北区松ケ枝町6番1-603号 グロウビル,090-8367-4091,南森町・天満
グッドライフケア居宅介護支援センター大阪北,大阪市北区紅梅町1番6号 カザリーノビル6階,06-6809-5570,南森町・天満
ケアサービスダンデライオン,大阪市北区天神橋五丁目7番10号 さかしん天神橋ビル7F,06-4801-8322,中崎・天六
ケアクル居宅介護支援センター,大阪市北区天神橋二丁目2番10-301号,06-6351-2177,南森町・天満
匠ケア,大阪市北区天神橋二丁目北1番21号 八千代ビル東館2K号,06-6967-9993,南森町・天満
株式会社KOSMOホームヘルプサービス大阪事業所,大阪市北区天神橋二丁目2番10-501号 ハイ・マウントビル,06-4309-6672,南森町・天満
ひかり介護サービス,大阪市北区天神橋三丁目2番31号,06-4801-9754,南森町・天満
居宅介護支援事業所ほりかわ,大阪市北区天神橋二丁目北1番2号,06-6351-8281,南森町・天満
クローバー居宅介護支援事業所,大阪市北区天神橋五丁目6番23号,06-6352-8470,中崎・天六
天神介護サービス,大阪市北区天神橋三丁目7番18-302号 三海ビル,06-6353-2012,南森町・天満
アリスケア,大阪市北区天神橋五丁目8番12号 大河崎ビル6階,06-6809-1168,中崎・天六
トータルサービス冨士田,大阪市北区天神橋一丁目18番25号,06-6352-0567,南森町・天満
アンポートケアプランセンター,大阪市北区天満二丁目9番13号,06-4801-8373,南森町・天満
すこやか介護ケアプランセンター,大阪市北区天神西町1番6号 アールビル天神西8F,06-6940-4160,南森町・天満
ピースケアプランセンター,大阪市北区菅原町11番10号 オーキッド中之島402号North,06-6361-0075,南森町・天満
ケアプランセンターMSC,大阪市北区西天満三丁目13番20号 ASビル6階,06-6232-8263,南森町・天満
ケアプランセンターあずき,大阪市北区南森町一丁目3番29-1004号,06-6926-4275,南森町・天満
株式会社ハート介護サービス居宅介護支援事業所,大阪市北区南森町二丁目2番9号 南森町八千代ビル1階,06-6362-3368,南森町・天満
ケアプランセンターひまわりの苑,大阪市北区曽根崎一丁目1番20号,06-7501-8688,梅田・中津
きん柑ケアプランセンター北,大阪市北区天神橋七丁目3番2-604号 大山ビル,06-4792-8859,中崎・天六
えすぽわーるこころ,大阪市北区天神橋七丁目10番2号 喜住ビル1F,06-6766-4147,中崎・天六
ケアプランセンター寿梨の里,大阪市北区天神橋七丁目15番2-101号,06-6360-9323,中崎・天六
まごころケア北,大阪市北区長柄西一丁目1番16号,06-6352-0830,中崎・天六
ハートフルかのうケアプランセンター,大阪市北区長柄中一丁目1番21号,06-6354-1108,中崎・天六
エルケア株式会社エルケア長柄ケアプランセンター,大阪市北区長柄東二丁目8番36号 淀川リバーサイド・ビーネ2階,06-7688-5078,中崎・天六
ケア21北,大阪市北区国分寺二丁目1番14号 ACOM天六ビル5階,06-7167-2421,中崎・天六
株式会社ソニックコーポレーショントータルケアサービス,大阪市北区中津七丁目3番7-301号,06-6457-0207,梅田・中津
居宅介護支援事業所藤ミレニアム,大阪市北区本庄西二丁目6番15号,06-6371-6322,本庄・大淀
ケアプランセンターアセス,大阪市北区本庄西一丁目9番12号 朝日プラザ北梅田1F東側,06-6486-9073,本庄・大淀
なでしこケアプランセンター,大阪市北区本庄西二丁目15番12号,06-6373-1724,本庄・大淀
ユアーズ介護ケアプランオフィス,大阪市北区本庄東二丁目2番25号 クリエイト天八ビル7階,06-6373-7224,本庄・大淀
もりたケアプランセンター,大阪市北区本庄東二丁目1番23-202号 スペチアーレ,06-6131-9740,本庄・大淀
もこもこセンター,大阪市北区本庄東二丁目12番15号,06-7651-6935,本庄・大淀
介護ステーションワンピース,大阪市北区本庄東三丁目10番22号,06-6373-4033,本庄・大淀
愛と心の居宅介護支援センター大阪,大阪市北区本庄東一丁目14番4号,06-6305-8008,本庄・大淀
居宅介護支援事業所淳風おおさか,大阪市北区大淀南二丁目5番20号,06-6450-1140,本庄・大淀
ケアプランセンターあいわ,大阪市北区大淀中四丁目6番16号,06-6345-7832,本庄・大淀
支援事業所大阪北,大阪市北区大淀中五丁目5番8号,06-7174-4425,本庄・大淀
`;

var data = [];
var doneList = JSON.parse(localStorage.getItem("kita_done") || "[]");

function loadData(){
  data = [];
  var lines = baseCSV.trim().split("\n");
  for(var i=0;i<lines.length;i++){
    var c = lines[i].split(",");
    data.push({
      name:c[0] || "",
      address:c[1] || "",
      tel:c[2] || "",
      area:c[3] || "北区"
    });
  }

  var add = JSON.parse(localStorage.getItem("kita_added") || "[]");
  data = data.concat(add);
}

function clean(t){
  return String(t || "")
    .toLowerCase()
    .replace(/　/g," ")
    .replace(/[０-９]/g,function(s){return String.fromCharCode(s.charCodeAt(0)-65248);});
}

function getItems(){
  var key = clean(document.getElementById("keyword").value);
  var area = document.getElementById("area").value;

  return data.filter(function(x){
    var target = clean(x.name + " " + x.address + " " + x.tel + " " + x.area);
    var ok1 = key === "" || target.indexOf(key) !== -1;
    var ok2 = area === "" || x.area === area;
    return ok1 && ok2;
  });
}

function showList(){
  loadData();

  var list = document.getElementById("list");
  var items = getItems();
  document.getElementById("count").textContent = items.length;
  list.innerHTML = "";

  if(items.length === 0){
    list.innerHTML = "<div class='card'>表示できる事業所がありません。検索を短くしてください。例：天神橋、中崎、南森町、本庄</div>";
    return;
  }

  for(var i=0;i<items.length;i++){
    var x = items[i];
    var id = x.name + x.address;
    var isDone = doneList.indexOf(id) !== -1;

    var mapUrl = "https://www.google.com/maps/search/?api=1&query=" + encodeURIComponent(x.address);
    var routeUrl = "https://www.google.com/maps/dir/?api=1&destination=" + encodeURIComponent(x.address) + "&travelmode=walking";

    var div = document.createElement("div");
    div.className = "card" + (isDone ? " doneCard" : "");

    div.innerHTML =
      "<div class='name'>" + (i+1) + ". " + x.name + "</div>" +
      "<span class='badge'>" + x.area + "</span>" +
      "<span class='badge'>居宅介護支援</span>" +
      "<div class='info'>" +
      "住所：" + x.address + "<br>" +
      "電話：" + x.tel +
      "</div>" +
      "<div>" +
      "<a href='tel:" + x.tel + "'><button class='tel'>電話</button></a>" +
      "<a href='" + mapUrl + "' target='_blank'><button class='map'>地図</button></a>" +
      "<a href='" + routeUrl + "' target='_blank'><button class='route'>ここへ行く</button></a>" +
      "<button class='done' onclick='toggleDone(" + JSON.stringify(id) + ")'>" + (isDone ? "営業済み解除" : "営業済み") + "</button>" +
      "</div>";

    list.appendChild(div);
  }
}

function toggleDone(id){
  var n = doneList.indexOf(id);
  if(n === -1){
    doneList.push(id);
  }else{
    doneList.splice(n,1);
  }
  localStorage.setItem("kita_done", JSON.stringify(doneList));
  showList();
}

function resetSearch(){
  document.getElementById("keyword").value = "";
  document.getElementById("area").value = "";
  showList();
}

function openRouteAll(){
  var items = getItems().slice(0,9);

  if(items.length === 0){
    alert("ルートにする事業所がありません");
    return;
  }

  var destination = items[items.length-1].address;
  var waypoints = items.slice(0,items.length-1).map(function(x){return x.address;}).join("|");

  var url = "https://www.google.com/maps/dir/?api=1";
  url += "&origin=" + encodeURIComponent("大阪市北区");
  url += "&destination=" + encodeURIComponent(destination);
  if(waypoints){
    url += "&waypoints=" + encodeURIComponent(waypoints);
  }
  url += "&travelmode=walking";

  window.open(url,"_blank");
}

function addCSV(){
  var text = document.getElementById("csvInput").value.trim();
  if(!text){
    alert("CSVを入れてください");
    return;
  }

  var added = JSON.parse(localStorage.getItem("kita_added") || "[]");
  var lines = text.split("\n");

  for(var i=0;i<lines.length;i++){
    var c = lines[i].split(",");
    if(c.length >= 3){
      added.push({
        name:c[0] || "",
        address:c[1] || "",
        tel:c[2] || "",
        area:c[3] || "北区"
      });
    }
  }

  localStorage.setItem("kita_added", JSON.stringify(added));
  document.getElementById("csvInput").value = "";
  alert("追加しました");
  showList();
}

function copyCSV(){
  var items = getItems();
  var csv = "事業所名,住所,電話番号,エリア\n";
  for(var i=0;i<items.length;i++){
    csv += '"' + items[i].name + '","' + items[i].address + '","' + items[i].tel + '","' + items[i].area + '"\n';
  }

  navigator.clipboard.writeText(csv).then(function(){
    alert("CSVをコピーしました");
  });
}

window.onload = function(){
  showList();
};
</script>

</body>
</html>

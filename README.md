<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>MOA営業アプリ｜中央区・北区 地域包括・居宅</title>

<style>
*{box-sizing:border-box;}

body{
  margin:0;
  font-family:-apple-system,BlinkMacSystemFont,"Hiragino Sans","Yu Gothic",Meiryo,sans-serif;
  background:#f4f1ec;
  color:#2f2a25;
}

header{
  background:linear-gradient(135deg,#4b3628,#9a7a54);
  color:#fff;
  padding:18px 12px;
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
  min-height:90px;
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
.btn-orange{background:#d9822b;color:#fff;}
.btn-red{background:#b94b4b;color:#fff;}

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

.card.houkatsu{border-left-color:#2f6fbd;}
.card.branch{border-left-color:#d9822b;}
.card.kyotaku{border-left-color:#2f8f5b;}

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

.tel{background:#2f8f5b;}
.map{background:#2f6fbd;}
.route{background:#d9822b;}
.copy{background:#5b4636;}

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
  <h1>MOA営業アプリ<br>中央区・北区 地域包括・居宅</h1>
  <p>老人ホーム紹介 ぬくもり｜営業訪問・電話・地図・ルート確認</p>
</header>

<div class="wrap">

  <div class="notice">
    ※このアプリは営業訪問の補助用です。電話番号・所在地は変更される場合があります。訪問前に必ず公式情報または電話で確認してください。<br>
    ※説明時は「無料の老人ホーム紹介」「施設情報の提供」「見学同行・入居手続きサポート」として案内し、法律相談・契約判断の代行は行わない表現にしてください。
  </div>

  <div class="controls">
    <div class="row">
      <div class="col">
        <input id="keyword" type="text" placeholder="例：北区、中央区、本町、梅田、天神橋、居宅、地域包括">
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
      <button class="btn-orange" onclick="openAllRoute()">表示中ルート</button>
    </div>
  </div>

  <div class="controls">
    <strong>CSVで営業先を追加</strong>
    <p class="small">
      形式：区,種別,名前,住所,電話,FAX,メモ<br>
      例：北区,居宅介護支援事業所,〇〇ケアプランセンター,大阪市北区〇〇1-1-1,06-0000-0000,06-0000-0001,営業メモ
    </p>
    <textarea id="csvInput" placeholder="ここにCSVを貼り付け"></textarea>
    <div class="row">
      <button class="btn-green" onclick="importCsv()">CSVを追加する</button>
      <button class="btn-red" onclick="clearAddedData()">追加データを消す</button>
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
   中央区・北区 地域包括支援センター・ブランチ・居宅介護支援事業所
===================================================== */

const baseHoukatsu = [
  {
    ward:"中央区",
    category:"地域包括支援センター",
    name:"中央区地域包括支援センター",
    address:"大阪市中央区上本町西2-5-25",
    tel:"06-6763-8139",
    fax:"06-6763-8151",
    hours:"訪問前に確認",
    area:"中央区南部・上本町西方面",
    memo:"中央区の地域包括支援センター。居宅・高齢者相談の連携挨拶先。",
    priority:1
  },
  {
    ward:"中央区",
    category:"地域包括支援センター",
    name:"中央区北部地域包括支援センター",
    address:"大阪市中央区農人橋3-1-3 ドミール堺筋本町1階",
    tel:"06-6944-2116",
    fax:"06-6944-2117",
    hours:"訪問前に確認",
    area:"本町・堺筋本町・谷町四丁目方面",
    memo:"MOA事務所から近く、営業起点にしやすい地域包括。",
    priority:2
  },
  {
    ward:"北区",
    category:"地域包括支援センター",
    name:"北区地域包括支援センター",
    address:"大阪市北区神山町15-11",
    tel:"06-6313-5568",
    fax:"06-6314-6377",
    hours:"平日9:00〜19:00／土曜9:00〜17:00",
    area:"梅田・中崎町・扇町・西天満・堂島・中之島方面",
    memo:"北区中心部の高齢者総合相談窓口。",
    priority:3
  },
  {
    ward:"北区",
    category:"地域包括支援センター",
    name:"北区大淀地域包括支援センター",
    address:"大阪市北区長柄中1-1-21",
    tel:"06-6354-1165",
    fax:"06-6354-1175",
    hours:"訪問前に確認",
    area:"長柄・豊崎・中津・大淀方面",
    memo:"北区北部・大淀方面の地域包括。",
    priority:4
  },
  {
    ward:"北区",
    category:"総合相談窓口・ブランチ",
    name:"梅田東地域総合相談窓口・ブランチ",
    address:"大阪市北区芝田2-10-39",
    tel:"06-6372-0804",
    fax:"06-6105-1361",
    hours:"訪問前に確認",
    area:"梅田東・曽根崎・堂島・中之島方面",
    memo:"梅田周辺の相談窓口。梅田方面の営業時に回りやすい。",
    priority:5
  },
  {
    ward:"北区",
    category:"総合相談窓口・ブランチ",
    name:"豊崎地域総合相談窓口・ブランチ",
    address:"大阪市北区本庄西2-6-15",
    tel:"06-6371-6233",
    fax:"06-6371-6244",
    hours:"訪問前に確認",
    area:"豊崎・本庄・中津方面",
    memo:"豊崎・中津方面の営業時に回りやすい。",
    priority:6
  }
];

const baseKyotaku = [
  /* =========================
     中央区 居宅介護支援事業所
  ========================= */
  {ward:"中央区",category:"居宅介護支援事業所",name:"あいあいケア中央",address:"大阪市中央区谷町6-2-30 川島機械ビル2階",tel:"06-6191-2222",fax:"06-6191-2223",memo:"中央区居宅介護支援事業所",priority:101},
  {ward:"中央区",category:"居宅介護支援事業所",name:"愛フジックス居宅介護支援事業所",address:"大阪市中央区谷町7-3-4 新谷町第3ビル203",tel:"06-6768-1771",fax:"06-6767-5310",memo:"中央区居宅介護支援事業所",priority:102},
  {ward:"中央区",category:"居宅介護支援事業所",name:"あやめケアプランセンター",address:"大阪市中央区大手通3-3-3 日宝東本町ビル6階1号",tel:"06-4790-8226",fax:"06-4790-8227",memo:"中央区居宅介護支援事業所",priority:103},
  {ward:"中央区",category:"居宅介護支援事業所",name:"うえに生協診療所ケアプランセンター",address:"大阪市中央区玉造1-8-10 にじ玉造ビル4階",tel:"06-6718-4140",fax:"06-6718-4141",memo:"中央区居宅介護支援事業所",priority:104},
  {ward:"中央区",category:"居宅介護支援事業所",name:"NPOあったかい手",address:"大阪市中央区安堂寺町1-4-12-201 ヴェルドール安堂寺",tel:"06-6767-8103",fax:"06-6767-8104",memo:"中央区居宅介護支援事業所",priority:105},
  {ward:"中央区",category:"居宅介護支援事業所",name:"エールシステムズⅠ",address:"大阪市中央区難波3-6-11 なんば池田ビル10階",tel:"06-6634-1590",fax:"06-6634-1589",memo:"中央区居宅介護支援事業所",priority:106},
  {ward:"中央区",category:"居宅介護支援事業所",name:"大阪ろうあ会館",address:"大阪市中央区谷町5-4-13 谷町福祉センター4階",tel:"06-6761-1394",fax:"06-6768-3833",memo:"中央区居宅介護支援事業所",priority:107},
  {ward:"中央区",category:"居宅介護支援事業所",name:"おとしよりケアプランセンター",address:"大阪市中央区島之内2-12-28",tel:"06-6212-3261",fax:"06-6212-3497",memo:"中央区居宅介護支援事業所",priority:108},
  {ward:"中央区",category:"居宅介護支援事業所",name:"オリーブの森",address:"大阪市中央区玉造2-26-70-305",tel:"06-4302-5190",fax:"06-4302-5191",memo:"中央区居宅介護支援事業所",priority:109},
  {ward:"中央区",category:"居宅介護支援事業所",name:"居宅介護支援事業所アバンダンス",address:"大阪市中央区久太郎町2-2-7 山口興産堺筋本町ビル7階",tel:"06-4963-3224",fax:"06-6261-5621",memo:"中央区居宅介護支援事業所",priority:110},
  {ward:"中央区",category:"居宅介護支援事業所",name:"居宅介護支援といろ",address:"大阪市中央区安土町1-6-22 グランドメゾン船場905",tel:"06-6263-1016",fax:"06-6262-6606",memo:"中央区居宅介護支援事業所",priority:111},
  {ward:"中央区",category:"居宅介護支援事業所",name:"くおるとケアプランセンター",address:"大阪市中央区高津3-8-20-101",tel:"06-6636-0605",fax:"06-7635-8127",memo:"中央区居宅介護支援事業所",priority:112},
  {ward:"中央区",category:"居宅介護支援事業所",name:"グッドライフケア居宅介護支援センター大阪中央",address:"大阪市中央区南船場3-3-5 OKTビル5階",tel:"06-4708-3900",fax:"06-6227-8440",memo:"中央区居宅介護支援事業所",priority:113},
  {ward:"中央区",category:"居宅介護支援事業所",name:"ケア21 中央",address:"大阪市中央区谷町6-1-14 谷町大治ビル3階A室",tel:"06-4304-7325",fax:"06-4304-7327",memo:"中央区居宅介護支援事業所",priority:114},
  {ward:"中央区",category:"居宅介護支援事業所",name:"ケアプランセンターそら",address:"大阪市中央区内本町1-3-10-306",tel:"06-4790-1440",fax:"06-4790-1441",memo:"中央区居宅介護支援事業所",priority:115},
  {ward:"中央区",category:"居宅介護支援事業所",name:"ケアプランセンターナービス大阪",address:"大阪市中央区高麗橋1-7-3",tel:"06-7506-9674",fax:"06-7506-9067",memo:"中央区居宅介護支援事業所",priority:116},
  {ward:"中央区",category:"居宅介護支援事業所",name:"ケアプランセンターぷらっと",address:"大阪市中央区松屋町9-1 セントラルフォーラム4階",tel:"06-6115-8766",fax:"06-6777-5689",memo:"中央区居宅介護支援事業所",priority:117},
  {ward:"中央区",category:"居宅介護支援事業所",name:"こころ",address:"大阪市中央区上汐2-1-23 心幸ピースビル3階",tel:"06-6191-0556",fax:"06-6191-0557",memo:"中央区居宅介護支援事業所",priority:118},
  {ward:"中央区",category:"居宅介護支援事業所",name:"たむらソーシャルネット",address:"大阪市中央区谷町6-14-23",tel:"06-6766-7071",fax:"06-6766-7081",memo:"中央区居宅介護支援事業所",priority:119},
  {ward:"中央区",category:"居宅介護支援事業所",name:"中央区在宅サービスセンター",address:"大阪市中央区上本町西2-5-25",tel:"06-6763-8139",fax:"06-6763-8151",memo:"中央区居宅介護支援事業所",priority:120},
  {ward:"中央区",category:"居宅介護支援事業所",name:"ニチイケアセンター難波",address:"大阪市中央区南船場2-6-10 ツチノビル2階2",tel:"06-4964-8531",fax:"06-4964-8535",memo:"中央区居宅介護支援事業所",priority:121},
  {ward:"中央区",category:"居宅介護支援事業所",name:"パインケアプランセンター中央",address:"大阪市中央区南久宝寺町2-1-9 船場メディカルビル5F",tel:"06-6224-0924",fax:"06-6224-0925",memo:"中央区居宅介護支援事業所",priority:122},
  {ward:"中央区",category:"居宅介護支援事業所",name:"パルフェ",address:"大阪市中央区上本町西1-2-14 第3松屋ビル1153",tel:"06-6764-0738",fax:"06-6764-0739",memo:"中央区居宅介護支援事業所",priority:123},
  {ward:"中央区",category:"居宅介護支援事業所",name:"法円坂ケアプランセンター",address:"大阪市中央区谷町4-5-9 谷町アークビル1104",tel:"06-6949-5672",fax:"06-6947-7806",memo:"中央区居宅介護支援事業所",priority:124},
  {ward:"中央区",category:"居宅介護支援事業所",name:"まっちゃ町ケアステーション",address:"大阪市中央区谷町7-6-14",tel:"06-6764-7856",fax:"06-6764-7866",memo:"中央区居宅介護支援事業所",priority:125},
  {ward:"中央区",category:"居宅介護支援事業所",name:"南大江地域在宅サービスステーション さくら居宅介護支援事業所",address:"大阪市中央区農人橋1-4-20",tel:"06-6947-3271",fax:"06-6947-5213",memo:"中央区居宅介護支援事業所",priority:126},
  {ward:"中央区",category:"居宅介護支援事業所",name:"みんとケアプランセンター",address:"大阪市中央区安堂寺町2-2-24 ニッシンビル201",tel:"06-6191-0677",fax:"06-6191-0678",memo:"中央区居宅介護支援事業所",priority:127},
  {ward:"中央区",category:"居宅介護支援事業所",name:"よつ葉ケアプランセンター",address:"大阪市中央区玉造1-6-22 ジュネス玉造505",tel:"06-6762-6987",fax:"06-6762-6986",memo:"中央区居宅介護支援事業所",priority:128},
  {ward:"中央区",category:"居宅介護支援事業所",name:"ライフ居宅支援センター",address:"大阪市中央区本町4-4-17 RE-012 610",tel:"06-6484-5410",fax:"06-7635-5622",memo:"中央区居宅介護支援事業所",priority:129},
  {ward:"中央区",category:"居宅介護支援事業所",name:"らくゆう会ケアプランセンター",address:"大阪市中央区久太郎町1-4-4 JKビル1階",tel:"06-6262-6767",fax:"06-6262-6688",memo:"中央区居宅介護支援事業所",priority:130},
  {ward:"中央区",category:"居宅介護支援事業所",name:"小規模多機能 フレンド大阪中央",address:"大阪市中央区高津3-14-26",tel:"06-6634-7081",fax:"06-6634-7082",memo:"中央区居宅介護支援事業所",priority:131},

  /* =========================
     北区 居宅介護支援事業所
  ========================= */
  {ward:"北区",category:"居宅介護支援事業所",name:"社会福祉法人恩賜財団済生会支部大阪府済生会中津病院",address:"大阪市北区芝田2-10-39",tel:"06-6372-0733",fax:"06-6372-0752",memo:"北区居宅介護支援事業所",priority:201},
  {ward:"北区",category:"居宅介護支援事業所",name:"有限会社介護ステーションヘイル",address:"大阪市北区鶴野町4-11-903 朝日プラザ梅田",tel:"06-4802-2084",fax:"06-4802-2086",memo:"北区居宅介護支援事業所",priority:202},
  {ward:"北区",category:"居宅介護支援事業所",name:"居宅介護支援事業所せいび",address:"大阪市北区中崎西3-3-40",tel:"06-6485-2283",fax:"06-6485-2283",memo:"北区居宅介護支援事業所",priority:203},
  {ward:"北区",category:"居宅介護支援事業所",name:"アリーケアプランセンター",address:"大阪市北区中崎西1-4-22-305 梅田東ビル",tel:"072-260-9486",fax:"06-7739-5316",memo:"北区居宅介護支援事業所",priority:204},
  {ward:"北区",category:"居宅介護支援事業所",name:"sfee",address:"大阪市北区中崎西3-2-7",tel:"06-6476-8255",fax:"06-6476-8256",memo:"北区居宅介護支援事業所",priority:205},
  {ward:"北区",category:"居宅介護支援事業所",name:"ケアプランセンター蓮",address:"大阪市北区中崎西4-3-32-802 ARCA梅田ビル8階",tel:"06-6131-7075",fax:"06-6131-8803",memo:"北区居宅介護支援事業所",priority:206},
  {ward:"北区",category:"居宅介護支援事業所",name:"医療福祉生協おおさかいきいきケアプランセンター",address:"大阪市北区中崎1-6-20",tel:"06-4802-4366",fax:"06-4802-3511",memo:"北区居宅介護支援事業所",priority:207},
  {ward:"北区",category:"居宅介護支援事業所",name:"社会医療法人行岡医学研究会行岡病院",address:"大阪市北区浮田2-2-3",tel:"06-6371-9921",fax:"06-6371-4199",memo:"北区居宅介護支援事業所",priority:208},
  {ward:"北区",category:"居宅介護支援事業所",name:"ケアプランセンタータオ",address:"大阪市北区浪花町13-38 千代田ビル北館6階B号室",tel:"06-6486-9618",fax:"06-6476-8245",memo:"北区居宅介護支援事業所",priority:209},
  {ward:"北区",category:"居宅介護支援事業所",name:"あいあいケアセンター中崎通り",address:"大阪市北区浪花町5-7",tel:"06-6292-4530",fax:"06-6292-4534",memo:"北区居宅介護支援事業所",priority:210},
  {ward:"北区",category:"居宅介護支援事業所",name:"あんじゅケアプランセンター",address:"大阪市北区山崎町1-6",tel:"06-6374-2170",fax:"06-6374-2171",memo:"北区居宅介護支援事業所",priority:211},
  {ward:"北区",category:"居宅介護支援事業所",name:"北区在宅サービスセンター（いきいきネット）",address:"大阪市北区神山町15-11",tel:"06-6313-1911",fax:"06-6314-6377",memo:"北区居宅介護支援事業所",priority:212},
  {ward:"北区",category:"居宅介護支援事業所",name:"医師会立北区訪問看護ステーション",address:"大阪市北区神山町15-11",tel:"06-6313-1415",fax:"06-6313-1416",memo:"北区居宅介護支援事業所",priority:213},
  {ward:"北区",category:"居宅介護支援事業所",name:"ケアセンターてんま",address:"大阪市北区池田町12-10",tel:"06-6136-0200",fax:"06-6136-0202",memo:"北区居宅介護支援事業所",priority:214},
  {ward:"北区",category:"居宅介護支援事業所",name:"リンクケアプラン",address:"大阪市北区松ケ枝町6-1-603 グロウビル",tel:"090-8367-4091",fax:"",memo:"北区居宅介護支援事業所",priority:215},
  {ward:"北区",category:"居宅介護支援事業所",name:"グッドライフケア居宅介護支援センター大阪北",address:"大阪市北区紅梅町1-6 カザリーノビル6階",tel:"06-6809-5570",fax:"06-6948-6521",memo:"北区居宅介護支援事業所",priority:216},
  {ward:"北区",category:"居宅介護支援事業所",name:"ケアサービスダンデライオン",address:"大阪市北区天神橋5-7-10 さかしん天神橋ビル7F",tel:"06-4801-8322",fax:"06-4801-8344",memo:"北区居宅介護支援事業所",priority:217},
  {ward:"北区",category:"居宅介護支援事業所",name:"ケアクル居宅介護支援センター",address:"大阪市北区天神橋2-2-10-301",tel:"06-6351-2177",fax:"06-6351-2178",memo:"北区居宅介護支援事業所",priority:218},
  {ward:"北区",category:"居宅介護支援事業所",name:"匠ケア",address:"大阪市北区天神橋2丁目北1-21 八千代ビル東館2K号",tel:"06-6967-9993",fax:"06-6967-9994",memo:"北区居宅介護支援事業所",priority:219},
  {ward:"北区",category:"居宅介護支援事業所",name:"株式会社KOSMOホームヘルプサービス大阪事業所",address:"大阪市北区天神橋2-2-10-501 ハイ・マウントビル",tel:"06-4309-6672",fax:"06-4309-6673",memo:"北区居宅介護支援事業所",priority:220},
  {ward:"北区",category:"居宅介護支援事業所",name:"ひかり介護サービス",address:"大阪市北区天神橋3-2-31",tel:"06-4801-9754",fax:"06-4801-9755",memo:"北区居宅介護支援事業所",priority:221},
  {ward:"北区",category:"居宅介護支援事業所",name:"居宅介護支援事業所ほりかわ",address:"大阪市北区天神橋2丁目北1-2",tel:"06-6351-8281",fax:"06-6351-8298",memo:"北区居宅介護支援事業所",priority:222},
  {ward:"北区",category:"居宅介護支援事業所",name:"クローバー居宅介護支援事業所",address:"大阪市北区天神橋5-6-23",tel:"06-6352-8470",fax:"06-6352-8472",memo:"北区居宅介護支援事業所",priority:223},
  {ward:"北区",category:"居宅介護支援事業所",name:"天神介護サービス",address:"大阪市北区天神橋3-7-18-302 三海ビル",tel:"06-6353-2012",fax:"06-6353-2013",memo:"北区居宅介護支援事業所",priority:224},
  {ward:"北区",category:"居宅介護支援事業所",name:"アリスケア",address:"大阪市北区天神橋5-8-12 大河崎ビル6階",tel:"06-6809-1168",fax:"06-6809-1169",memo:"北区居宅介護支援事業所",priority:225},
  {ward:"北区",category:"居宅介護支援事業所",name:"トータルサービス冨士田",address:"大阪市北区天神橋1-18-25",tel:"06-6352-0567",fax:"06-6352-2900",memo:"北区居宅介護支援事業所",priority:226},
  {ward:"北区",category:"居宅介護支援事業所",name:"アンポートケアプランセンター",address:"大阪市北区天満2-9-13",tel:"06-4801-8373",fax:"06-4801-8372",memo:"北区居宅介護支援事業所",priority:227},
  {ward:"北区",category:"居宅介護支援事業所",name:"すこやか介護ケアプランセンター",address:"大阪市北区天神西町1-6 アールビル天神西8F",tel:"06-6940-4160",fax:"06-6940-4161",memo:"北区居宅介護支援事業所",priority:228},
  {ward:"北区",category:"居宅介護支援事業所",name:"ピースケアプランセンター",address:"大阪市北区菅原町11-10 オーキッド中之島402号North",tel:"06-6361-0075",fax:"06-4709-6000",memo:"北区居宅介護支援事業所",priority:229},
  {ward:"北区",category:"居宅介護支援事業所",name:"ケアプランセンターMSC",address:"大阪市北区西天満3-13-20 ASビル6階",tel:"06-6232-8263",fax:"06-6232-8122",memo:"北区居宅介護支援事業所",priority:230},
  {ward:"北区",category:"居宅介護支援事業所",name:"ケアプランセンターあずき",address:"大阪市北区南森町1-3-29-1004",tel:"06-6926-4275",fax:"06-6926-4276",memo:"北区居宅介護支援事業所",priority:231},
  {ward:"北区",category:"居宅介護支援事業所",name:"株式会社ハート介護サービス居宅介護支援事業所",address:"大阪市北区南森町2-2-9 南森町八千代ビル1階",tel:"06-6362-3368",fax:"06-6362-3367",memo:"北区居宅介護支援事業所",priority:232},
  {ward:"北区",category:"居宅介護支援事業所",name:"ケアプランセンターひまわりの苑",address:"大阪市北区曽根崎1-1-20",tel:"06-7501-8688",fax:"06-7501-8691",memo:"北区居宅介護支援事業所",priority:233},
  {ward:"北区",category:"居宅介護支援事業所",name:"きん柑ケアプランセンター北",address:"大阪市北区天神橋7-3-2-604 大山ビル",tel:"06-4792-8859",fax:"06-4792-8860",memo:"北区居宅介護支援事業所",priority:234},
  {ward:"北区",category:"居宅介護支援事業所",name:"えすぽわーるこころ",address:"大阪市北区天神橋7-10-2 喜住ビル1F",tel:"06-6766-4147",fax:"06-6766-4148",memo:"北区居宅介護支援事業所",priority:235},
  {ward:"北区",category:"居宅介護支援事業所",name:"ケアプランセンター寿梨の里",address:"大阪市北区天神橋7-15-2-101",tel:"06-6360-9323",fax:"06-6360-9322",memo:"北区居宅介護支援事業所",priority:236},
  {ward:"北区",category:"居宅介護支援事業所",name:"まごころケア北",address:"大阪市北区長柄西1-1-16",tel:"06-6352-0830",fax:"06-6352-0831",memo:"北区居宅介護支援事業所",priority:237},
  {ward:"北区",category:"居宅介護支援事業所",name:"ハートフルかのうケアプランセンター",address:"大阪市北区長柄中1-1-21",tel:"06-6354-1108",fax:"06-6354-1121",memo:"北区居宅介護支援事業所",priority:238},
  {ward:"北区",category:"居宅介護支援事業所",name:"エルケア長柄ケアプランセンター",address:"大阪市北区長柄東2-8-36 淀川リバーサイド・ビーネ2階",tel:"06-7688-5078",fax:"06-7688-5079",memo:"北区居宅介護支援事業所",priority:239},
  {ward:"北区",category:"居宅介護支援事業所",name:"ケア21北",address:"大阪市北区国分寺2-1-14 ACOM天六ビル5階",tel:"06-7167-2421",fax:"06-6355-0121",memo:"北区居宅介護支援事業所",priority:240},
  {ward:"北区",category:"居宅介護支援事業所",name:"株式会社ソニックコーポレーショントータルケアサービス",address:"大阪市北区中津7-3-7-301",tel:"06-6457-0207",fax:"06-6457-0208",memo:"北区居宅介護支援事業所",priority:241},
  {ward:"北区",category:"居宅介護支援事業所",name:"居宅介護支援事業所藤ミレニアム",address:"大阪市北区本庄西2-6-15",tel:"06-6371-6322",fax:"06-6371-6364",memo:"北区居宅介護支援事業所",priority:242},
  {ward:"北区",category:"居宅介護支援事業所",name:"ケアプランセンターアセス",address:"大阪市北区本庄西1-9-12 朝日プラザ北梅田1F東側",tel:"06-6486-9073",fax:"06-6292-6658",memo:"北区居宅介護支援事業所",priority:243},
  {ward:"北区",category:"居宅介護支援事業所",name:"なでしこケアプランセンター",address:"大阪市北区本庄西2-15-12",tel:"06-6373-1724",fax:"06-7502-2296",memo:"北区居宅介護支援事業所",priority:244},
  {ward:"北区",category:"居宅介護支援事業所",name:"ユアーズ介護ケアプランオフィス",address:"大阪市北区本庄東2-2-25 クリエイト天八ビル7階",tel:"06-6373-7224",fax:"06-6373-7223",memo:"北区居宅介護支援事業所",priority:245},
  {ward:"北区",category:"居宅介護支援事業所",name:"もりたケアプランセンター",address:"大阪市北区本庄東2-1-23-202 スペチアーレ",tel:"06-6131-9740",fax:"06-6131-9755",memo:"北区居宅介護支援事業所",priority:246},
  {ward:"北区",category:"居宅介護支援事業所",name:"もこもこセンター",address:"大阪市北区本庄東2-12-15",tel:"06-7651-6935",fax:"06-7652-7774",memo:"北区居宅介護支援事業所",priority:247},
  {ward:"北区",category:"居宅介護支援事業所",name:"介護ステーションワンピース",address:"大阪市北区本庄東3-10-22",tel:"06-6373-4033",fax:"06-6373-4033",memo:"北区居宅介護支援事業所",priority:248},
  {ward:"北区",category:"居宅介護支援事業所",name:"愛と心の居宅介護支援センター大阪",address:"大阪市北区本庄東1-14-4",tel:"06-6305-8008",fax:"06-7739-5321",memo:"北区居宅介護支援事業所",priority:249},
  {ward:"北区",category:"居宅介護支援事業所",name:"居宅介護支援事業所淳風おおさか",address:"大阪市北区大淀南2-5-20",tel:"06-6450-1140",fax:"06-6450-1130",memo:"北区居宅介護支援事業所",priority:250},
  {ward:"北区",category:"居宅介護支援事業所",name:"ケアプランセンターあいわ",address:"大阪市北区大淀中4-6-16",tel:"06-6345-7832",fax:"06-6345-7833",memo:"北区居宅介護支援事業所",priority:251},
  {ward:"北区",category:"居宅介護支援事業所",name:"支援事業所大阪北",address:"大阪市北区大淀中5-5-8",tel:"06-7174-4425",fax:"06-7174-4425",memo:"北区居宅介護支援事業所",priority:252}
];

let addedData = JSON.parse(localStorage.getItem("moa_added_data") || "[]");

function getAllData(){
  return [...baseHoukatsu, ...baseKyotaku, ...addedData];
}

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

function renderList(){
  const keyword = document.getElementById("keyword").value.trim().toLowerCase();
  const ward = document.getElementById("ward").value;
  const category = document.getElementById("category").value;

  const allData = getAllData();

  let data = allData.filter(item => {
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

    return (!keyword || text.includes(keyword)) &&
           (!ward || item.ward === ward) &&
           (!category || item.category === category);
  });

  data.sort((a,b) => (a.priority || 9999) - (b.priority || 9999));

  document.getElementById("summary").textContent =
    "表示件数：" + data.length + "件 ／ 登録総数：" + allData.length + "件";

  const list = document.getElementById("list");

  if(data.length === 0){
    list.innerHTML = `<div class="empty">該当する営業先がありません。<br>検索文字を短くして試してください。</div>`;
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
          <span class="tag">${escapeHtml(item.ward)}</span>
          <span class="tag">${escapeHtml(item.category)}</span>
        </div>

        <div class="name">${escapeHtml(item.name)}</div>

        <div class="info">📍 <strong>住所：</strong>${escapeHtml(item.address)}</div>
        <div class="info">☎️ <strong>電話：</strong>${item.tel ? escapeHtml(item.tel) : "未入力"}</div>
        <div class="info">📠 <strong>FAX：</strong>${item.fax ? escapeHtml(item.fax) : "未入力"}</div>
        <div class="info">🗺️ <strong>対象：</strong>${escapeHtml(item.area || item.ward || "")}</div>

        <div class="memo">
          <strong>営業メモ：</strong><br>
          ${escapeHtml(item.memo || "")}
        </div>

        <div class="actions">
          <a class="tel" href="${telUrl(item.tel)}">電話</a>
          <a class="map" href="${mapUrl(item.address)}" target="_blank">地図</a>
          <a class="route" href="${routeUrl(item.address)}" target="_blank">ルート</a>
          <button class="copy" onclick="copyInfo('${escapeJs(item.name)}')">コピー</button>
        </div>
      </div>
    `;
  }).join("");
}

function resetSearch(){
  document.getElementById("keyword").value = "";
  document.getElementById("ward").value = "";
  document.getElementById("category").value = "";
  renderList();
}

function openAllRoute(){
  const keyword = document.getElementById("keyword").value.trim().toLowerCase();
  const ward = document.getElementById("ward").value;
  const category = document.getElementById("category").value;

  let data = getAllData().filter(item => {
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

    return (!keyword || text.includes(keyword)) &&
           (!ward || item.ward === ward) &&
           (!category || item.category === category);
  });

  data.sort((a,b) => (a.priority || 9999) - (b.priority || 9999));

  if(data.length === 0){
    alert("表示中の営業先がありません。");
    return;
  }

  if(data.length > 10){
    alert("Googleマップのルートは多すぎると開けない場合があります。区や種別で10件以内に絞るのがおすすめです。");
  }

  const destination = data[data.length - 1].address;
  const waypoints = data.slice(0, -1).map(x => x.address).join("|");

  let url = "https://www.google.com/maps/dir/?api=1";
  url += "&destination=" + encodeURIComponent(destination);
  if(waypoints) url += "&waypoints=" + encodeURIComponent(waypoints);

  window.open(url, "_blank");
}

function copyInfo(name){
  const item = getAllData().find(x => x.name === name);
  if(!item) return;

  const text =
`【${item.ward}】${item.category}
${item.name}

住所：${item.address}
電話：${item.tel || "未入力"}
FAX：${item.fax || "未入力"}
メモ：${item.memo || ""}
地図：${mapUrl(item.address)}`;

  navigator.clipboard.writeText(text).then(() => {
    alert("コピーしました。");
  }).catch(() => {
    alert("コピーできませんでした。");
  });
}

function importCsv(){
  const csv = document.getElementById("csvInput").value.trim();
  if(!csv){
    alert("CSVを貼り付けてください。");
    return;
  }

  const lines = csv.split(/\r?\n/).filter(line => line.trim());
  const newItems = [];

  lines.forEach((line,idx) => {
    const cols = line.split(",").map(x => x.trim());

    if(cols.length < 4) return;

    const item = {
      ward: cols[0] || "",
      category: cols[1] || "居宅介護支援事業所",
      name: cols[2] || "",
      address: cols[3] || "",
      tel: cols[4] || "",
      fax: cols[5] || "",
      memo: cols[6] || "CSV追加データ",
      priority: 1000 + addedData.length + idx
    };

    if(item.name && item.address){
      newItems.push(item);
    }
  });

  if(newItems.length === 0){
    alert("追加できるデータがありません。形式を確認してください。");
    return;
  }

  addedData = [...addedData, ...newItems];
  localStorage.setItem("moa_added_data", JSON.stringify(addedData));

  document.getElementById("csvInput").value = "";
  alert(newItems.length + "件追加しました。");
  renderList();
}

function clearAddedData(){
  if(!confirm("CSVで追加したデータだけを消します。よろしいですか？")) return;
  addedData = [];
  localStorage.removeItem("moa_added_data");
  renderList();
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

function escapeJs(str){
  return String(str).replaceAll("\\","\\\\").replaceAll("'","\\'");
}

renderList();
</script>

</body>
</html>

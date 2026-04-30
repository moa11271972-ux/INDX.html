import React, { useEffect, useMemo, useState } from 'react';
import {
  Search, Phone, MapPin, Upload, Download, Route, CheckCircle2, X, LocateFixed,
  Navigation, Camera, Image as ImageIcon, Building2, Users, ClipboardList, Star,
  Trash2, Plus, ExternalLink, FileText
} from 'lucide-react';

const NL = String.fromCharCode(10);

const STORAGE = {
  records: 'osaka-care-sales.records.full.v1',
  route: 'osaka-care-sales.route.full.v1',
  visits: 'osaka-care-sales.visits.full.v1',
};

const OFFICIAL_CSVS = [
  {
    label: '大阪市 居宅介護支援事業所CSV',
    url: 'https://www.city.osaka.lg.jp/fukushi/cmsfiles/contents/0000491/491832/kyotakukaigosien.csv',
    type: '居宅介護支援事業所',
  },
  {
    label: '大阪市 地域包括支援センター・ブランチCSV',
    url: 'https://www.city.osaka.lg.jp/fukushi/cmsfiles/contents/0000370/370519/r7-3itiran.csv',
    type: '地域包括支援センター',
  },
];

const WARDS = [
  'すべて', '北区', '都島区', '福島区', '此花区', '中央区', '西区', '港区', '大正区', '天王寺区',
  '浪速区', '西淀川区', '淀川区', '東淀川区', '東成区', '生野区', '旭区', '城東区', '鶴見区',
  '阿倍野区', '住之江区', '住吉区', '東住吉区', '平野区', '西成区', '区未設定'
];
const STATUSES = ['未アプローチ', '初回架電済', '資料送付', '訪問予定', '訪問済', '商談化', '見込み薄', '契約済'];
const TYPES = ['すべて', '地域包括支援センター', '居宅介護支援事業所'];
const PRIORITIES = ['A', 'B', 'C'];

const INITIAL_RECORDS = [
  rec('hokatsu-kita', '地域包括支援センター', '北区', '北区地域包括支援センター', '530-0026', '大阪市北区神山町15-11', '06-6313-5568', '06-6313-6377', 34.7039, 135.5074),
  rec('hokatsu-kita-oyodo', '地域包括支援センター', '北区', '北区大淀地域包括支援センター', '531-0062', '大阪市北区長柄中1-1-21', '06-6354-1165', '06-6354-1175', 34.7109, 135.5120),
  rec('hokatsu-miyakojima', '地域包括支援センター', '都島区', '都島区地域包括支援センター', '534-0021', '大阪市都島区都島本通3-12-31', '06-6929-9500', '06-6929-9504', 34.7077, 135.5287),
  rec('hokatsu-fukushima', '地域包括支援センター', '福島区', '福島区地域包括支援センター', '553-0001', '大阪市福島区海老江6-2-22', '06-6454-6330', '06-6454-6331', 34.6960, 135.4728),
  rec('hokatsu-chuo', '地域包括支援センター', '中央区', '中央区地域包括支援センター', '542-0062', '大阪市中央区上本町西2-5-25', '06-6763-8139', '06-6763-8151', 34.6778, 135.5206),
  rec('hokatsu-nishi', '地域包括支援センター', '西区', '西区地域包括支援センター', '550-0013', '大阪市西区新町4-5-14 西区役所合同庁舎6階', '06-6539-8075', '06-6539-8073', 34.6746, 135.4868),
  rec('hokatsu-yodogawa', '地域包括支援センター', '淀川区', '淀川区地域包括支援センター', '532-0005', '大阪市淀川区三国本町2-14-3', '06-6394-2914', '06-6394-2977', 34.7352, 135.4868),
  rec('hokatsu-abeno', '地域包括支援センター', '阿倍野区', '阿倍野区地域包括支援センター', '545-0037', '大阪市阿倍野区帝塚山1-3-8', '06-6628-1400', '06-6628-9393', 34.6337, 135.5136),
  rec('hokatsu-suminoe', '地域包括支援センター', '住之江区', '住之江区地域包括支援センター', '559-0013', '大阪市住之江区御崎4-6-10', '06-6686-2235', '06-6686-2122', 34.6135, 135.4820),
  rec('hokatsu-nishinari', '地域包括支援センター', '西成区', '西成区地域包括支援センター', '557-0041', '大阪市西成区岸里1-5-20 西成区合同庁舎8階', '06-6656-0080', '06-6656-0083', 34.6379, 135.4945),
  rec('kyotaku-saiseikai-nakatsu', '居宅介護支援事業所', '北区', '済生会中津病院', '530-0012', '大阪市北区芝田2-10-39', '06-6372-0733', '06-6372-0752', 34.7073, 135.4947),
  rec('kyotaku-minato-coop', '居宅介護支援事業所', '港区', '居宅介護支援事業所コープみなと介護よろず相談所', '552-0003', '大阪市港区磯路三丁目3番4号', '06-6571-7880', '06-6571-5659', 34.6655, 135.4576),
  rec('kyotaku-nishinari-imamiya', '居宅介護支援事業所', '西成区', '今宮ケアプランセンター', '557-0014', '大阪市西成区天下茶屋一丁目31番9号', '06-6656-6300', '06-6656-6322', 34.6365, 135.5003),
  rec('kyotaku-nishinari-banana', '居宅介護支援事業所', '西成区', '居宅介護支援事業所ばなな', '557-0014', '大阪市西成区天下茶屋二丁目18番13号', '06-6655-6018', '06-6655-6028', 34.6379, 135.5018),
  rec('kyotaku-nishinari-ribu', '居宅介護支援事業所', '西成区', 'りぶケアプランセンター', '557-0014', '大阪市西成区天下茶屋三丁目24番15-404号 メゾンドゥアルシオン', '06-6654-9266', '06-6654-9276', 34.6373, 135.5002),
  rec('kyotaku-nishinari-paul', '居宅介護支援事業所', '西成区', 'ポールケアプランセンター', '557-0014', '大阪市西成区天下茶屋二丁目23番6号', '06-6690-0391', '06-6690-0392', 34.6378, 135.5008),
  rec('kyotaku-nishinari-tsubasa', '居宅介護支援事業所', '西成区', 'バリアフリーサービスつばさケア・ステーション', '557-0016', '大阪市西成区花園北二丁目5番7号', '06-6636-5502', '06-6636-5503', 34.6453, 135.4985),
  rec('kyotaku-nishinari-human', '居宅介護支援事業所', '西成区', 'ヒューマンケアプランセンター', '557-0023', '大阪市西成区南開一丁目6番10号 アイビスコート1階', '06-6563-6578', '06-6563-6646', 34.6480, 135.4887),
  rec('kyotaku-nishinari-cyclo', '居宅介護支援事業所', '西成区', 'シクロケアプランセンター', '557-0031', '大阪市西成区鶴見橋一丁目6番32号', '06-6629-8737', '06-6629-8738', 34.6467, 135.4921),
];

function rec(id, type, ward, name, zip, address, phone, fax, lat, lng) {
  return { id, type, ward, name, zip, address, phone, fax, lat, lng, status: '未アプローチ', priority: 'A', memo: '初期登録データ。公式CSVを取り込むと全件化できます。', photoUrl: '' };
}

function save(key, value) { try { window.localStorage.setItem(key, JSON.stringify(value)); } catch {} }
function load(key, fallback) { try { const raw = window.localStorage.getItem(key); return raw ? JSON.parse(raw) : fallback; } catch { return fallback; } }
function makeId() { return `id-${Date.now()}-${Math.random().toString(36).slice(2)}`; }
function normalize(value) { return String(value || '').replace(/^﻿/, '').trim(); }

function parseCsv(text) {
  const rows = [];
  let row = [];
  let cell = '';
  let quoted = false;
  for (let i = 0; i < text.length; i += 1) {
    const char = text[i];
    const next = text[i + 1];
    const code = char.charCodeAt(0);
    if (char === '"' && quoted && next === '"') { cell += '"'; i += 1; }
    else if (char === '"') quoted = !quoted;
    else if (char === ',' && !quoted) { row.push(normalize(cell)); cell = ''; }
    else if ((code === 10 || code === 13) && !quoted) {
      if (cell || row.length) { row.push(normalize(cell)); rows.push(row); }
      row = []; cell = '';
      if (code === 13 && next && next.charCodeAt(0) === 10) i += 1;
    } else cell += char;
  }
  if (cell || row.length) { row.push(normalize(cell)); rows.push(row); }
  return rows.filter(r => r.some(Boolean));
}

function pick(row, names) {
  const key = Object.keys(row).find(k => names.some(n => k.toLowerCase().includes(n.toLowerCase())));
  return key ? row[key] : '';
}
function inferWard(address) { return WARDS.find(w => w !== 'すべて' && w !== '区未設定' && String(address).includes(w)) || '区未設定'; }

function csvToRecords(text, fallbackType) {
  const rows = parseCsv(text);
  if (!rows.length) return [];
  let headerIndex = rows.findIndex(r => r.some(c => ['事業所番号', '事業所名称', '名称', '所在地', '電話番号'].includes(c)));
  if (headerIndex < 0) headerIndex = 0;
  const headers = rows[headerIndex].map(normalize);
  return rows.slice(headerIndex + 1).map(values => {
    const row = Object.fromEntries(headers.map((h, i) => [h, normalize(values[i])]));
    const address = pick(row, ['所在地', '住所', '事業所所在地', 'address']);
    const typeRaw = pick(row, ['サービス', '種別', '類型', 'type']);
    const name = pick(row, ['事業所名称', '名称', '事業所名', 'name']);
    return {
      id: makeId(),
      type: typeRaw.includes('地域包括') ? '地域包括支援センター' : fallbackType,
      ward: pick(row, ['区', 'ward']) || inferWard(address),
      name: name || '名称未設定',
      zip: pick(row, ['郵便', 'zip']),
      address,
      phone: pick(row, ['電話', 'tel', 'phone']),
      fax: pick(row, ['fax', 'ファックス']),
      lat: Number(pick(row, ['lat', '緯度'])) || null,
      lng: Number(pick(row, ['lng', 'lon', '経度'])) || null,
      status: '未アプローチ', priority: 'B', memo: '', photoUrl: pick(row, ['写真', '画像', 'photo', 'image'])
    };
  }).filter(r => r.name !== '名称未設定' || r.address || r.phone);
}

function toCsv(rows, headers) {
  const escape = value => `"${String(value ?? '').replaceAll('"', '""')}"`;
  return `﻿${headers.join(',')}${NL}${rows.map(row => headers.map(h => escape(row[h])).join(',')).join(NL)}`;
}
function download(filename, text, type = 'text/csv;charset=utf-8;') {
  const blob = new Blob([text], { type });
  const url = URL.createObjectURL(blob);
  const link = document.createElement('a');
  link.href = url; link.download = filename; link.click(); URL.revokeObjectURL(url);
}
function distanceKm(from, to) {
  if (!from || !to?.lat || !to?.lng) return null;
  const r = 6371, toRad = deg => deg * Math.PI / 180;
  const dLat = toRad(to.lat - from.lat), dLng = toRad(to.lng - from.lng);
  const a = Math.sin(dLat / 2) ** 2 + Math.cos(toRad(from.lat)) * Math.cos(toRad(to.lat)) * Math.sin(dLng / 2) ** 2;
  return r * 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1 - a));
}
function distanceText(km) { if (km == null) return ''; return km < 1 ? `約${Math.round(km * 1000)}m` : `約${km.toFixed(1)}km`; }
function googleSearchUrl(record) { return `https://www.google.com/maps/search/?api=1&query=${encodeURIComponent(record.address || record.name)}`; }
function googleRouteUrl(records, currentLocation) {
  const stops = records.filter(r => r.address).map(r => encodeURIComponent(r.address));
  if (!stops.length) return '';
  const start = currentLocation ? encodeURIComponent(`${currentLocation.lat},${currentLocation.lng}`) : encodeURIComponent('現在地');
  return `https://www.google.com/maps/dir/${start}/${stops.join('/')}`;
}

export default function App() {
  const [records, setRecords] = useState(() => load(STORAGE.records, INITIAL_RECORDS));
  const [routeIds, setRouteIds] = useState(() => load(STORAGE.route, []));
  const [visitLogs, setVisitLogs] = useState(() => load(STORAGE.visits, []));
  const [query, setQuery] = useState('');
  const [ward, setWard] = useState('すべて');
  const [type, setType] = useState('すべて');
  const [status, setStatus] = useState('すべて');
  const [selectedId, setSelectedId] = useState(records[0]?.id || '');
  const [csvType, setCsvType] = useState('居宅介護支援事業所');
  const [visitDate, setVisitDate] = useState(() => new Date().toISOString().slice(0, 10));
  const [visitNote, setVisitNote] = useState('');
  const [currentLocation, setCurrentLocation] = useState(null);
  const [locationMessage, setLocationMessage] = useState('');
  const [sortByNear, setSortByNear] = useState(false);
  const [nearCount, setNearCount] = useState(5);

  useEffect(() => save(STORAGE.records, records), [records]);
  useEffect(() => save(STORAGE.route, routeIds), [routeIds]);
  useEffect(() => save(STORAGE.visits, visitLogs), [visitLogs]);

  const enrichedRecords = useMemo(() => records.map(record => ({ ...record, distanceKm: distanceKm(currentLocation, record) })), [records, currentLocation]);
  const filteredRecords = useMemo(() => {
    const list = enrichedRecords.filter(record => {
      const haystack = [record.type, record.ward, record.name, record.address, record.phone, record.memo].join(' ').toLowerCase();
      return haystack.includes(query.toLowerCase()) && (ward === 'すべて' || record.ward === ward) && (type === 'すべて' || record.type === type) && (status === 'すべて' || record.status === status);
    });
    if (sortByNear && currentLocation) return [...list].sort((a, b) => (a.distanceKm ?? 99999) - (b.distanceKm ?? 99999));
    return list;
  }, [enrichedRecords, query, ward, type, status, sortByNear, currentLocation]);
  const groupedRecords = useMemo(() => {
    const groups = new Map();
    filteredRecords.forEach(record => { const key = record.ward || '区未設定'; if (!groups.has(key)) groups.set(key, []); groups.get(key).push(record); });
    return [...groups.entries()].sort(([a], [b]) => WARDS.indexOf(a) - WARDS.indexOf(b));
  }, [filteredRecords]);
  const selected = enrichedRecords.find(r => r.id === selectedId) || enrichedRecords[0];
  const routeRecords = routeIds.map(id => enrichedRecords.find(r => r.id === id)).filter(Boolean);
  const stats = useMemo(() => ({
    total: records.length,
    hokatsu: records.filter(r => r.type === '地域包括支援センター').length,
    kyotaku: records.filter(r => r.type === '居宅介護支援事業所').length,
    hot: records.filter(r => ['訪問予定', '商談化', '契約済'].includes(r.status)).length,
    visited: records.filter(r => r.status === '訪問済').length,
  }), [records]);

  function updateRecord(id, patch) { setRecords(prev => prev.map(record => record.id === id ? { ...record, ...patch } : record)); }
  function addOrRemoveRoute(id) { setRouteIds(prev => prev.includes(id) ? prev.filter(x => x !== id) : [...prev, id]); }
  function appendMemo(current, line) { return current ? `${current}${NL}${line}` : line; }
  function markVisitPlanned(record) { updateRecord(record.id, { status: '訪問予定', memo: appendMemo(record.memo, `${visitDate} 訪問予定`) }); setRouteIds(prev => prev.includes(record.id) ? prev : [...prev, record.id]); }
  function markVisited(record) {
    const note = visitNote.trim() || '訪問済み';
    setVisitLogs(prev => [{ id: makeId(), date: visitDate, ward: record.ward, type: record.type, name: record.name, address: record.address, phone: record.phone, note }, ...prev]);
    updateRecord(record.id, { status: '訪問済', memo: appendMemo(record.memo, `${visitDate} 訪問済：${note}`) });
    setRouteIds(prev => prev.filter(id => id !== record.id)); setVisitNote('');
  }
  function locateMe() {
    setLocationMessage('現在地を取得中です...');
    if (!navigator.geolocation) { setLocationMessage('この端末では現在地を取得できません。'); return; }
    navigator.geolocation.getCurrentPosition(
      position => { setCurrentLocation({ lat: position.coords.latitude, lng: position.coords.longitude }); setSortByNear(true); setLocationMessage('現在地を取得しました。'); },
      () => setLocationMessage('現在地を取得できませんでした。ブラウザの位置情報を許可してください。'),
      { enableHighAccuracy: true, timeout: 10000, maximumAge: 60000 }
    );
  }
  function addNearbyToRoute() {
    if (!currentLocation) { locateMe(); return; }
    const ids = filteredRecords.filter(r => r.status !== '訪問済' && r.distanceKm != null).sort((a, b) => a.distanceKm - b.distanceKm).slice(0, Number(nearCount)).map(r => r.id);
    setRouteIds(prev => [...new Set([...prev, ...ids])]); setSortByNear(true);
  }
  function openRoute(recordsToOpen = routeRecords) { const url = googleRouteUrl(recordsToOpen, currentLocation); if (url) window.open(url, '_blank'); }
  function handlePhotoUpload(record, event) {
    const file = event.target.files?.[0]; if (!file) return;
    const reader = new FileReader(); reader.onload = () => updateRecord(record.id, { photoUrl: reader.result }); reader.readAsDataURL(file); event.target.value = '';
  }
  async function handleCsvImport(event) {
    const file = event.target.files?.[0]; if (!file) return;
    const buffer = await file.arrayBuffer(); let text = new TextDecoder('utf-8').decode(buffer);
    if (text.includes('�')) text = new TextDecoder('shift-jis').decode(buffer);
    const imported = csvToRecords(text, csvType); setRecords(prev => [...prev, ...imported]); if (imported[0]) setSelectedId(imported[0].id); event.target.value = '';
  }
  function exportRecords() { download('osaka-care-sales-list.csv', toCsv(records, ['type', 'ward', 'name', 'zip', 'address', 'phone', 'fax', 'lat', 'lng', 'status', 'priority', 'memo', 'photoUrl'])); }
  function exportVisits() { download('osaka-care-visit-logs.csv', toCsv(visitLogs, ['date', 'ward', 'type', 'name', 'address', 'phone', 'note'])); }
  function resetApp() { if (!window.confirm('保存済みデータを初期状態に戻します。よろしいですか？')) return; setRecords(INITIAL_RECORDS); setRouteIds([]); setVisitLogs([]); setSelectedId(INITIAL_RECORDS[0].id); }

  return (
    <div className="min-h-screen bg-slate-100 text-slate-900">
      <div className="mx-auto max-w-7xl p-4 md:p-6 space-y-5">
        <header className="rounded-3xl bg-slate-950 text-white p-5 md:p-7 shadow-sm">
          <div className="flex flex-col gap-5 lg:flex-row lg:items-end lg:justify-between">
            <div><p className="text-sm text-slate-300">大阪市 介護・高齢者支援向け</p><h1 className="mt-1 text-2xl md:text-4xl font-bold tracking-tight">介護営業ルートアプリ</h1><p className="mt-3 text-sm md:text-base text-slate-300 max-w-3xl">事業所CSV取込、現在地から近い順、電話、ルート、訪問記録、写真登録まで全部入りです。</p></div>
            <div className="flex flex-wrap gap-2"><select className="rounded-xl bg-white text-slate-900 px-3 py-2 text-sm" value={csvType} onChange={e => setCsvType(e.target.value)}><option>居宅介護支援事業所</option><option>地域包括支援センター</option></select><label className="inline-flex items-center gap-2 rounded-xl bg-white text-slate-900 px-4 py-2 text-sm font-semibold cursor-pointer hover:bg-slate-100"><Upload size={16} />CSV取込<input className="hidden" type="file" accept=".csv,text/csv" onChange={handleCsvImport} /></label><Button onClick={exportRecords} className="rounded-xl gap-2 bg-white text-slate-900 hover:bg-slate-100"><Download size={16} />営業リストCSV</Button><Button onClick={resetApp} className="rounded-xl gap-2 bg-slate-800 hover:bg-slate-700"><Trash2 size={16} />初期化</Button></div>
          </div>
        </header>

        <section className="grid grid-cols-2 md:grid-cols-5 gap-3"><Stat icon={<Users />} label="全件" value={stats.total} /><Stat icon={<Building2 />} label="地域包括" value={stats.hokatsu} /><Stat icon={<ClipboardList />} label="居宅介護支援" value={stats.kyotaku} /><Stat icon={<Star />} label="有望" value={stats.hot} /><Stat icon={<CheckCircle2 />} label="訪問済" value={stats.visited} /></section>

        <section className="rounded-3xl border bg-white p-4 shadow-sm space-y-4">
          <div className="grid grid-cols-1 md:grid-cols-5 gap-3"><div className="md:col-span-2 relative"><Search className="absolute left-3 top-3 text-slate-400" size={18} /><input className="w-full rounded-xl border px-3 py-2 pl-10" placeholder="名称・住所・電話・メモで検索" value={query} onChange={e => setQuery(e.target.value)} /></div><Select value={ward} onChange={setWard} options={WARDS} /><Select value={type} onChange={setType} options={TYPES} /><Select value={status} onChange={setStatus} options={['すべて', ...STATUSES]} /></div>
          <div className="rounded-2xl bg-amber-50 border border-amber-100 p-4"><div className="font-bold flex gap-2 items-center"><FileText size={18} />公式CSVを全件取り込み</div><p className="text-sm text-slate-600 mt-1">大阪市公式CSVをダウンロードして、このアプリのCSV取込から読み込むと全件リストになります。</p><div className="flex flex-wrap gap-2 mt-3">{OFFICIAL_CSVS.map(item => <a key={item.url} href={item.url} target="_blank" rel="noreferrer" className="inline-flex items-center gap-2 rounded-xl border bg-white px-3 py-2 text-sm font-semibold hover:bg-slate-50"><ExternalLink size={15} />{item.label}</a>)}</div></div>
          <div className="rounded-2xl bg-blue-50 border border-blue-100 p-4"><div className="flex flex-col gap-3 lg:flex-row lg:items-center lg:justify-between"><div><div className="flex items-center gap-2 font-bold"><LocateFixed size={18} />現在地から近い事業所</div><p className="text-sm text-slate-600 mt-1">営業中の場所から近い順に並べ替え、近い事業所をまとめてルート追加できます。</p>{locationMessage && <p className="text-xs text-blue-700 mt-1">{locationMessage}</p>}{currentLocation && <p className="text-xs text-slate-500 mt-1">緯度 {currentLocation.lat.toFixed(5)} / 経度 {currentLocation.lng.toFixed(5)}</p>}</div><div className="flex flex-wrap gap-2"><Button className="rounded-xl gap-2" onClick={locateMe}><LocateFixed size={16} />現在地取得</Button><Button variant={sortByNear ? 'default' : 'outline'} className="rounded-xl gap-2" disabled={!currentLocation} onClick={() => setSortByNear(v => !v)}><Navigation size={16} />近い順</Button><select className="rounded-xl border bg-white px-3 py-2 text-sm" value={nearCount} onChange={e => setNearCount(e.target.value)}><option value="3">近くの3件</option><option value="5">近くの5件</option><option value="8">近くの8件</option><option value="10">近くの10件</option></select><Button variant="outline" className="rounded-xl gap-2" onClick={addNearbyToRoute}><Route size={16} />近い事業所をルート追加</Button></div></div></div>
        </section>

        <section className="rounded-3xl border bg-white p-4 shadow-sm space-y-3"><div className="flex flex-col gap-3 lg:flex-row lg:items-center lg:justify-between"><div><div className="flex items-center gap-2 font-bold"><Route size={18} />本日の訪問ルート</div><p className="text-sm text-slate-600 mt-1">追加した順にGoogleマップでルート表示します。現在地取得後は現在地スタートになります。</p></div><div className="flex flex-wrap gap-2"><input className="rounded-xl border px-3 py-2 text-sm" type="date" value={visitDate} onChange={e => setVisitDate(e.target.value)} /><input className="rounded-xl border px-3 py-2 text-sm min-w-56" placeholder="訪問メモ" value={visitNote} onChange={e => setVisitNote(e.target.value)} /><Button disabled={!routeRecords.length} className="rounded-xl gap-2" onClick={() => openRoute(routeRecords)}><MapPin size={16} />ルート地図</Button><Button disabled={!routeRecords.length} variant="outline" className="rounded-xl gap-2" onClick={() => setRouteIds([])}><X size={16} />クリア</Button></div></div>{routeRecords.length ? <div className="flex gap-3 overflow-x-auto pb-1">{routeRecords.map((record, index) => <div key={record.id} className="min-w-72 rounded-2xl border bg-slate-50 p-3"><div className="text-xs font-bold text-slate-500">{index + 1}件目・{record.ward}{record.distanceKm != null ? `・${distanceText(record.distanceKm)}` : ''}</div><div className="mt-1 font-bold truncate">{record.name}</div><div className="text-xs text-slate-600 truncate">{record.address}</div><div className="mt-3 flex gap-2"><IconButton onClick={() => record.phone && (window.location.href = `tel:${record.phone}`)}><Phone size={15} /></IconButton><IconButton onClick={() => openRoute([record])}><MapPin size={15} /></IconButton><IconButton onClick={() => markVisited(record)}><CheckCircle2 size={15} /></IconButton><IconButton onClick={() => addOrRemoveRoute(record.id)}><X size={15} /></IconButton></div></div>)}</div> : <div className="rounded-2xl border bg-slate-50 p-4 text-sm text-slate-500">営業先の「ルート追加」を押すと、ここに訪問順で表示されます。</div>}</section>

        <main className="grid grid-cols-1 lg:grid-cols-3 gap-5"><section className="lg:col-span-2 space-y-5">{groupedRecords.map(([wardName, items]) => <div key={wardName} className="space-y-3"><div className="flex items-center justify-between rounded-2xl bg-slate-950 text-white px-4 py-3"><h2 className="font-bold">{wardName}</h2><span className="text-sm rounded-full bg-white/15 px-3 py-1">{items.length}件</span></div>{items.map(record => <RecordCard key={record.id} record={record} selected={selected?.id === record.id} inRoute={routeIds.includes(record.id)} onSelect={() => setSelectedId(record.id)} onCall={() => record.phone && (window.location.href = `tel:${record.phone}`)} onPlan={() => markVisitPlanned(record)} onRoute={() => addOrRemoveRoute(record.id)} onVisited={() => markVisited(record)} onMap={() => openRoute([record])} />)}</div>)}{!filteredRecords.length && <div className="rounded-3xl border bg-white p-8 text-center text-slate-500">条件に一致する事業所がありません。</div>}</section><aside className="lg:sticky lg:top-5 h-fit"><DetailPanel record={selected} inRoute={selected ? routeIds.includes(selected.id) : false} onUpdate={updateRecord} onUploadPhoto={handlePhotoUpload} onCall={() => selected?.phone && (window.location.href = `tel:${selected.phone}`)} onMap={() => selected && openRoute([selected])} onPlan={() => selected && markVisitPlanned(selected)} onRoute={() => selected && addOrRemoveRoute(selected.id)} onVisited={() => selected && markVisited(selected)} /></aside></main>

        <section className="rounded-3xl border bg-white p-4 shadow-sm space-y-3"><div className="flex flex-col gap-3 md:flex-row md:items-center md:justify-between"><div><h2 className="font-bold text-lg">訪問記録</h2><p className="text-sm text-slate-600">訪問済にした事業所が日付・メモ付きで残ります。</p></div><div className="flex gap-2"><Button disabled={!visitLogs.length} variant="outline" className="rounded-xl" onClick={exportVisits}>訪問記録CSV</Button><Button disabled={!visitLogs.length} variant="outline" className="rounded-xl" onClick={() => setVisitLogs([])}>記録クリア</Button></div></div>{visitLogs.length ? <div className="overflow-x-auto"><table className="w-full text-sm"><thead><tr className="border-b text-left text-slate-500"><th className="py-2 pr-3">訪問日</th><th className="py-2 pr-3">区</th><th className="py-2 pr-3">種別</th><th className="py-2 pr-3">事業所</th><th className="py-2 pr-3">電話</th><th className="py-2 pr-3">メモ</th></tr></thead><tbody>{visitLogs.map(log => <tr key={log.id} className="border-b last:border-0"><td className="py-2 pr-3 whitespace-nowrap">{log.date}</td><td className="py-2 pr-3 whitespace-nowrap">{log.ward}</td><td className="py-2 pr-3 whitespace-nowrap">{log.type}</td><td className="py-2 pr-3 font-semibold">{log.name}</td><td className="py-2 pr-3 whitespace-nowrap">{log.phone || '-'}</td><td className="py-2 pr-3">{log.note}</td></tr>)}</tbody></table></div> : <div className="rounded-2xl border bg-slate-50 p-4 text-sm text-slate-500">まだ訪問記録はありません。</div>}</section>
      </div>
    </div>
  );
}

function Button({ children, className = '', variant = 'default', disabled, ...props }) { const variants = { default: 'bg-slate-950 text-white hover:bg-slate-800', outline: 'bg-white border text-slate-900 hover:bg-slate-100' }; return <button disabled={disabled} className={`inline-flex items-center justify-center gap-1.5 px-4 py-2 text-sm font-semibold transition disabled:opacity-50 disabled:pointer-events-none ${variants[variant] || variants.default} ${className}`} {...props}>{children}</button>; }
function IconButton({ children, ...props }) { return <button className="inline-flex h-9 w-9 items-center justify-center rounded-xl border bg-white hover:bg-slate-100" {...props}>{children}</button>; }
function Select({ value, onChange, options }) { return <select className="w-full rounded-xl border bg-white px-3 py-2" value={value} onChange={e => onChange(e.target.value)}>{options.map(option => <option key={option} value={option}>{option}</option>)}</select>; }
function Stat({ icon, label, value }) { return <div className="rounded-3xl border bg-white p-4 shadow-sm flex items-center gap-3"><div className="rounded-2xl bg-slate-100 p-3 text-slate-700">{React.cloneElement(icon, { size: 20 })}</div><div><div className="text-sm text-slate-500">{label}</div><div className="text-2xl font-bold">{value}</div></div></div>; }
function Badge({ children }) { return <span className="inline-flex rounded-full bg-slate-100 px-2.5 py-1 text-xs font-semibold text-slate-700">{children}</span>; }
function Action({ children, onClick, dark, active }) { return <span onClick={e => { e.stopPropagation(); onClick?.(); }} className={`inline-flex cursor-pointer items-center gap-1 rounded-xl border px-3 py-1.5 text-xs font-bold ${dark || active ? 'bg-slate-950 text-white border-slate-950' : 'bg-white text-slate-900'}`}>{children}</span>; }
function PhotoSmall({ record }) { if (record.photoUrl) return <img src={record.photoUrl} alt={record.name} className="h-24 w-24 shrink-0 rounded-2xl border object-cover bg-slate-100" />; return <div className="h-24 w-24 shrink-0 rounded-2xl border bg-slate-100 text-slate-400 flex flex-col items-center justify-center"><ImageIcon size={24} /><span className="mt-1 text-[10px]">写真なし</span></div>; }
function PhotoLarge({ record }) { if (record.photoUrl) return <img src={record.photoUrl} alt={record.name} className="h-52 w-full rounded-3xl border object-cover bg-slate-100" />; return <div className="h-52 w-full rounded-3xl border bg-slate-100 text-slate-500 flex flex-col items-center justify-center"><ImageIcon size={36} /><div className="mt-2 font-bold">写真未登録</div><div className="mt-1 text-xs">訪問時の外観写真または写真URLを登録できます</div></div>; }
function RecordCard({ record, selected, inRoute, onSelect, onCall, onPlan, onRoute, onVisited, onMap }) { return <button onClick={onSelect} className={`w-full rounded-3xl border bg-white p-4 text-left transition hover:shadow-md ${selected ? 'ring-2 ring-slate-950' : ''}`}><div className="flex gap-3"><PhotoSmall record={record} /><div className="min-w-0 flex-1"><div className="flex flex-wrap gap-2"><Badge>{record.type}</Badge><Badge>優先度 {record.priority}</Badge><span className="inline-flex rounded-full bg-white border px-2.5 py-1 text-xs font-semibold">{record.status}</span>{record.distanceKm != null && <span className="inline-flex rounded-full bg-blue-50 text-blue-700 px-2.5 py-1 text-xs font-bold">{distanceText(record.distanceKm)}</span>}</div><h3 className="mt-2 text-lg font-bold leading-tight">{record.name}</h3><p className="mt-1 text-sm text-slate-600"><MapPin size={14} className="inline mr-1" />{record.address || '住所未登録'}</p><p className="mt-1 text-sm text-slate-600"><Phone size={14} className="inline mr-1" />{record.phone || '電話未登録'}</p><div className="mt-3 flex flex-wrap gap-2"><Action onClick={onCall} dark><Phone size={13} />電話</Action><Action onClick={onPlan}><CheckCircle2 size={13} />訪問予定</Action><Action onClick={onRoute} active={inRoute}><Plus size={13} />{inRoute ? '追加済' : 'ルート追加'}</Action><Action onClick={onVisited}><CheckCircle2 size={13} />訪問済</Action><Action onClick={onMap}><MapPin size={13} />地図</Action></div></div></div></button>; }
function Info({ label, value }) { return <div className="rounded-2xl bg-slate-50 p-3"><div className="text-xs text-slate-500">{label}</div><div className="mt-1 break-all font-bold">{value || '-'}</div></div>; }
function DetailPanel({ record, inRoute, onUpdate, onUploadPhoto, onCall, onMap, onPlan, onRoute, onVisited }) { if (!record) return <div className="rounded-3xl border bg-white p-5 text-slate-500">事業所を選択してください。</div>; return <div className="rounded-3xl border bg-white p-5 shadow-sm space-y-4"><PhotoLarge record={record} /><div className="flex flex-wrap gap-2"><label className="inline-flex cursor-pointer items-center gap-2 rounded-xl border bg-white px-3 py-2 text-sm font-semibold hover:bg-slate-100"><Camera size={16} />写真登録<input className="hidden" type="file" accept="image/*" capture="environment" onChange={e => onUploadPhoto(record, e)} /></label><Button variant="outline" className="rounded-xl" onClick={() => window.open(googleSearchUrl(record), '_blank')}><ImageIcon size={16} />Googleで見る</Button>{record.photoUrl && <Button variant="outline" className="rounded-xl" onClick={() => onUpdate(record.id, { photoUrl: '' })}>写真削除</Button>}</div><input className="w-full rounded-xl border px-3 py-2 text-sm" placeholder="写真URLを貼り付け" value={record.photoUrl || ''} onChange={e => onUpdate(record.id, { photoUrl: e.target.value })} /><div><Badge>{record.type}</Badge><h2 className="mt-3 text-2xl font-bold leading-tight">{record.name}</h2><p className="mt-2 text-sm text-slate-600">{record.zip ? `〒${record.zip} ` : ''}{record.address}</p>{record.distanceKm != null && <p className="mt-2 text-sm font-bold text-blue-700">現在地から{distanceText(record.distanceKm)}</p>}</div><div className="grid grid-cols-2 gap-2 text-sm"><Info label="電話" value={record.phone} /><Info label="FAX" value={record.fax} /><Info label="区" value={record.ward} /><Info label="優先度" value={record.priority} /></div><div className="space-y-2"><label className="text-sm font-bold">営業ステータス</label><Select value={record.status} onChange={value => onUpdate(record.id, { status: value })} options={STATUSES} /></div><div className="space-y-2"><label className="text-sm font-bold">優先度</label><div className="grid grid-cols-3 gap-2">{PRIORITIES.map(p => <Button key={p} variant={record.priority === p ? 'default' : 'outline'} className="rounded-xl" onClick={() => onUpdate(record.id, { priority: p })}>{p}</Button>)}</div></div><div className="space-y-2"><label className="text-sm font-bold">営業メモ</label><textarea className="min-h-32 w-full rounded-xl border px-3 py-2" value={record.memo || ''} onChange={e => onUpdate(record.id, { memo: e.target.value })} placeholder="担当者名、架電結果、次回アクションなど" /></div><div className="grid grid-cols-2 gap-2"><Button className="rounded-xl" onClick={onCall}><Phone size={16} />電話</Button><Button variant="outline" className="rounded-xl" onClick={onMap}><MapPin size={16} />地図</Button><Button variant="outline" className="rounded-xl" onClick={onPlan}><CheckCircle2 size={16} />訪問予定</Button><Button variant={inRoute ? 'default' : 'outline'} className="rounded-xl" onClick={onRoute}><Route size={16} />{inRoute ? '追加済' : 'ルート追加'}</Button><Button variant="outline" className="col-span-2 rounded-xl" onClick={onVisited}><CheckCircle2 size={16} />訪問済として記録</Button></div></div>; }

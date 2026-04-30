import React, { useEffect, useMemo, useState } from 'react';
import { Search, Phone, MapPin, Building2, Download, Upload, Filter, ClipboardList, Star, Users, CalendarDays, Route, CheckCircle2, Plus, X, LocateFixed, Navigation, Image as ImageIcon, Camera } from 'lucide-react';

const Card = ({ className = '', children }) => <div className={`bg-white border ${className}`}>{children}</div>;
const CardContent = ({ className = '', children }) => <div className={className}>{children}</div>;
const Button = ({ className = '', variant = 'default', size, disabled, children, ...props }) => {
  const base = 'inline-flex items-center justify-center font-medium transition disabled:opacity-50 disabled:pointer-events-none';
  const variants = {
    default: 'bg-slate-900 text-white hover:bg-slate-700',
    outline: 'bg-white border text-slate-900 hover:bg-slate-100'
  };
  const sizes = size === 'sm' ? 'px-2 py-1 text-xs' : 'px-4 py-2 text-sm';
  return <button className={`${base} ${variants[variant] || variants.default} ${sizes} ${className}`} disabled={disabled} {...props}>{children}</button>;
};

const STORAGE_KEYS = {
  records: 'osaka-care-sales-records-v1',
  visits: 'osaka-care-sales-visit-logs-v1',
  route: 'osaka-care-sales-route-v1'
};

function readStorage(key, fallback) {
  try {
    const raw = localStorage.getItem(key);
    return raw ? JSON.parse(raw) : fallback;
  } catch {
    return fallback;
  }
}

function writeStorage(key, value) {
  try {
    localStorage.setItem(key, JSON.stringify(value));
  } catch {
    // 保存容量不足などの場合でもアプリ操作は継続します
  }
}

const INITIAL_RECORDS = [
  { id: 'hokatsu-kita', type: '地域包括支援センター', ward: '北区', name: '北区地域包括支援センター', zip: '530-0026', address: '大阪市北区神山町15-11', phone: '06-6313-5568', fax: '06-6313-6377', status: '未アプローチ', priority: 'A', memo: '大阪市公開CSV・一覧掲載' },
  { id: 'hokatsu-kita-oyodo', type: '地域包括支援センター', ward: '北区', name: '北区大淀地域包括支援センター', zip: '531-0062', address: '大阪市北区長柄中1-1-21', phone: '06-6354-1165', fax: '06-6354-1175', status: '未アプローチ', priority: 'A', memo: '大阪市公開CSV・一覧掲載' },
  { id: 'hokatsu-miyakojima', type: '地域包括支援センター', ward: '都島区', name: '都島区地域包括支援センター', zip: '534-0021', address: '大阪市都島区都島本通3-12-31', phone: '06-6929-9500', fax: '06-6929-9504', status: '未アプローチ', priority: 'A', memo: '大阪市公開CSV・一覧掲載' },
  { id: 'hokatsu-fukushima', type: '地域包括支援センター', ward: '福島区', name: '福島区地域包括支援センター', zip: '553-0001', address: '大阪市福島区海老江6-2-22', phone: '06-6454-6330', fax: '06-6454-6331', status: '未アプローチ', priority: 'A', memo: '大阪市公開CSV・一覧掲載' },
  { id: 'hokatsu-chuo', type: '地域包括支援センター', ward: '中央区', name: '中央区地域包括支援センター', zip: '542-0062', address: '大阪市中央区上本町西2-5-25', phone: '06-6763-8139', fax: '06-6763-8151', status: '未アプローチ', priority: 'A', memo: '大阪市公開CSV・一覧掲載' },
  { id: 'hokatsu-nishi', type: '地域包括支援センター', ward: '西区', name: '西区地域包括支援センター', zip: '550-0013', address: '大阪市西区新町4-5-14 西区役所合同庁舎6階', phone: '06-6539-8075', fax: '06-6539-8073', status: '未アプローチ', priority: 'A', memo: '大阪市公開CSV・一覧掲載' },
  { id: 'hokatsu-yodogawa', type: '地域包括支援センター', ward: '淀川区', name: '淀川区地域包括支援センター', zip: '532-0005', address: '大阪市淀川区三国本町2-14-3', phone: '06-6394-2914', fax: '06-6394-2977', status: '未アプローチ', priority: 'A', memo: '大阪市公開CSV・一覧掲載' },
  { id: 'hokatsu-abeno', type: '地域包括支援センター', ward: '阿倍野区', name: '阿倍野区地域包括支援センター', zip: '545-0037', address: '大阪市阿倍野区帝塚山1-3-8', phone: '06-6628-1400', fax: '06-6628-9393', status: '未アプローチ', priority: 'A', memo: '大阪市公開CSV・一覧掲載' },
  { id: 'hokatsu-suminoe', type: '地域包括支援センター', ward: '住之江区', name: '住之江区地域包括支援センター', zip: '559-0013', address: '大阪市住之江区御崎4-6-10', phone: '06-6686-2235', fax: '06-6686-2122', status: '未アプローチ', priority: 'A', memo: '大阪市公開CSV・一覧掲載' },
  { id: 'hokatsu-nishinari', type: '地域包括支援センター', ward: '西成区', name: '西成区地域包括支援センター', zip: '557-0041', address: '大阪市西成区岸里1-5-20 西成区合同庁舎8階', phone: '06-6656-0080', fax: '06-6656-0083', status: '未アプローチ', priority: 'A', memo: '大阪市公開CSV・一覧掲載' },
  { id: 'kyotaku-saiseikai-nakatsu', type: '居宅介護支援事業所', ward: '北区', name: '済生会中津病院', zip: '530-0012', address: '大阪市北区芝田2-10-39', phone: '06-6372-0733', fax: '06-6372-0752', status: '未アプローチ', priority: 'A', memo: '事業所番号 2774100040' },
  { id: 'kyotaku-yukioka', type: '居宅介護支援事業所', ward: '北区', name: '社会医療法人 行岡医学研究会 行岡病院', zip: '', address: '大阪市北区浮田2-2-3', phone: '', fax: '', status: '未アプローチ', priority: 'B', memo: '公開介護情報掲載' },
  { id: 'kyotaku-ishii', type: '居宅介護支援事業所', ward: '北区', name: '医療法人石井クリニック', zip: '', address: '大阪市北区菅栄町10-12', phone: '', fax: '', status: '未アプローチ', priority: 'B', memo: '公開介護情報掲載' },
  { id: 'kyotaku-kita-houkan', type: '居宅介護支援事業所', ward: '北区', name: '医師会立 北区訪問看護ステーション', zip: '', address: '大阪市北区神山町15-11', phone: '', fax: '', status: '未アプローチ', priority: 'B', memo: '公開介護情報掲載' },
  { id: 'kyotaku-minato-coop', type: '居宅介護支援事業所', ward: '港区', name: '居宅介護支援事業所コープみなと介護よろず相談所', zip: '552-0003', address: '大阪市港区磯路三丁目3番4号', phone: '06-6571-7880', fax: '06-6571-5659', status: '未アプローチ', priority: 'A', memo: '大阪市公開CSV掲載' },
  { id: 'kyotaku-nishinari-imamiya', type: '居宅介護支援事業所', ward: '西成区', name: '今宮ケアプランセンター', zip: '557-0014', address: '大阪市西成区天下茶屋一丁目31番9号', phone: '06-6656-6300', fax: '06-6656-6322', status: '未アプローチ', priority: 'A', memo: '大阪市公開PDF掲載' },
  { id: 'kyotaku-nishinari-banana', type: '居宅介護支援事業所', ward: '西成区', name: '居宅介護支援事業所ばなな', zip: '557-0014', address: '大阪市西成区天下茶屋二丁目18番13号', phone: '06-6655-6018', fax: '06-6655-6028', status: '未アプローチ', priority: 'B', memo: '大阪市公開PDF掲載' },
  { id: 'kyotaku-nishinari-ribu', type: '居宅介護支援事業所', ward: '西成区', name: 'りぶケアプランセンター', zip: '557-0014', address: '大阪市西成区天下茶屋三丁目24番15-404号 メゾンドゥアルシオン', phone: '06-6654-9266', fax: '06-6654-9276', status: '未アプローチ', priority: 'B', memo: '大阪市公開PDF掲載' },
  { id: 'kyotaku-nishinari-paul', type: '居宅介護支援事業所', ward: '西成区', name: 'ポールケアプランセンター', zip: '557-0014', address: '大阪市西成区天下茶屋二丁目23番6号', phone: '06-6690-0391', fax: '06-6690-0392', status: '未アプローチ', priority: 'B', memo: '大阪市公開PDF掲載' },
  { id: 'kyotaku-nishinari-tsubasa', type: '居宅介護支援事業所', ward: '西成区', name: 'バリアフリーサービスつばさケア・ステーション', zip: '557-0016', address: '大阪市西成区花園北二丁目5番7号', phone: '06-6636-5502', fax: '06-6636-5503', status: '未アプローチ', priority: 'B', memo: '大阪市公開PDF掲載' },
  { id: 'kyotaku-nishinari-human', type: '居宅介護支援事業所', ward: '西成区', name: 'ヒューマンケアプランセンター', zip: '557-0023', address: '大阪市西成区南開一丁目6番10号 アイビスコート1階', phone: '06-6563-6578', fax: '06-6563-6646', status: '未アプローチ', priority: 'A', memo: '大阪市公開PDF掲載' },
  { id: 'kyotaku-nishinari-ikoi', type: '居宅介護支援事業所', ward: '西成区', name: 'そーしゃるさぽーと憩', zip: '557-0023', address: '大阪市西成区南開二丁目2番7号', phone: '06-4392-0151', fax: '06-4392-0152', status: '未アプローチ', priority: 'B', memo: '大阪市公開PDF掲載' },
  { id: 'kyotaku-nishinari-animo', type: '居宅介護支援事業所', ward: '西成区', name: '居宅介護支援あにも', zip: '557-0025', address: '大阪市西成区長橋一丁目7番19号', phone: '06-6643-6733', fax: '06-6645-6606', status: '未アプローチ', priority: 'B', memo: '大阪市公開PDF掲載' },
  { id: 'kyotaku-nishinari-mayuu', type: '居宅介護支援事業所', ward: '西成区', name: 'マユウ介護サービス', zip: '557-0031', address: '大阪市西成区鶴見橋三丁目6番15号2階', phone: '06-6567-3612', fax: '06-6567-3613', status: '未アプローチ', priority: 'B', memo: '大阪市公開PDF掲載' },
  { id: 'kyotaku-nishinari-hotaru', type: '居宅介護支援事業所', ward: '西成区', name: 'ほたるソーシャルワーク', zip: '557-0031', address: '大阪市西成区鶴見橋二丁目1番8号', phone: '06-6556-7481', fax: '06-6556-7482', status: '未アプローチ', priority: 'B', memo: '大阪市公開PDF掲載' },
  { id: 'kyotaku-nishinari-cyclo', type: '居宅介護支援事業所', ward: '西成区', name: 'シクロケアプランセンター', zip: '557-0031', address: '大阪市西成区鶴見橋一丁目6番32号', phone: '06-6629-8737', fax: '06-6629-8738', status: '未アプローチ', priority: 'A', memo: '大阪市公開PDF掲載' },
  { id: 'kyotaku-nishinari-asahi', type: '居宅介護支援事業所', ward: '西成区', name: 'あさひ在宅サービスセンター', zip: '557-0032', address: '大阪市西成区旭一丁目9番20号', phone: '06-6631-5222', fax: '06-6631-5223', status: '未アプローチ', priority: 'B', memo: '大阪市公開PDF掲載' }
];

const COORDS_BY_ID = {
  'hokatsu-kita': { lat: 34.7039, lng: 135.5074 },
  'hokatsu-kita-oyodo': { lat: 34.7109, lng: 135.5120 },
  'hokatsu-miyakojima': { lat: 34.7077, lng: 135.5287 },
  'hokatsu-fukushima': { lat: 34.6960, lng: 135.4728 },
  'hokatsu-chuo': { lat: 34.6778, lng: 135.5206 },
  'hokatsu-nishi': { lat: 34.6746, lng: 135.4868 },
  'hokatsu-yodogawa': { lat: 34.7352, lng: 135.4868 },
  'hokatsu-abeno': { lat: 34.6337, lng: 135.5136 },
  'hokatsu-suminoe': { lat: 34.6135, lng: 135.4820 },
  'hokatsu-nishinari': { lat: 34.6379, lng: 135.4945 },
  'kyotaku-saiseikai-nakatsu': { lat: 34.7073, lng: 135.4947 },
  'kyotaku-yukioka': { lat: 34.7087, lng: 135.5087 },
  'kyotaku-ishii': { lat: 34.7103, lng: 135.5123 },
  'kyotaku-kita-houkan': { lat: 34.7039, lng: 135.5074 },
  'kyotaku-minato-coop': { lat: 34.6655, lng: 135.4576 },
  'kyotaku-nishinari-imamiya': { lat: 34.6365, lng: 135.5003 },
  'kyotaku-nishinari-banana': { lat: 34.6379, lng: 135.5018 },
  'kyotaku-nishinari-ribu': { lat: 34.6373, lng: 135.5002 },
  'kyotaku-nishinari-paul': { lat: 34.6378, lng: 135.5008 },
  'kyotaku-nishinari-tsubasa': { lat: 34.6453, lng: 135.4985 },
  'kyotaku-nishinari-human': { lat: 34.6480, lng: 135.4887 },
  'kyotaku-nishinari-ikoi': { lat: 34.6472, lng: 135.4876 },
  'kyotaku-nishinari-animo': { lat: 34.6496, lng: 135.4925 },
  'kyotaku-nishinari-mayuu': { lat: 34.6449, lng: 135.4844 },
  'kyotaku-nishinari-hotaru': { lat: 34.6456, lng: 135.4890 },
  'kyotaku-nishinari-cyclo': { lat: 34.6467, lng: 135.4921 },
  'kyotaku-nishinari-asahi': { lat: 34.6464, lng: 135.4973 }
};

const wards = ['すべて', '北区', '都島区', '福島区', '此花区', '中央区', '西区', '港区', '大正区', '天王寺区', '浪速区', '西淀川区', '淀川区', '東淀川区', '東成区', '生野区', '旭区', '城東区', '鶴見区', '阿倍野区', '住之江区', '住吉区', '東住吉区', '平野区', '西成区'];
const statuses = ['未アプローチ', '初回架電済', '資料送付', '訪問予定', '訪問済', '商談化', '見込み薄', '契約済'];
const priorities = ['A', 'B', 'C'];

function normalizeCsvValue(value = '') {
  return value.replace(/^\uFEFF/, '').trim();
}

function parseCsv(text) {
  const rows = [];
  let row = [];
  let cell = '';
  let inQuotes = false;
  for (let i = 0; i < text.length; i++) {
    const char = text[i];
    const next = text[i + 1];
    if (char === '"' && inQuotes && next === '"') {
      cell += '"';
      i++;
    } else if (char === '"') {
      inQuotes = !inQuotes;
    } else if (char === ',' && !inQuotes) {
      row.push(normalizeCsvValue(cell));
      cell = '';
    } else if ((char === '\n' || char === '\r') && !inQuotes) {
      if (cell || row.length) {
        row.push(normalizeCsvValue(cell));
        rows.push(row);
        row = [];
        cell = '';
      }
      if (char === '\r' && next === '\n') i++;
    } else {
      cell += char;
    }
  }
  if (cell || row.length) {
    row.push(normalizeCsvValue(cell));
    rows.push(row);
  }
  return rows;
}

function findValue(obj, candidates) {
  const key = Object.keys(obj).find(k => candidates.some(c => k.includes(c)));
  return key ? obj[key] : '';
}

function inferWard(address = '') {
  const found = wards.find(w => w !== 'すべて' && address.includes(w));
  return found || '';
}

function distanceKm(a, b) {
  if (!a || !b) return null;
  const toRad = value => value * Math.PI / 180;
  const earthRadiusKm = 6371;
  const dLat = toRad(b.lat - a.lat);
  const dLng = toRad(b.lng - a.lng);
  const lat1 = toRad(a.lat);
  const lat2 = toRad(b.lat);
  const h = Math.sin(dLat / 2) ** 2 + Math.cos(lat1) * Math.cos(lat2) * Math.sin(dLng / 2) ** 2;
  return earthRadiusKm * 2 * Math.atan2(Math.sqrt(h), Math.sqrt(1 - h));
}

function formatDistance(km) {
  if (km == null) return '';
  return km < 1 ? `${Math.round(km * 1000)}m` : `${km.toFixed(1)}km`;
}

function mapCsvRows(rows, defaultType) {
  if (!rows.length) return [];
  const headers = rows[0].map(normalizeCsvValue);
  return rows.slice(1).filter(r => r.some(Boolean)).map((r, index) => {
    const obj = Object.fromEntries(headers.map((h, i) => [h, normalizeCsvValue(r[i] || '')]));
    const address = findValue(obj, ['住所', '所在地', '事業所所在地']);
    const name = findValue(obj, ['名称', '事業所名', '事業所の名称']) || `取込データ ${index + 1}`;
    const typeRaw = findValue(obj, ['サービス種類', '種別', '類型']);
    return {
      id: `csv-${Date.now()}-${index}`,
      type: typeRaw.includes('地域包括') ? '地域包括支援センター' : defaultType,
      ward: findValue(obj, ['区']) || inferWard(address),
      name,
      zip: findValue(obj, ['郵便番号']),
      address,
      phone: findValue(obj, ['電話番号', 'TEL', '連絡先']),
      fax: findValue(obj, ['FAX', 'ファックス']),
      status: '未アプローチ',
      priority: 'B',
      memo: '',
      photoUrl: findValue(obj, ['写真', '画像', 'photo', 'image'])
    };
  });
}

function exportCsv(records) {
  const headers = ['type', 'ward', 'name', 'zip', 'address', 'phone', 'fax', 'status', 'priority', 'memo'];
  const body = records.map(r => headers.map(h => `"${String(r[h] || '').replaceAll('"', '""')}"`).join(','));
  const csv = `﻿${headers.join(',')}
${body.join('
')}`;
  downloadTextFile(csv, 'osaka-care-sales-list.csv', 'text/csv;charset=utf-8;');
}

function exportVisitLogs(logs) {
  const headers = ['date', 'ward', 'type', 'name', 'address', 'phone', 'note'];
  const body = logs.map(r => headers.map(h => `"${String(r[h] || '').replaceAll('"', '""')}"`).join(','));
  const csv = `﻿${headers.join(',')}
${body.join('
')}`;
  downloadTextFile(csv, 'osaka-care-visit-logs.csv', 'text/csv;charset=utf-8;');
}

function downloadTextFile(text, filename, type) {
  const blob = new Blob([text], { type });
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a');
  a.href = url;
  a.download = filename;
  a.click();
  URL.revokeObjectURL(url);
}

export default function OsakaCareSalesApp() {
  const [records, setRecords] = useState(() => readStorage(STORAGE_KEYS.records, INITIAL_RECORDS));
  const [query, setQuery] = useState('');
  const [ward, setWard] = useState('すべて');
  const [type, setType] = useState('すべて');
  const [status, setStatus] = useState('すべて');
  const [selected, setSelected] = useState(records[0]);
  const [importType, setImportType] = useState('居宅介護支援事業所');
  const [routeIds, setRouteIds] = useState(() => readStorage(STORAGE_KEYS.route, []));
  const [visitDate, setVisitDate] = useState('');
  const [visitNote, setVisitNote] = useState('');
  const [visitLogs, setVisitLogs] = useState(() => readStorage(STORAGE_KEYS.visits, []));
  const [currentLocation, setCurrentLocation] = useState(null);
  const [locationError, setLocationError] = useState('');
  const [sortNearest, setSortNearest] = useState(false);
  const [nearbyLimit, setNearbyLimit] = useState(5);

  useEffect(() => writeStorage(STORAGE_KEYS.records, records), [records]);
  useEffect(() => writeStorage(STORAGE_KEYS.route, routeIds), [routeIds]);
  useEffect(() => writeStorage(STORAGE_KEYS.visits, visitLogs), [visitLogs]);

  const recordsWithDistance = useMemo(() => records.map(record => {
    const coords = COORDS_BY_ID[record.id] || record.coords;
    return {
      ...record,
      coords,
      distanceKm: currentLocation && coords ? distanceKm(currentLocation, coords) : null
    };
  }), [records, currentLocation]);

  const filtered = useMemo(() => recordsWithDistance.filter(r => {
    const text = `${r.type} ${r.ward} ${r.name} ${r.address} ${r.phone} ${r.memo}`.toLowerCase();
    return text.includes(query.toLowerCase()) &&
      (ward === 'すべて' || r.ward === ward) &&
      (type === 'すべて' || r.type === type) &&
      (status === 'すべて' || r.status === status);
    }).sort((a, b) => {
    if (!sortNearest || !currentLocation) return 0;
    const aDistance = a.distanceKm ?? Number.POSITIVE_INFINITY;
    const bDistance = b.distanceKm ?? Number.POSITIVE_INFINITY;
    return aDistance - bDistance;
  }), [recordsWithDistance, query, ward, type, status, sortNearest, currentLocation]);

  const groupedByWard = useMemo(() => {
    const groups = new Map();
    wards.filter(w => w !== 'すべて').forEach(w => groups.set(w, []));
    groups.set('区未設定', []);
    filtered.forEach(record => {
      const key = record.ward || '区未設定';
      if (!groups.has(key)) groups.set(key, []);
      groups.get(key).push(record);
    });
    return Array.from(groups.entries()).filter(([, items]) => items.length > 0);
  }, [filtered]);

  const routeRecords = useMemo(() => routeIds
    .map(id => recordsWithDistance.find(r => r.id === id))
    .filter(Boolean), [routeIds, recordsWithDistance]);

  const stats = useMemo(() => ({
    total: records.length,
    hokatsu: records.filter(r => r.type === '地域包括支援センター').length,
    kyotaku: records.filter(r => r.type === '居宅介護支援事業所').length,
    hot: records.filter(r => ['商談化', '訪問予定', '契約済'].includes(r.status)).length,
    visited: records.filter(r => r.status === '訪問済').length
  }), [records]);

  const updateRecord = (id, patch) => {
    setRecords(prev => prev.map(r => r.id === id ? { ...r, ...patch } : r));
    setSelected(prev => prev?.id === id ? { ...prev, ...patch } : prev);
  };

  const setPhotoUrl = (record, photoUrl) => {
    updateRecord(record.id, { photoUrl });
  };

  const uploadPhoto = async (record, event) => {
    const file = event.target.files?.[0];
    if (!file) return;
    const reader = new FileReader();
    reader.onload = () => setPhotoUrl(record, reader.result);
    reader.readAsDataURL(file);
    event.target.value = '';
  };

  const openStreetView = (record) => {
    const coords = record.coords || COORDS_BY_ID[record.id];
    const query = coords ? `${coords.lat},${coords.lng}` : record.address;
    window.open(`https://www.google.com/maps/search/?api=1&query=${encodeURIComponent(query)}`, '_blank');
  };

  const toggleRoute = (id) => {
    setRouteIds(prev => prev.includes(id) ? prev.filter(routeId => routeId !== id) : [...prev, id]);
  };

  const locateMe = () => {
    setLocationError('');
    if (!navigator.geolocation) {
      setLocationError('この端末では現在地を取得できません。');
      return;
    }
    navigator.geolocation.getCurrentPosition(
      position => {
        setCurrentLocation({ lat: position.coords.latitude, lng: position.coords.longitude });
        setSortNearest(true);
      },
      () => setLocationError('現在地を取得できませんでした。ブラウザの位置情報許可を確認してください。'),
      { enableHighAccuracy: true, timeout: 10000, maximumAge: 60000 }
    );
  };

  const addNearbyToRoute = () => {
    if (!currentLocation) {
      locateMe();
      return;
    }
    const nearestIds = filtered
      .filter(r => r.distanceKm != null && r.status !== '訪問済')
      .sort((a, b) => a.distanceKm - b.distanceKm)
      .slice(0, Number(nearbyLimit))
      .map(r => r.id);
    setRouteIds(prev => Array.from(new Set([...prev, ...nearestIds])));
    setSortNearest(true);
  };

  const markVisitPlanned = (record) => {
    updateRecord(record.id, {
      status: '訪問予定',
      memo: `${record.memo ? `${record.memo}
` : ''}${visitDate ? `${visitDate} ` : ''}訪問予定`
    });
    if (!routeIds.includes(record.id)) setRouteIds(prev => [...prev, record.id]);
  };

  const openRouteMap = () => {
    const destinations = routeRecords.filter(r => r.address).map(r => r.address);
    if (!destinations.length) return;
    const start = currentLocation ? `${currentLocation.lat},${currentLocation.lng}` : '';
    const url = currentLocation
      ? `https://www.google.com/maps/dir/${encodeURIComponent(start)}/${destinations.map(address => encodeURIComponent(address)).join('/')}`
      : destinations.length === 1
        ? `https://www.google.com/maps/search/${encodeURIComponent(destinations[0])}`
        : `https://www.google.com/maps/dir/${destinations.map(address => encodeURIComponent(address)).join('/')}`;
    window.open(url, '_blank');
  };

  const openNearestMap = (record) => {
    if (!record?.address) return;
    const start = currentLocation ? `${currentLocation.lat},${currentLocation.lng}` : '現在地';
    window.open(`https://www.google.com/maps/dir/${encodeURIComponent(start)}/${encodeURIComponent(record.address)}`, '_blank');
  };

  const markVisited = (record) => {
    const date = visitDate || new Date().toISOString().slice(0, 10);
    const note = visitNote || '訪問済み';
    updateRecord(record.id, {
      status: '訪問済',
      memo: `${record.memo ? `${record.memo}
` : ''}${date} 訪問済：${note}`
    });
    setVisitLogs(prev => [{
      id: `visit-${Date.now()}`,
      recordId: record.id,
      name: record.name,
      type: record.type,
      ward: record.ward,
      address: record.address,
      phone: record.phone,
      date,
      note
    }, ...prev]);
    setVisitNote('');
    setRouteIds(prev => prev.filter(id => id !== record.id));
  };

  const clearRoute = () => setRouteIds([]);

  const onImport = async (event) => {
    const file = event.target.files?.[0];
    if (!file) return;
    const buffer = await file.arrayBuffer();
    const decoder = new TextDecoder('utf-8');
    let text = decoder.decode(buffer);
    if (text.includes('�')) text = new TextDecoder('shift-jis').decode(buffer);
    const imported = mapCsvRows(parseCsv(text), importType);
    setRecords(prev => [...prev.filter(r => !r.id.startsWith('kyotaku-sample')), ...imported]);
    setSelected(imported[0] || selected);
    event.target.value = '';
  };

  return (
    <div className="min-h-screen bg-slate-50 text-slate-900 p-6">
      <div className="max-w-7xl mx-auto space-y-5">
        <header className="flex flex-col gap-4 md:flex-row md:items-end md:justify-between">
          <div>
            <p className="text-sm font-medium text-slate-500">大阪市 介護・高齢者支援向け</p>
            <h1 className="text-3xl font-bold tracking-tight">営業リストCRM</h1>
            <p className="text-slate-600 mt-2">現在地から近い事業所を探し、電話・訪問予定・地図ルート・訪問記録を一画面で管理できます。入力内容はこのブラウザに自動保存されます。</p>
          </div>
          <div className="flex gap-2 flex-wrap">
            <select className="rounded-xl border bg-white px-3 py-2 text-sm" value={importType} onChange={e => setImportType(e.target.value)}>
              <option>居宅介護支援事業所</option>
              <option>地域包括支援センター</option>
            </select>
            <label className="inline-flex items-center gap-2 rounded-xl bg-white border px-4 py-2 text-sm font-medium cursor-pointer hover:bg-slate-100">
              <Upload size={16} /> CSV取込
              <input type="file" accept=".csv,text/csv" onChange={onImport} className="hidden" />
            </label>
            <Button onClick={() => exportCsv(records)} className="rounded-xl gap-2"><Download size={16} />営業リストCSV</Button>
          </div>
        </header>

        <div className="grid grid-cols-2 md:grid-cols-5 gap-3">
          <StatCard icon={<Users />} label="全件" value={stats.total} />
          <StatCard icon={<Building2 />} label="地域包括" value={stats.hokatsu} />
          <StatCard icon={<ClipboardList />} label="居宅介護支援" value={stats.kyotaku} />
          <StatCard icon={<Star />} label="有望案件" value={stats.hot} />
          <StatCard icon={<CheckCircle2 />} label="訪問済" value={stats.visited} />
        </div>

        <Card className="rounded-2xl shadow-sm">
          <CardContent className="p-4 grid grid-cols-1 md:grid-cols-5 gap-3">
            <div className="md:col-span-2 relative">
              <Search className="absolute left-3 top-3 text-slate-400" size={18} />
              <input className="w-full rounded-xl border pl-10 pr-3 py-2" placeholder="名称・住所・電話・メモで検索" value={query} onChange={e => setQuery(e.target.value)} />
            </div>
            <SelectWithIcon icon={<MapPin size={16} />} value={ward} setValue={setWard} options={wards} />
            <SelectWithIcon icon={<Filter size={16} />} value={type} setValue={setType} options={['すべて', '地域包括支援センター', '居宅介護支援事業所']} />
            <SelectWithIcon icon={<CalendarDays size={16} />} value={status} setValue={setStatus} options={['すべて', ...statuses]} />
          </CardContent>
        </Card>

        <Card className="rounded-2xl shadow-sm border-slate-300">
          <CardContent className="p-4 space-y-3">
            <div className="rounded-2xl bg-blue-50 border border-blue-100 p-4 space-y-3">
              <div className="flex flex-col gap-3 md:flex-row md:items-center md:justify-between">
                <div>
                  <div className="flex items-center gap-2 font-bold"><LocateFixed size={18} />現在地から近い事業所</div>
                  <p className="text-sm text-slate-600 mt-1">外出先・車内・訪問先など、どこにいても現在地から近い順に表示してルート化できます。</p>
                  {currentLocation && <p className="text-xs text-slate-500 mt-1">現在地取得済み：緯度 {currentLocation.lat.toFixed(5)} / 経度 {currentLocation.lng.toFixed(5)}</p>}
                  {locationError && <p className="text-xs text-red-600 mt-1">{locationError}</p>}
                </div>
                <div className="flex gap-2 flex-wrap">
                  <Button className="rounded-xl gap-2" onClick={locateMe}><LocateFixed size={16} />現在地取得</Button>
                  <Button variant={sortNearest ? 'default' : 'outline'} className="rounded-xl gap-2" onClick={() => setSortNearest(v => !v)} disabled={!currentLocation}><Navigation size={16} />近い順</Button>
                  <select className="rounded-xl border bg-white px-3 py-2 text-sm" value={nearbyLimit} onChange={e => setNearbyLimit(e.target.value)}>
                    <option value="3">近くの3件</option>
                    <option value="5">近くの5件</option>
                    <option value="8">近くの8件</option>
                    <option value="10">近くの10件</option>
                  </select>
                  <Button variant="outline" className="rounded-xl gap-2" onClick={addNearbyToRoute}><Route size={16} />近い事業所をルート追加</Button>
                </div>
              </div>
            </div>
            <div className="flex flex-col gap-3 md:flex-row md:items-center md:justify-between">
              <div>
                <div className="flex items-center gap-2 font-bold"><Route size={18} />本日の訪問ルート</div>
                <p className="text-sm text-slate-600 mt-1">訪問先を追加すると、Googleマップで巡回ルートを開けます。現在地取得後は、現在地スタートのルートになります。</p>
              </div>
              <div className="flex gap-2 flex-wrap">
                <input type="date" className="rounded-xl border px-3 py-2 text-sm" value={visitDate} onChange={e => setVisitDate(e.target.value)} />
                <input className="rounded-xl border px-3 py-2 text-sm min-w-56" placeholder="訪問メモ例：所長不在・資料渡し" value={visitNote} onChange={e => setVisitNote(e.target.value)} />
                <Button className="rounded-xl gap-2" onClick={openRouteMap} disabled={!routeRecords.length}><MapPin size={16} />ルート地図</Button>
                <Button variant="outline" className="rounded-xl gap-2" onClick={clearRoute} disabled={!routeRecords.length}><X size={16} />クリア</Button>
              </div>
            </div>
            <div className="flex gap-2 overflow-x-auto pb-1">
              {routeRecords.length ? routeRecords.map((record, index) => (
                <div key={record.id} className="min-w-64 rounded-xl bg-slate-50 border p-3">
                  <div className="text-xs font-bold text-slate-500">{index + 1}件目・{record.ward}{record.distanceKm != null ? `・現在地から${formatDistance(record.distanceKm)}` : ''}</div>
                  <div className="font-semibold mt-1 truncate">{record.name}</div>
                  <div className="text-xs text-slate-600 truncate">{record.address}</div>
                  <div className="flex gap-2 mt-2">
                    <Button size="sm" className="rounded-lg h-8" onClick={() => record.phone && (window.location.href = `tel:${record.phone}`)}><Phone size={14} /></Button>
                    <Button size="sm" variant="outline" className="rounded-lg h-8" onClick={() => openNearestMap(record)}><MapPin size={14} /></Button>
                    <Button size="sm" variant="outline" className="rounded-lg h-8" onClick={() => markVisited(record)}><CheckCircle2 size={14} /></Button>
                    <Button size="sm" variant="outline" className="rounded-lg h-8" onClick={() => toggleRoute(record.id)}><X size={14} /></Button>
                  </div>
                </div>
              )) : <div className="rounded-xl bg-slate-50 border p-4 text-sm text-slate-500 w-full">リストから「ルート追加」を押すと、訪問順にここへ追加されます。</div>}
            </div>
          </CardContent>
        </Card>

        <main className="grid grid-cols-1 lg:grid-cols-3 gap-5">
          <section className="lg:col-span-2 space-y-5">
            {groupedByWard.map(([wardName, items]) => (
              <div key={wardName} className="space-y-3">
                <div className="flex items-center justify-between rounded-2xl bg-slate-900 text-white px-4 py-3">
                  <h2 className="font-bold text-lg">{wardName}</h2>
                  <span className="text-sm bg-white/15 rounded-full px-3 py-1">{items.length}件</span>
                </div>
                {items.map(record => (
                  <button key={record.id} onClick={() => setSelected(record)} className={`w-full text-left rounded-2xl border bg-white p-4 hover:shadow-md transition ${selected?.id === record.id ? 'ring-2 ring-slate-900' : ''}`}>
                    <div className="flex items-start justify-between gap-3">
                      <div className="flex gap-3 flex-1 min-w-0">
                        <PhotoThumb record={record} />
                        <div className="min-w-0 flex-1">
                        <div className="flex gap-2 flex-wrap mb-2">
                          <Badge>{record.type}</Badge><Priority priority={record.priority} />
                        </div>
                        <h3 className="font-bold text-lg">{record.name}</h3>
                        {record.distanceKm != null && <p className="text-sm font-semibold text-blue-700 mt-1">現在地から約{formatDistance(record.distanceKm)}</p>}
                        <p className="text-sm text-slate-600 mt-1"><MapPin size={14} className="inline mr-1" />{record.address || '住所未登録'}</p>
                        <p className="text-sm text-slate-600 mt-1"><Phone size={14} className="inline mr-1" />{record.phone || '電話未登録'}</p>
                        <div className="flex gap-2 mt-3 flex-wrap">
                          <span onClick={(e) => { e.stopPropagation(); record.phone && (window.location.href = `tel:${record.phone}`); }} className="inline-flex items-center gap-1 rounded-lg bg-slate-900 text-white px-3 py-1.5 text-xs font-semibold cursor-pointer"><Phone size={13} />電話</span>
                          <span onClick={(e) => { e.stopPropagation(); markVisitPlanned(record); }} className="inline-flex items-center gap-1 rounded-lg bg-white border px-3 py-1.5 text-xs font-semibold cursor-pointer"><CheckCircle2 size={13} />訪問予定</span>
                          <span onClick={(e) => { e.stopPropagation(); toggleRoute(record.id); }} className={`inline-flex items-center gap-1 rounded-lg border px-3 py-1.5 text-xs font-semibold cursor-pointer ${routeIds.includes(record.id) ? 'bg-slate-900 text-white' : 'bg-white'}`}><Plus size={13} />ルート追加</span>
                          <span onClick={(e) => { e.stopPropagation(); markVisited(record); }} className="inline-flex items-center gap-1 rounded-lg bg-emerald-50 border border-emerald-200 px-3 py-1.5 text-xs font-semibold cursor-pointer"><CheckCircle2 size={13} />訪問済</span>
                          <span onClick={(e) => { e.stopPropagation(); openNearestMap(record); }} className="inline-flex items-center gap-1 rounded-lg bg-white border px-3 py-1.5 text-xs font-semibold cursor-pointer"><MapPin size={13} />ルート</span>
                        </div>
                      </div>
                      </div>
                      <span className="rounded-full bg-slate-100 px-3 py-1 text-xs font-semibold whitespace-nowrap">{record.status}</span>
                    </div>
                  </button>
                ))}
              </div>
            ))}
            {!filtered.length && <div className="rounded-2xl border bg-white p-8 text-center text-slate-500">条件に一致するリストがありません。</div>}
          </section>

          <aside className="lg:sticky lg:top-6 h-fit">
            <Card className="rounded-2xl shadow-sm">
              <CardContent className="p-5 space-y-4">
                {selected ? (
                  <>
                    <div>
                      <PhotoLarge record={selected} />
                      <div className="flex gap-2 mt-3 flex-wrap">
                        <label className="inline-flex items-center gap-2 rounded-xl bg-white border px-3 py-2 text-sm font-medium cursor-pointer hover:bg-slate-100">
                          <Camera size={16} />写真を登録
                          <input type="file" accept="image/*" capture="environment" onChange={(e) => uploadPhoto(selected, e)} className="hidden" />
                        </label>
                        <input className="flex-1 min-w-48 rounded-xl border px-3 py-2 text-sm" placeholder="写真URLを貼り付け" value={selected.photoUrl || ''} onChange={e => setPhotoUrl(selected, e.target.value)} />
                        <Button variant="outline" className="rounded-xl gap-2" onClick={() => openStreetView(selected)}><ImageIcon size={16} />Googleで見る</Button>
                        {selected.photoUrl && <Button variant="outline" className="rounded-xl" onClick={() => setPhotoUrl(selected, '')}>写真削除</Button>}
                      </div>
                    </div>
                    <div>
                      <Badge>{selected.type}</Badge>
                      <h2 className="text-2xl font-bold mt-3">{selected.name}</h2>
                      <p className="text-sm text-slate-600 mt-2">{selected.zip && `〒${selected.zip} `}{selected.address}</p>
                      {selected.distanceKm != null && <p className="text-sm font-semibold text-blue-700 mt-2">現在地から約{formatDistance(selected.distanceKm)}</p>}
                    </div>
                    <div className="grid grid-cols-2 gap-2 text-sm">
                      <Info label="電話" value={selected.phone} />
                      <Info label="FAX" value={selected.fax} />
                      <Info label="区" value={selected.ward} />
                      <Info label="優先度" value={selected.priority} />
                    </div>
                    <div className="space-y-2">
                      <label className="text-sm font-semibold">営業ステータス</label>
                      <select className="w-full rounded-xl border px-3 py-2" value={selected.status} onChange={e => updateRecord(selected.id, { status: e.target.value })}>
                        {statuses.map(s => <option key={s}>{s}</option>)}
                      </select>
                    </div>
                    <div className="space-y-2">
                      <label className="text-sm font-semibold">優先度</label>
                      <div className="flex gap-2">
                        {priorities.map(p => <Button key={p} variant={selected.priority === p ? 'default' : 'outline'} className="rounded-xl flex-1" onClick={() => updateRecord(selected.id, { priority: p })}>{p}</Button>)}
                      </div>
                    </div>
                    <div className="space-y-2">
                      <label className="text-sm font-semibold">営業メモ</label>
                      <textarea className="w-full min-h-32 rounded-xl border px-3 py-2" value={selected.memo} onChange={e => updateRecord(selected.id, { memo: e.target.value })} placeholder="担当者名、架電結果、次回アクションなど" />
                    </div>
                    <div className="grid grid-cols-2 gap-2">
                      <Button className="rounded-xl gap-2" onClick={() => selected.phone && (window.location.href = `tel:${selected.phone}`)}><Phone size={16} />電話する</Button>
                      <Button variant="outline" className="rounded-xl gap-2" onClick={() => openNearestMap(selected)}><MapPin size={16} />現在地からルート</Button>
                      <Button variant="outline" className="rounded-xl gap-2" onClick={() => markVisitPlanned(selected)}><CheckCircle2 size={16} />訪問予定</Button>
                      <Button variant={routeIds.includes(selected.id) ? 'default' : 'outline'} className="rounded-xl gap-2" onClick={() => toggleRoute(selected.id)}><Route size={16} />{routeIds.includes(selected.id) ? '追加済み' : 'ルート追加'}</Button>
                      <Button variant="outline" className="rounded-xl gap-2 col-span-2" onClick={() => markVisited(selected)}><CheckCircle2 size={16} />訪問済として記録</Button>
                    </div>
                  </>
                ) : <p className="text-slate-500">左のリストから選択してください。</p>}
              </CardContent>
            </Card>
          </aside>
        </main>

        <Card className="rounded-2xl shadow-sm">
          <CardContent className="p-5 space-y-3">
            <div className="flex items-center justify-between">
              <div>
                <h2 className="font-bold text-lg">訪問記録</h2>
                <p className="text-sm text-slate-600">訪問済みにした事業所が日付・メモ付きで残ります。</p>
              </div>
              <div className="flex gap-2">
                <Button variant="outline" className="rounded-xl" onClick={() => exportVisitLogs(visitLogs)} disabled={!visitLogs.length}>訪問記録CSV</Button>
                <Button variant="outline" className="rounded-xl" onClick={() => setVisitLogs([])} disabled={!visitLogs.length}>記録クリア</Button>
              </div>
            </div>
            {visitLogs.length ? (
              <div className="overflow-x-auto">
                <table className="w-full text-sm">
                  <thead>
                    <tr className="text-left text-slate-500 border-b">
                      <th className="py-2 pr-3">訪問日</th>
                      <th className="py-2 pr-3">区</th>
                      <th className="py-2 pr-3">事業所</th>
                      <th className="py-2 pr-3">電話</th>
                      <th className="py-2 pr-3">メモ</th>
                    </tr>
                  </thead>
                  <tbody>
                    {visitLogs.map(log => (
                      <tr key={log.id} className="border-b last:border-0">
                        <td className="py-2 pr-3 whitespace-nowrap">{log.date}</td>
                        <td className="py-2 pr-3 whitespace-nowrap">{log.ward}</td>
                        <td className="py-2 pr-3 font-semibold">{log.name}</td>
                        <td className="py-2 pr-3 whitespace-nowrap">{log.phone || '-'}</td>
                        <td className="py-2 pr-3">{log.note}</td>
                      </tr>
                    ))}
                  </tbody>
                </table>
              </div>
            ) : <div className="rounded-xl bg-slate-50 border p-4 text-sm text-slate-500">まだ訪問記録はありません。リストまたは詳細画面の「訪問済」を押すと記録されます。</div>}
          </CardContent>
        </Card>
      </div>
    </div>
  );
}

function StatCard({ icon, label, value }) {
  return <Card className="rounded-2xl shadow-sm"><CardContent className="p-4 flex items-center gap-3"><div className="rounded-2xl bg-slate-100 p-3 text-slate-700">{React.cloneElement(icon, { size: 20 })}</div><div><p className="text-sm text-slate-500">{label}</p><p className="text-2xl font-bold">{value}</p></div></CardContent></Card>;
}

function SelectWithIcon({ icon, value, setValue, options }) {
  return <div className="relative"><span className="absolute left-3 top-3 text-slate-400">{icon}</span><select className="w-full rounded-xl border bg-white pl-9 pr-3 py-2" value={value} onChange={e => setValue(e.target.value)}>{options.map(o => <option key={o}>{o}</option>)}</select></div>;
}

function Badge({ children }) {
  return <span className="inline-flex rounded-full bg-slate-100 px-2.5 py-1 text-xs font-semibold text-slate-700">{children}</span>;
}

function Priority({ priority }) {
  return <span className="inline-flex rounded-full bg-white border px-2.5 py-1 text-xs font-bold">優先度 {priority}</span>;
}

function Info({ label, value }) {
  return <div className="rounded-xl bg-slate-50 p-3"><p className="text-xs text-slate-500">{label}</p><p className="font-semibold break-all">{value || '-'}</p></div>;
}

function PhotoThumb({ record }) {
  return record.photoUrl ? (
    <img src={record.photoUrl} alt={`${record.name}の写真`} className="w-20 h-20 rounded-xl object-cover border bg-slate-100 shrink-0" />
  ) : (
    <div className="w-20 h-20 rounded-xl border bg-slate-100 shrink-0 flex flex-col items-center justify-center text-slate-400">
      <ImageIcon size={22} />
      <span className="text-[10px] mt-1">写真なし</span>
    </div>
  );
}

function PhotoLarge({ record }) {
  return record.photoUrl ? (
    <img src={record.photoUrl} alt={`${record.name}の写真`} className="w-full h-48 rounded-2xl object-cover border bg-slate-100" />
  ) : (
    <div className="w-full h-48 rounded-2xl border bg-slate-100 flex flex-col items-center justify-center text-slate-500">
      <ImageIcon size={34} />
      <p className="font-semibold mt-2">写真未登録</p>
      <p className="text-xs mt-1">訪問時の外観写真や写真URLを登録できます</p>
    </div>
  );
}

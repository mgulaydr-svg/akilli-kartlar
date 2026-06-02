# Akıllı Kartlar

React + TypeScript + Firebase ile hazırlanmış, web tabanlı flashcard öğrenme uygulaması.

## Özellikler

- E-posta/şifre ile giriş ve kayıt
- Firebase Auth + Firestore veri saklama
- Deste oluşturma
- Kart ekleme, düzenleme ve yumuşak silme
- CSV, JSON ve TXT dosyalarından NotebookLM kartlarını içe aktarma
- İçe aktarma önizlemesi, düzenleme ve seçim
- Basit duplicate kontrolü
- SM-2 benzeri spaced repetition algoritması
- Bugün zamanı gelen kartları çalışma
- Öğrenme paneli, kart istatistikleri ve grafik
- Açık/koyu tema
- Mobil uyumlu Tailwind CSS arayüzü

## Kurulum

```bash
npm install
cp .env.example .env
npm run dev
```

`.env` dosyasını Firebase Console > Project settings > Web app config bilgileriyle doldurun.

## Firebase

1. Firebase Console'da proje oluşturun.
2. Authentication > Sign-in method bölümünden Email/Password sağlayıcısını açın.
3. Firestore Database oluşturun.
4. `firestore.rules` dosyasındaki kuralları yayınlayın.
5. Hosting için:

```bash
npm run build
firebase deploy
```

## Firestore index önerileri

Aşağıdaki sorgular için Firestore gerekirse otomatik index linki verecektir:

- `cards`: `userId ASC`, `isDeleted ASC`, `createdAt DESC`
- `cards`: `userId ASC`, `isDeleted ASC`, `dueDate ASC`
- `cards`: `userId ASC`, `isDeleted ASC`, `deckId ASC`, `dueDate ASC`
- `decks`: `userId ASC`, `createdAt DESC`

## NotebookLM içe aktarma formatları

### CSV

```csv
front,back,explanation,example,tags
"StatefulWidget nedir?","Durumu değişebilen widgettır.","Kullanıcı etkileşimine göre arayüz değişebilir.","Sayaç uygulaması","Flutter,Widget"
```

### JSON

```json
[
  {
    "front": "FutureBuilder nedir?",
    "back": "Future sonucuna göre arayüz oluşturan widgettır.",
    "explanation": "Asenkron veri geldiğinde ekranı günceller.",
    "example": "API'den veri çekme",
    "tags": ["Flutter", "Async"]
  }
]
```

### TXT

```txt
Soru: FutureBuilder nedir?
Cevap: Future sonucuna göre arayüz oluşturan widgettır.
Açıklama: Asenkron veri geldiğinde ekranı günceller.
Örnek: API'den veri çekme
Etiketler: Flutter, Async
```

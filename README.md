# Academic Research MCP Server 🔬📚

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Node.js Version](https://img.shields.io/badge/node-%3E%3D18.0.0-brightgreen.svg)](https://nodejs.org/)
[![MCP Compatible](https://img.shields.io/badge/MCP-Compatible-blue.svg)](https://modelcontextprotocol.io/)

Claude Desktop için **akademik literatür araştırması** yapabilen Model Context Protocol (MCP) server'ı. PubMed, Google Scholar ve Semantic Scholar veritabanlarından en çok atıf alan makaleleri bulur, yazar analizleri yapar ve profesyonel raporlar oluşturur.

## ✨ Özellikler

### 🔍 **Kapsamlı Araştırma**
- **Çoklu Veritabanı Desteği**: Semantic Scholar, PubMed (yakında)
- **Makale Türü Filtreleme**: Sistematik derlemeler, meta-analizler, RCT'ler, klinik çalışmalar
- **Zaman Aralığı**: Son 20 yıldaki yayınları tarama
- **Atıf Bazlı Sıralama**: En etkili makaleleri öncelikle gösterme

### 📊 **Detaylı Analiz ve Raporlama**
- **En Çok Atıf Alan 20 Makale**: Tam bibliografik bilgilerle
- **En Aktif 5 Yazar**: Yayın sayıları ve en etkili çalışmalarıyla
- **APA Formatında Atıflar**: Akademik standartlarda referanslar
- **İstatistiksel Özet**: Trend analizi, dergi dağılımı, atıf metrikleri

### 🎯 **Kullanım Alanları**
- Akademik literatür taraması
- Sistematik derleme hazırlığı
- Meta-analiz ön çalışması
- Araştırma konusu keşfi
- Yazar ve dergi analizi

## 🚀 Hızlı Başlangıç

### Önkoşullar
- [Node.js](https://nodejs.org/) (v18 veya üstü)
- [Claude Desktop](https://claude.ai/desktop)

### Kurulum

1. **Projeyi klonlayın**
```bash
git clone https://github.com/KULLANICI_ADINIZ/academic-research-mcp-server.git
cd academic-research-mcp-server
```

2. **Bağımlılıkları yükleyin**
```bash
npm install
```

3. **Server'ı test edin**
```bash
node academic-server.js
```

4. **Claude Desktop'ı yapılandırın**

Config dosyasını açın:
- **Windows**: `%APPDATA%\Claude\claude_desktop_config.json`
- **macOS**: `~/Library/Application Support/Claude/claude_desktop_config.json`
- **Linux**: `~/.config/Claude/claude_desktop_config.json`

Şu konfigürasyonu ekleyin:
```json
{
  "mcpServers": {
    "academic-research": {
      "command": "node",
      "args": ["/TAM/YOL/academic-research-mcp-server/academic-server.js"]
    }
  }
}
```

5. **Claude Desktop'ı yeniden başlatın**

## 📖 Kullanım

### Temel Araştırma
```
"diabetes treatment" konusunda akademik literatür araştırması yap
```

### Gelişmiş Sorgular
```
"machine learning healthcare" için son 10 yıldaki sistematik derlemeleri bul
```

```
"COVID-19 vaccine effectiveness" konusunda Q1 dergilerdeki yayınları araştır
```

## 📋 Çıktı Örneği

### 1. En Çok Atıf Alan Makaleler Tablosu
| # | Başlık | Yazarlar | Dergi | Yıl | Atıf | DOI |
|---|--------|----------|-------|-----|------|-----|
| 1 | Deep Learning in Medicine | Smith et al. | Nature Medicine | 2023 | 1,245 | 10.1038/... |

### 2. En Aktif Yazarlar Analizi
| Yazar | Yayın Sayısı | Toplam Atıf | En Çok Atıf Alan Yayınlar |
|-------|--------------|-------------|---------------------------|
| Dr. John Smith | 15 | 2,340 | Paper 1 (456 atıf), Paper 2 (234 atıf)... |

### 3. Detaylı İstatistiksel Özet
- Toplam makale: 147
- Ortalama atıf: 89.5
- En aktif dergi: Nature Medicine (12 yayın)
- Trend: 2020-2023 arası %45 artış

## 🔧 Yapılandırma

### API Ayarları
```javascript
// academic-server.js içinde
const config = {
  maxResults: 100,        // Maksimum sonuç sayısı
  yearRange: 20,          // Geriye gidilecek yıl
  timeout: 15000,         // API timeout (ms)
  retryAttempts: 3        // Yeniden deneme sayısı
};
```

### Makale Türü Filtreleri
Server otomatik olarak şu türleri destekler:
- Sistematik derlemeler
- Meta-analizler
- Randomize kontrollü çalışmalar
- Klinik araştırmalar
- Kesitsel çalışmalar
- Olgu serileri
- Guidelines

## 🛠️ Geliştirme

### Yeni Veritabanı Ekleme
```javascript
async function searchPubMed(query, years, maxResults) {
  // PubMed API entegrasyonu
}

async function searchGoogleScholar(query, years, maxResults) {
  // Google Scholar entegrasyonu (SerpAPI ile)
}
```

### Özel Filtreler
```javascript
function filterByJournalRank(articles, minRank) {
  // Q1-Q4 dergi sıralaması filtresi
}
```

## 📊 API Referansı

### `search_academic_literature`

**Parametreler:**
- `query` (string, zorunlu): Araştırma konusu
- `years` (number, opsiyonel): Geriye gidilecek yıl sayısı (varsayılan: 20)
- `max_results` (number, opsiyonel): Maksimum sonuç sayısı (varsayılan: 100)

**Çıktı:**
- En çok atıf alan 20 makale tablosu
- En aktif 5 yazar analizi
- Detaylı istatistiksel özet
- APA formatında atıflar

## 🔄 Güncellemeler ve Versiyonlar

### v1.0.0 (Mevcut)
- ✅ Semantic Scholar API entegrasyonu
- ✅ En çok atıf alan makale listesi
- ✅ Yazar analizi
- ✅ APA formatında atıflar
- ✅ İstatistiksel özet

### v1.1.0 (Planlanıyor)
- 🔄 PubMed API entegrasyonu
- 🔄 Google Scholar desteği
- 🔄 Q1-Q4 dergi filtreleri
- 🔄 Excel export özelliği

### v1.2.0 (Gelecek)
- 🔄 Görselleştirme grafikleri
- 🔄 Atıf ağı analizi
- 🔄 Trend prediksiyon
- 🔄 Multi-language desteği

## 🤝 Katkıda Bulunma

1. Fork yapın
2. Feature branch oluşturun (`git checkout -b feature/yeni-ozellik`)
3. Değişikliklerinizi commit edin (`git commit -am 'Yeni özellik eklendi'`)
4. Branch'i push edin (`git push origin feature/yeni-ozellik`)
5. Pull Request oluşturun

## 🐛 Sorun Giderme

### Yaygın Sorunlar

**Problem**: MCP server görünmüyor
```bash
# Çözüm: Config dosyası kontrolü
cat ~/.config/Claude/claude_desktop_config.json
```

**Problem**: API rate limiting
```bash
# Çözüm: Timeout artırma
# academic-server.js'te timeout değerini yükseltin
```

**Problem**: Boş sonuçlar
```bash
# Çözüm: Sorgu terimlerini İngilizce deneyin
# Örnek: "diyabet tedavisi" yerine "diabetes treatment"
```

### Debug Modu
```bash
NODE_ENV=development node academic-server.js
```

## 📄 Lisans

Bu proje [MIT Lisansı](LICENSE) altında lisanslanmıştır.

## 🙏 Teşekkürler

- [Semantic Scholar](https://www.semanticscholar.org/) - Ücretsiz API desteği
- [Model Context Protocol](https://modelcontextprotocol.io/) - MCP framework
- [Claude Desktop](https://claude.ai/desktop) - Platform desteği

## 📞 İletişim

- GitHub Issues: Teknik sorular ve öneriler
- Email: [your-email@domain.com]
- Twitter: [@your-handle]

---

**⭐ Bu projeyi beğendiyseniz yıldız vermeyi unutmayın!**

> *"Academic research made simple with AI-powered literature discovery"*

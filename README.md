# Academic Research MCP Server - Kurulum ve Kullanım Kılavuzu

## Kurulum Adımları

### 1. Proje Klasörü Oluşturma
```bash
mkdir academic-research-mcp-server
cd academic-research-mcp-server
```

### 2. Dosya Yapısını Oluşturma
```
academic-research-mcp-server/
├── src/
│   └── index.ts
├── package.json
├── tsconfig.json
└── README.md
```

### 3. Bağımlılıkları Yükleme
```bash
npm install
```

### 4. TypeScript Derleme
```bash
npm run build
```

### 5. Claude Desktop Yapılandırması

#### Windows:
`%APPDATA%\Claude\claude_desktop_config.json` dosyasını düzenleyin

#### macOS:
`~/Library/Application Support/Claude/claude_desktop_config.json` dosyasını düzenleyin

#### Linux:
`~/.config/Claude/claude_desktop_config.json` dosyasını düzenleyin

Yapılandırma dosyasına aşağıdaki konfigürasyonu ekleyin:

```json
{
  "mcpServers": {
    "academic-research": {
      "command": "node",
      "args": ["/tam/yol/academic-research-mcp-server/dist/index.js"],
      "env": {
        "NODE_ENV": "production"
      }
    }
  }
}
```

**ÖNEMLİ:** `/tam/yol/` kısmını projenizin gerçek yolu ile değiştirin.

### 6. Claude Desktop'ı Yeniden Başlatma
Claude Desktop uygulamasını kapatıp tekrar açın.

## Kullanım

Claude Desktop'ta MCP server aktif olduktan sonra şu şekilde kullanabilirsiniz:

```
"Diabetes mellitus" konusunda akademik literatür araştırması yap. Son 15 yıldaki yayınları incele.
```

veya

```
search_academic_literature fonksiyonunu kullanarak "artificial intelligence in medicine" konusunda araştırma yap.
```

## Özellikler

### 🔍 **Çoklu Veritabanı Desteği**
- PubMed
- Google Scholar (geliştirilecek)
- Semantic Scholar

### 📊 **Kapsamlı Analiz**
- En çok atıf alan makaleler
- Yazar istatistikleri
- Dergi dağılımı
- Trend analizi

### 📋 **Profesyonel Raporlama**
- APA formatında atıf
- Tablo formatında sonuçlar
- Detaylı özet
- Exportable sonuçlar

### 🎯 **Makale Türü Filtreleme**
- Sistematik derlemeler
- Meta-analizler
- Randomize kontrollü çalışmalar
- Klinik araştırmalar
- Kesitsel çalışmalar
- Olgu serileri
- Guidelines

## API Özellikleri

### search_academic_literature
**Parametreler:**
- `query` (string, zorunlu): Araştırma konusu
- `years` (number, opsiyonel): Geriye gidilecek yıl sayısı (varsayılan: 20)
- `max_results` (number, opsiyonel): Maksimum sonuç sayısı (varsayılan: 20)

**Çıktı:**
- En çok atıf alan makaleler tablosu
- En aktif yazarlar ve yayınları
- Detaylı literatür özeti
- İstatistiksel analizler

## Geliştirme ve Özelleştirme

### Yeni Veritabanı Ekleme
`searchGoogleScholar` fonksiyonunu geliştirerek SerpAPI entegrasyonu yapabilirsiniz:

```typescript
private async searchGoogleScholar(query: string, years: number, maxResults: number): Promise<Article[]> {
  // SerpAPI entegrasyonu
  const serpapi = require('google-search-results-nodejs');
  const search = new serpapi.GoogleScholarSearch();
  
  // Implementation...
}
```

### Makale Türü Filtreleme
PubMed aramasına makale türü filtreleri ekleyebilirsiniz:

```typescript
const searchParams = {
  db: 'pubmed',
  term: `${query} AND ${startYear}:${currentYear}[pdat] AND (systematic review[pt] OR meta analysis[pt] OR randomized controlled trial[pt])`,
  // ...
};
```

### Ek API Entegrasyonları
- CrossRef API (DOI metadata)
- arXiv API (preprint'ler için)
- bioRxiv API (biyoloji preprint'leri)

## Sorun Giderme

### Common Issues

1. **MCP Server Görünmüyor**
   - Claude Desktop config dosyasının doğru yolda olduğundan emin olun
   - JSON formatının geçerli olduğunu kontrol edin
   - Claude Desktop'ı yeniden başlatın

2. **API Rate Limiting**
   - PubMed: saniyede 3 request
   - Semantic Scholar: dakikada 100 request
   - Gerekirse delay ekleyin

3. **Dependency Errors**
   - `npm install` komutunu tekrar çalıştırın
   - Node.js versiyonunun 18+ olduğundan emin olun

### Debug Modu
```bash
NODE_ENV=development npm run dev
```

## Güvenlik ve Etik Kullanım

- API rate limitlerini respekt edin
- Academic fair use kurallarına uyun
- Elde edilen verilerin telif haklarını gözetin
- Kişisel verileri (varsa) koruyun

## Katkıda Bulunma

1. Fork yapın
2. Feature branch oluşturun (`git checkout -b feature/yeni-ozellik`)
3. Commit yapın (`git commit -am 'Yeni özellik eklendi'`)
4. Push yapın (`git push origin feature/yeni-ozellik`)
5. Pull Request oluşturun

## Lisans

MIT License - Detaylar için LICENSE dosyasına bakın.

## İletişim

Sorularınız için GitHub issues kullanın veya email ile iletişime geçin.

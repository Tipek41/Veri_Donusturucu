# Veri Dönüştürücü

Tarayıcıda çalışan, TXT, CSV, TSV ve DAT dosyalarını tablo olarak önizleyip CSV/TSV veya biçimlendirilmiş XLSX olarak indiren tek sayfalık araç.

## Kullanım

1. [Uygulamayı açın](https://tipek41.github.io/Veri_Donusturucu/) veya `index.html` dosyasını tarayıcıda açın.
2. `.txt`, `.csv`, `.tsv` ya da `.dat` dosyanızı alana sürükleyin veya alana tıklayıp seçin.
3. Türkçe karakterler yanlış görünüyorsa **Karakter Kodlaması** seçimini değiştirin. Varsayılan `Windows-1254`; `UTF-8` ve `ISO-8859-9` da desteklenir.
4. İlk 50 veri satırının önizlemesini kontrol edin. **XLSX İndir** veya CSV ayırıcısını seçip **CSV / TSV İndir** düğmesine basın.

> GitHub Pages bağlantısı, depo ayarlarından Pages yayımlandığında çalışır. Yayımlama yapılmadıysa `index.html` dosyasını yerel olarak açın.

## Özellikler

- İlk satırdaki sekme, noktalı virgül ve virgül sayılarına bakarak giriş ayırıcısını seçer.
- İlk satırı sütun başlıkları olarak kullanır. Tırnak içindeki ayırıcıları ve çift tırnak kaçışlarını okur.
- XLSX çıktısında başlık biçimi, otomatik filtre, sabitlenmiş başlık satırı ve sütun genişliği uygular; tarih ve sayıya benzeyen hücreleri dönüştürür.
- CSV/TSV çıktısını UTF-8 BOM ile oluşturur; çıkış ayırıcısı `;`, `,` veya sekme olabilir.
- Dosya işlemleri tarayıcıda yapılır; uygulamada dosya yüklemek için bir sunucu uç noktası bulunmaz. XLSX üretimi için ExcelJS, CDN üzerinden yüklenir ve internet bağlantısı gerektirir.

## Önemli sınırlar

- Giriş ayırıcısı yalnızca ilk satırın ham karakter sayılarına göre tahmin edilir. Karmaşık başlıklarda yanlış seçilebilir.
- İlk satır başlık kabul edilir; başlıksız dosyalarda ilk veri satırı başlık olur. Fazla hücreler atılır, eksik hücreler boş bırakılır; hücrelerin başındaki ve sonundaki boşluklar kırpılır.
- XLSX dönüşümünde başında sıfır bulunan kodlar, uzun kimlikler ve sayıya benzeyen metinler sayı olarak yorumlanabilir. Tarih benzeri metinler de tarih hücresine dönüşebilir. **Böyle alanları içeren dosyaların XLSX çıktısını kullanmadan önce mutlaka kontrol edin.** CSV/TSV çıktısı metin değerlerini korur; ancak kırpılmış boşluklar ve atılmış fazla sütunlar geri getirilemez.
- Önizleme yalnızca ilk 50 veri satırını gösterir. Büyük dosyalarda tarayıcı belleği ve XLSX oluşturma süresi artabilir.

Ayrıntılar için [Teknik notlar](docs/TEKNIK_NOTLAR.md) dosyasına bakın.

## Geliştirme

Derleme veya kurulum gerekmez. `index.html` dosyasını tarayıcıda açın. Uygulama HTML, CSS ve JavaScript içerir; XLSX için [ExcelJS 4.3.0](https://github.com/exceljs/exceljs) CDN betiğini kullanır.

## Lisans

Bu depoya henüz bir lisans eklenmedi. Kullanım ve yeniden dağıtım hakları için depo sahibinin açık lisans tercihine ihtiyaç vardır.

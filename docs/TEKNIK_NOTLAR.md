# Teknik notlar

## İşleme akışı

1. Dosya `FileReader.readAsArrayBuffer` ile okunur; seçilen kodlama `TextDecoder` ile uygulanır. Kodlama değişince aynı bayt dizisi yeniden çözümlenir.
2. İlk satırdaki ham `\t`, `;` ve `,` sayıları karşılaştırılır. Eşitlikte varsayılan ayırıcı sekmedir.
3. Ayrıştırıcı tırnak içindeki ayırıcıları ve satır sonlarını veri olarak tutar; `""` dizisini tek çift tırnağa çevirir. Hücreler `trim()` ile kırpılır.
4. İlk kayıt başlıktır. Sonraki kayıtlar başlık sütun sayısına göre kesilir veya boş hücrelerle tamamlanır. Boş satırlar atlanır.
5. Tablo ilk 50 veri satırıyla çizilir. Dışa aktarım bütün ayrıştırılmış satırları kullanır.

## Dışa aktarım

| Çıktı | Davranış |
| --- | --- |
| XLSX | ExcelJS 4.3.0 ile çalışma kitabı oluşturur. Başlığı biçimler, ilk satırı dondurur, filtre ekler, sütun genişliğini 12–60 arasında sınırlar. `dd.mm.yyyy`, `dd/mm/yyyy`, `dd-mm-yyyy`, ISO tarihleri ve saniyeli tarih-saat biçimlerini tarih; Türkçe/ABD biçimlerine benzeyen hücreleri sayı yapar. |
| CSV/TSV | UTF-8 BOM ekler. Seçilen ayırıcıya, çift tırnağa veya yeni satıra sahip hücreleri tırnaklar; iç tırnakları çiftler. Metin değerlerini yazar. |

İndirilen dosya adı, yüklenen dosya adından türetilen `_aktarilan.xlsx`, `_aktarilan.csv` veya `_aktarilan.tsv` biçimindedir.

## Bilinen sınırlar ve geliştirme adayları

- Ayırıcı tespiti tırnak içindeki karakterleri de sayar ve yalnızca ilk satırı inceler. Kullanıcının giriş ayırıcısını elle seçebilmesi daha güvenilir olur.
- İlk satır her zaman başlık sayılır. Başlıksız dosya seçeneği bulunmaz.
- Sütun sayısı ilk satırla sabittir; sonraki satırlardaki fazla hücreler sessizce atılır.
- `trim()` nedeniyle anlamlı baş/son boşlukları korunmaz.
- XLSX sayı algılama baştaki sıfırları veya uzun kimliklerin hassasiyetini kaybettirebilir. Ayrıca tarih eşleşmelerinde takvim doğrulaması yapılmaz; JavaScript geçersiz tarihleri başka güne taşıyabilir.
- XLSX sütun genişliği her hücreyi dolaşarak hesaplanır. Büyük dosyalar bellek ve işlemciyi zorlayabilir.
- ExcelJS CDN yüklenmezse XLSX indirilemez. CSV/TSV indirimi kütüphaneye bağlı değildir.
- Uygulama giriş dosyasını sunucuya göndermez; dış CDN betiği için ağ isteği yapılır. Hassas veri iş akışında üçüncü taraf betik kullanımını ayrıca değerlendirin.

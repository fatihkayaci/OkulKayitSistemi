# Okul Kayıt Sistemi

Bu repository, TechCareer içerisinde düzenlenen SQL bootcamp bitirme projesi için kodlar ve yedek içeriyor. Bu projede okul kayıt sistemi ele alınmakta; içinde bulunan tablolar ve aralarındaki ilişkiler anlatılmaktadır. Ayrıca veritabanı oluşturma, rastgele veri oluşturma, view, index ve stored procedure'lerin nasıl kullanıldığını açıklamaktadır.

## Proje İçeriği

Proje, aşağıdaki tabloları içermektedir:

### Tablolar ve Sütunları

1. **tbl_okul**
   - `okulID`: Okulun benzersiz kimliği.
   - `okulAdi`: Okulun adı.
   - `okulKonum`: Okulun fiziksel konumu.

2. **tbl_ogretmen**
   - `ogretmenID`: Öğretmenin benzersiz kimliği.
   - `ad`: Öğretmenin adı.
   - `soyad`: Öğretmenin soyadı.
   - `sehir`: Öğretmenin ikamet ettiği şehir.
   - `email`: Öğretmenin e-posta adresi.
   - `bolumID`: Öğretmenin çalıştığı bölümün kimliği.
   - `girisTarih`: Öğretmenin işe giriş tarihi.

3. **tbl_ogrenci**
   - `ogrenciID`: Öğrencinin benzersiz kimliği.
   - `ad`: Öğrencinin adı.
   - `soyad`: Öğrencinin soyadı.
   - `sehir`: Öğrencinin ikamet ettiği şehir.
   - `email`: Öğrencinin e-posta adresi.
   - `bolumID`: Öğrencinin kayıtlı olduğu bölümün kimliği.
   - `danismanID`: Öğrencinin danışmanının kimliği.

4. **tbl_kayit**
   - `kayitID`: Kayıt işleminin benzersiz kimliği.
   - `ogrenciID`: Kayıtlı öğrencinin kimliği.
   - `bolumID`: Kayıtlı olduğu bölümün kimliği.
   - `kayıtTarihi`: Kayıt işleminin tarihi.

5. **tbl_kampus**
   - `kampusID`: Kampüsün benzersiz kimliği.
   - `okulID`: Kampüsün bağlı olduğu okulun kimliği.
   - `kampusKonum`: Kampüsün fiziksel konumu.
   - `kampusAdi`: Kampüsün adı.

6. **tbl_fakulte**
   - `fakulteID`: Fakültenin benzersiz kimliği.
   - `kampusID`: Fakültenin bağlı olduğu kampüsün kimliği.
   - `fakulteAdi`: Fakültenin adı.

7. **tbl_ders_kayit**
   - `dersKayitID`: Ders kaydının benzersiz kimliği.
   - `ogrenciID`: Kayıtlı öğrencinin kimliği.
   - `dersID`: Kaydedilen dersin kimliği.
   - `nott`: Öğrencinin dersten aldığı not.

8. **tbl_ders**
   - `dersID`: Dersin benzersiz kimliği.
   - `bolumID`: Dersin ait olduğu bölümün kimliği.
   - `dersAdi`: Dersin adı.
   - `kredi`: Dersin kredi değeri.

9. **tbl_bolum**
   - `bolumID`: Bölümün benzersiz kimliği.
   - `fakulteID`: Bölümün ait olduğu fakültenin kimliği.
   - `bolumAdi`: Bölümün adı.

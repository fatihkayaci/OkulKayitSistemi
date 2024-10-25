# Okul Kayıt Sistemi

Bu repository, TechCareer içerisinde düzenlenen SQL bootcamp bitirme projesi için kodlar ve yedek içeriyor. Bu projede okul kayıt sistemi ele alınmakta; içinde bulunan tablolar ve aralarındaki ilişkiler anlatılmaktadır. Ayrıca veritabanı oluşturma, rastgele veri oluşturma, view, index ve stored procedure'lerin nasıl kullanıldığını açıklamaktadır.

## Proje İçeriği

Proje, aşağıdaki tabloları içermektedir:

### Tablolar ve Sütunları

- **tbl_okul**
  - okulID: Okulun benzersiz kimliği.
  - okulAdi: Okulun adı.
  - okulKonum: Okulun fiziksel konumu.

- **tbl_ogretmen**
  - ogretmenID: Öğretmenin benzersiz kimliği.
  - ad: Öğretmenin adı.
  - soyad: Öğretmenin soyadı.
  - sehir: Öğretmenin ikamet ettiği şehir.
  - email: Öğretmenin e-posta adresi.
  - bolumID: Öğretmenin çalıştığı bölümün kimliği.
  - girisTarih: Öğretmenin işe giriş tarihi.

- **tbl_ogrenci**
  - ogrenciID: Öğrencinin benzersiz kimliği.
  - ad: Öğrencinin adı.
  - soyad: Öğrencinin soyadı.
  - sehir: Öğrencinin ikamet ettiği şehir.
  - email: Öğrencinin e-posta adresi.
  - bolumID: Öğrencinin kayıtlı olduğu bölümün kimliği.
  - danismanID: Öğrencinin danışmanının kimliği.

- **tbl_kayit**
  - kayitID: Kayıt işleminin benzersiz kimliği.
  - ogrenciID: Kayıtlı öğrencinin kimliği.
  - bolumID: Kayıtlı olduğu bölümün kimliği.
  - kayitTarihi: Kayıt işleminin tarihi.

- **tbl_kampus**
  - kampusID: Kampüsün benzersiz kimliği.
  - okulID: Kampüsün bağlı olduğu okulun kimliği.
  - kampusKonum: Kampüsün fiziksel konumu.
  - kampusAdi: Kampüsün adı.

- **tbl_fakulte**
  - fakulteID: Fakültenin benzersiz kimliği.
  - kampusID: Fakültenin bağlı olduğu kampüsün kimliği.
  - fakulteAdi: Fakültenin adı.

- **tbl_ders_kayit**
  - dersKayitID: Ders kaydının benzersiz kimliği.
  - ogrenciID: Kayıtlı öğrencinin kimliği.
  - dersID: Kaydedilen dersin kimliği.
  - not: Öğrencinin dersten aldığı not.

- **tbl_ders**
  - dersID: Dersin benzersiz kimliği.
  - bolumID: Dersin ait olduğu bölümün kimliği.
  - dersAdi: Dersin adı.
  - kredi: Dersin kredi değeri.

- **tbl_bolum**
  - bolumID: Bölümün benzersiz kimliği.
  - fakulteID: Bölümün ait olduğu fakültenin kimliği.
  - bolumAdi: Bölümün adı.

## Veritabanı Oluşturma

Veritabanını oluşturmak için aşağıdaki SQL komutunu kullanabilirsiniz:

```
CREATE DATABASE OkulSistemi;
```

Veritabanını kullanmak için:

```
USE OkulSistemi;
```

## Tablo Oluşturma

Örnek olarak `tbl_ogrenci` tablosunu oluşturmak için:

```
CREATE TABLE tbl_ogrenci
(
    ogrenciID INT IDENTITY(1,1) PRIMARY KEY,
    ad NVARCHAR(100),
    soyad NVARCHAR(100),
    sehir NVARCHAR(30),
    email NVARCHAR(50),
    bolumID INT,
    danismanID INT,
    FOREIGN KEY (bolumID) REFERENCES tbl_bolum(bolumID),
    FOREIGN KEY (danismanID) REFERENCES tbl_ogretmen(ogretmenID)
);
```

## Rastgele Veri Doldurma

Tablonun içini rastgele doldurmak için aşağıdaki komutları kullanabilirsiniz:

```
DECLARE @i INT = 1;
DECLARE @Ad NVARCHAR(50);
DECLARE @Soyad NVARCHAR(50);
DECLARE @Email NVARCHAR(100);
DECLARE @Sehir NVARCHAR(50);
DECLARE @OgrenciNumarasi NVARCHAR(50);

DECLARE @Isimler TABLE (Ad NVARCHAR(50));
INSERT INTO @Isimler VALUES
('Ahmet'),('Mehmet'),('Ayşe'),('Fatma'),('Ali'),('Veli'),
('Elif'),('Zeynep'),('Hasan'),('Hüseyin'),('Emine'),('Selin');

DECLARE @Soyadlar TABLE (Soyad NVARCHAR(50));
INSERT INTO @Soyadlar VALUES
('Kaya'),('Yılmaz'),('Koşar'),('Çelik'),('Demir'),('Yıldız'),
('Aydın'),('Korkmaz'),('Özdemir'),('Koç'),('Doğan'),('Şahin');

DECLARE @Sehirler TABLE (Sehir NVARCHAR(50));
INSERT INTO @Sehirler VALUES
('İstanbul'),('Ankara'),('Mersin'),('İzmir'),('Van'),
('Diyarbakır'),('Bursa'),('Aydın'),('Balıkesir'),('Eskişehir'),('Adıyaman'),('Konya');

WHILE @i <= 100000
BEGIN
    SELECT TOP 1 @Ad = Ad FROM @Isimler ORDER BY NEWID();
    SELECT TOP 1 @Soyad = Soyad FROM @Soyadlar ORDER BY NEWID();
    
    SET @OgrenciNumarasi = 'OgrenciNo' + CAST(@i AS NVARCHAR(10));
    SET @Email = @OgrenciNumarasi + '@cumhuriyet.edu.com.tr';
    SELECT TOP 1 @Sehir = Sehir FROM @Sehirler ORDER BY NEWID();
    
    INSERT INTO tbl_ogrenci (ad, soyad, email, sehir)
    VALUES (@Ad, @Soyad, @Email, @sehir);

    SET @i = @i + 1;
END;
```

## Index, View ve Stored Procedure Kullanımı

### Index Oluşturma

Index oluşturmak için:

```
CREATE INDEX indx_sehir ON tbl_ogrenci(sehir);
```

Index'i silmek için:

```
DROP INDEX indx_sehir ON tbl_ogrenci;
```

### View Oluşturma

View oluşturmak için:

```
CREATE VIEW istanbulluOgrenciler AS
SELECT * FROM tbl_ogrenci WHERE sehir = 'İstanbul';
```

View'i güncellemek için:

```
ALTER VIEW istanbulluOgrenciler AS
SELECT * FROM tbl_ogrenci WHERE sehir = 'İstanbul';
```

View'i silmek için:

```
DROP VIEW istanbulluOgrenciler;
```

### Stored Procedure Oluşturma

Prosedür oluşturmak için:

```
CREATE PROCEDURE GetKayitlarByDateRange
    @StartDate DATE,
    @EndDate DATE
AS
BEGIN
    SELECT 
        k.kayitID,
        o.ad AS OgrenciAd,
        o.soyad AS OgrenciSoyad,
        b.bolumID,
        b.bolumAdi,
        k.kayitTarihi
    FROM 
        tbl_kayit k
    INNER JOIN 
        tbl_ogrenci o ON k.ogrenciID = o.ogrenciID
    INNER JOIN 
        tbl_bolum b ON k.bolumID = b.bolumID
    WHERE 
        k.kayitTarihi BETWEEN @StartDate AND @EndDate;
END;
```

Prosedürü çağırmak için:

```
EXEC GetKayitlarByDateRange '2024-01-01', '2024-12-31';
```
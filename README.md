Belirli bir kategorideki ürünleri listele:

SELECT * FROM Urunler WHERE KategoriID = 1;

Belirli bir aralıktaki fiyatları getir:

SELECT * FROM Urunler WHERE Fiyat BETWEEN 1000 AND 10000;

Stokta olan ve belirli bir tedarikçiye ait ürünleri getir:

SELECT * FROM Urunler WHERE StokMiktari > 0 AND TedarikciID = 5;

Adı tel ile başlayan ürünleri getir:

SELECT * FROM Urunler WHERE UrunAdi LIKE 'tel%';

MusteriID'si 1 olan müşterinin siparişleri:

SELECT s.SiparisID, s.SiparisTarihi, s.SiparisDurumu, u.UrunAdi, sd.Adet, sd.Fiyat
FROM Siparisler s
INNER JOIN SiparisDetaylari sd ON s.SiparisID = sd.SiparisID
INNER JOIN Urunler u ON sd.UrunID = u.UrunID
WHERE s.MusteriID = 1;

Belirli Bir Tarih Aralığındaki Siparişler:

SELECT * FROM Siparisler
WHERE SiparisTarihi BETWEEN '2022-01-01' AND '2024-12-31';

Kategorilere Göre Toplam Geliri en yüksek olan

SELECT k.KategoriAdi, SUM(sd.Adet * sd.Fiyat) AS ToplamGelir
FROM Kategoriler k
INNER JOIN Urunler u ON k.KategoriID = u.KategoriID
INNER JOIN SiparisDetaylari sd ON u.UrunID = sd.UrunID
GROUP BY k.KategoriAdi
ORDER BY ToplamGelir DESC;

En Çok Satan Ürünleri listele;

SELECT TOP 10 u.UrunAdi, SUM(s.Adet) AS ToplamSatisAdedi
FROM Urunler u
INNER JOIN SiparisDetaylari s ON u.UrunID = s.UrunID
GROUP BY u.UrunAdi
ORDER BY ToplamSatisAdedi DESC;

En yüksek ve en düşük ürün fiyatları bulma;

SELECT MAX(Fiyat) AS EnYuksekFiyat, MIN(Fiyat) AS EnDusukFiyat FROM Urunler;
Her kategorideki ürün sayısını bulma;
SELECT KategoriID, COUNT(*) AS UrunSayisi FROM Urunler GROUP BY KategoriID;

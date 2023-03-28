# SQL Sorgu Alıştırmaları

Bu hafta SQL sorguları üzerine çalışıyorsunuz. Bugünkü alıştırmada sizin için hazırladığımız veritabanında aşağıda istediğimiz sonuçları elde etmenize yarayan SQL sorgularını oluşturacaksınız.

## Proje Kurulumu
Projeyi forklayın ve clonlayın. Tamamladığınızda da pushlayın.

### Kütüphane Bilgi Sistemi

Bu veritabanı, bir okulun kütüphanesinden öğrencilerin aldıkları kitapların bilgisini barındırmaktadır.

#### Tablolar 
`ogrenci` tablosu öğrencilerin listesini tutar.
`islem` tablosu öğrencilerin kütüphaneden aldıkları kitapların bilgilerini tutar
`kitap` tablosu kütüphanedeki kitapların bilgisini tutar
`yazar` tablosu kitapların yazarları bilgisini tutar
`tur` tablosu kitapların türlerini tutar.

Tablo ilişiklerini görmek için [ktphn.png] dosyasına göz atın.

Yazdığınız sorguları buradan test edebilirsiniz: [https://ergineer.com/assets/materials/fkg36so5-kutuphanebilgisistemi-sql/]


##### Görevler
Aşağıda istenilen sonuçlara ulaşabilmek için gerekli SQL sorgularını yazın. 


MIN-MAX, COUNT-AVG-SUM, GROUP BY, JOINS (INNER, OUTER, LEFT, RIGHT
	#ilk 3 soruyu join kullanmadan yazın.
	1) Öğrencinin adını, soyadını ve kitap aldığı tarihleri listeleyin.
	
		select ogrenci.ograd,ogrenci.ogrsoyad,islem.atarih from ogrenci,islem

	
	2) Fıkra ve hikaye türündeki kitapların adını ve türünü listeleyin.
	
		select kitap.kitapadi,tur.turadi from kitap,tur where tur.turno=kitap.turno and tur.turadi in ("Fıkra","Hikaye")
	
	3) 10B veya 10C sınıfındaki öğrencilerin numarasını, adını, soyadını ve okuduğu kitapları listeleyin.
	
		select ograd,ogrsoyad,ogrenci.ogrno, kitapadi from ogrenci,islem,kitap where (sinif= "10B" or "10C") and ogrenci.ogrno=islem.ogrno and kitap.kitapno=islem.kitapno

#join ile yazın

	#join ile yazın
	4) Öğrencinin adını, soyadını ve kitap aldığı tarihleri listeleyin.
	
	SELECT ograd, ogrsoyad, atarih
	FROM Ogrenci
	INNER JOIN islem
	ON ogrenci.ogrno = islem.ogrno
	
	5) Fıkra ve hikaye türündeki kitapların adını ve türünü listeleyin.
	
	SELECT turadi, kitapadi
	FROM tur INNER JOIN kitap
	ON tur.turno = kitap.turno
	AND (tur.turadi = "Fıkra" OR tur.turadi= "Hikaye")
	
	6) 10B veya 10C sınıfındaki öğrencilerin numarasını, adını, soyadını ve okuduğu kitapları, öğrenci adına göre listeleyin.
	
	
	7) Kitap alan öğrencinin adı, soyadı, kitap aldığı tarih listelensin. Kitap almayan öğrencilerinde listede görünsün.
	
		select ogrenci.ograd,ogrenci.ogrsoyad,islem.atarih from ogrenci left join islem on ogrenci.ogrno=islem.ogrno
	
	8) Kitap almayan öğrencileri listeleyin.
	
	select ogrenci.ograd,ogrenci.ogrsoyad,islem.atarih from ogrenci left join islem on ogrenci.ogrno=islem.ogrno where islem.atarih is null

	9) Alınan kitapların kitap numarasını, adını ve kaç defa alındığını kitap numaralarına göre artan sırada listeleyiniz.
	
	

	10) Alınan kitapların kitap numarasını, adını kaç defa alındığını (alınmayan kitapların yanında 0 olsun) listeleyin.

	Select kitapno, COUNT(islemno), kitapadi 
	FROM kitap LEFT JOIN islem 
	ON kitap.kitapno = islem.kitapno 
	GROUP BY kitapadi 
	ORDER BY kitap.kitapno;


	11) Öğrencilerin adı soyadı ve aldıkları kitabın adı listelensin.
	
	SELECT ograd, ogrsoyad, kitapadi
	FROM ogrenci INNER JOIN kitap
	INNER JOIN islem
	ON islem.ogrno = ogrenci.ogrno

	12) Her öğrencinin adı, soyadı, kitabın adı, yazarın adı soyad ve kitabın türünü ve kitabın alındığı tarihi listeleyiniz. Kitap almayan öğrenciler de listede görünsün.
	
	
	13) 10A veya 10B sınıfındaki öğrencilerin adı soyadı ve okuduğu kitap sayısını getirin.
	

	
	14) Tüm kitapların ortalama sayfa sayısını bulunuz.
	#AVG
	
	SELECT AVG(sayfasayisi) AS AvgPageNumber From kitap

	15) Sayfa sayısı ortalama sayfanın üzerindeki kitapları listeleyin.
	
	SELECT kitapadi, sayfasayisi 
	From kitap WHERE sayfasayisi > 
	(Select AVG(sayfasayisi) From kitap)
	
	16) Öğrenci tablosundaki öğrenci sayısını gösterin
	
	Select COUNT(ograd)  From ogrenci

	17) Öğrenci tablosundaki toplam öğrenci sayısını toplam sayı takma(alias kullanımı) adı ile listeleyin.
	
	Select COUNT(ograd) AS "Toplam Sayı" From ogrenci

	18) Öğrenci tablosunda kaç farklı isimde öğrenci olduğunu listeleyiniz.
	
	SELECT COUNT(distinct ograd) from ogrenci

	19) En fazla sayfa sayısı olan kitabın sayfa sayısını listeleyiniz.
	SELECT MAX(sayfasayisi) FROM kitap
	
	20) En fazla sayfası olan kitabın adını ve sayfa sayısını listeleyiniz.
	
	
	21) En az sayfa sayısı olan kitabın sayfa sayısını listeleyiniz.
	
	SELECT min(sayfasayisi) from kitap
	
	22) En az sayfası olan kitabın adını ve sayfa sayısını listeleyiniz.
	Select kitapadi, sayfasayisi From kitap Where sayfasayisi = (Select Min(sayfasayisi) From kitap)
	
	23) Dram türündeki en fazla sayfası olan kitabın sayfa sayısını bulunuz.
	
	
	24) numarası 15 olan öğrencinin okuduğu toplam sayfa sayısını bulunuz.
	
	
	25) İsme göre öğrenci sayılarının adedini bulunuz.(Örn: ali 5 tane, ahmet 8 tane )

	select ograd, count(ograd) from ogrenci group by ograd
	
	26) Her sınıftaki öğrenci sayısını bulunuz.
	
	select sinif, count(*) from ogrenci group by sinif
	
	27) Her sınıftaki erkek ve kız öğrenci sayısını bulunuz.
	
	SELECT COUNT(*),cinsiyet FROM ogrenci group by cinsiyet
	
	28) Her öğrencinin adını, soyadını ve okuduğu toplam sayfa sayısını büyükten küçüğe doğru listeleyiniz.
	
	
	29) Her öğrencinin okuduğu kitap sayısını getiriniz.
# SQL Sorgu Alıştırmaları

Bu hafta SQL sorguları üzerine çalışıyorsunuz. Bugünkü alıştırmada sizin için hazırladığımız veritabanında aşağıda istediğimiz sonuçları elde etmenize yarayan SQL sorgularını oluşturacaksınız.

# Proje Kurulumu
Projeyi forklayın ve clonlayın. Tamamladığınızda da pushlayın.

## Kütüphane Bilgi Sistemi

Bu veritabanı, bir okulun kütüphanesinden öğrencilerin aldıkları kitapların bilgisini barındırmaktadır.

#Tablolar 
`ogrenci` tablosu öğrencilerin listesini tutar.
`islem` tablosu öğrencilerin kütüphaneden aldıkları kitapların bilgilerini tutar
`kitap` tablosu kütüphanedeki kitapların bilgisini tutar
`yazar` tablosu kitapların yazarları bilgisini tutar
`tur` tablosu kitapların türlerini tutar.

Tablo ilişiklerini görmek için [ktphn.png] dosyasına göz atın.

Yazdığınız sorguları buradan test edebilirsiniz: [https://ergineer.com/assets/materials/fkg36so5-kutuphanebilgisistemi-sql/]



# Görevler
Aşağıda istenilen sonuçlara ulaşabilmek için gerekli SQL sorgularını yazın. 



	1) ÖRNEK SORU: Yazar tablosunu KEMAL UYUMAZ isimli yazarı ekleyin.
	
        INSERT INTO yazar (yazarno, yazarad, yazarsoyad) VALUES ('128', 'Kemal' , 'Uymaz')
      
	
	2) Biyografi türünü tür tablosuna ekleyiniz.
	 
	    INSERT INTO tur (turno, turadi) VALUES (77, 'Biyografi')
	    
	
	3) 10A sınıfı olan ÇAĞLAR ÜZÜMCÜ isimli erkek, sınıfı 9B olan LEYLA ALAGÖZ isimli kız ve sınıfı 11C olan Ayşe Bektaş isimli kız öğrencileri tek sorguda ekleyin. 
	 
	    INSERT INTO ogrenci (ograd, ogrsoyad, sinif)
		VALUES 
		( 'Çağlar' , 'Üzümcü', '10A'),
		( 'Leyla' , 'Alagöz', '9B'),
		( 'Ayşe' , 'Bektaş', '11C')
	
	4) Öğrenci tablosundaki rastgele bir öğrenciyi yazarlar tablosuna yazar olarak ekleyiniz.
	
	    INSERT INTO yazar (yazarno, yazarad, yazarsoyad)
		SELECT ogrno, ograd, ogrsoyad
		FROM ogrenci
		ORDER BY RAND()
        LIMIT 1
	
	5) Öğrenci numarası 10 ile 30 arasındaki öğrencileri yazar olarak ekleyiniz.
	    
		INSERT INTO yazar (yazarno, yazarad, yazarsoyad)
		SELECT ogrno, ograd, ogrsoyad
		FROM ogrenci
		WHERE ogrno BETWEEN 10 AND 30
	
	6) Nurettin Belek isimli yazarı ekleyip yazar numarasını yazdırınız.
	(Not: Otomatik arttırmada son arttırılan değer @@IDENTITY değişkeni içinde tutulur.)
	
	
	7) 10B sınıfındaki öğrenci numarası 3 olan öğrenciyi 10C sınıfına geçirin.
	
	
	8) 9A sınıfındaki tüm öğrencileri 10A sınıfına aktarın
	  
	    UPDATE ogrenci SET sinif ='10A' WHERE sinif = '9A';
	
	9) Tüm öğrencilerin puanını 5 puan arttırın.
	 
	    UPDATE ogrenci SET puan=puan+5 
	
	10) 25 numaralı yazarı silin.

        DELETE FROM yazar where yazarno=25

	11) Doğum tarihi null olan öğrencileri listeleyin. (insert sorgusu ile girilen 3 öğrenci listelenecektir)
	 
	    SELECT dtarih FROM ogrenci WHERE dtarih='null'
	
	12) Doğum tarihi null olan öğrencileri silin. 
	
	    DELETE FROM ogrenci WHERE dtarih='null'
	
	13) Kitap tablosunda adı a ile başlayan kitapların puanlarını 2 artırın.
	 
	    UPDATE kitap SET puan=puan+2 WHERE kitapadi LIKE 'A&'
	
	14) Kişisel Gelişim isimli bir tür oluşturun.
	
	    INSERT INTO tur (turadi) VALUES ('kişisel gelişim')
	
	15) Kitap tablosundaki Başarı Rehberi kitabının türünü bu tür ile değiştirin.
	
	    
	
	16) Öğrenci tablosunu kontrol etmek amaçlı tüm öğrencileri görüntüleyen "ogrencilistesi" adında bir prosedür oluşturun.
	
	    CREATE PROCEDURE ogrencilistesi()
		LANGUAGE 'sql'
        AS $BODY$
        BEGIN 
        SELECT * FROM ogrenci 
        $BODY$
	 
	17) Öğrenci tablosuna yeni öğrenci eklemek için "ekle" adında bir prosedür oluşturun.
	
	    CREATE PROCEDURE ekle()
		LANGUAGE 'sql'
		AS $BODY$
	    INSERT INTO ogrenci (ograd, ogrsoyad, sinif)
		VALUES ('abc', 'def', 10C)
		$BODY$

	
	18) Öğrenci noya göre öğrenci silebilmeyi sağlayan "sil" adında bir prosedür oluşturun.
	
	
	19) Öğrenci numarasını kullanarak kolay bir biçimde öğrencinin sınıfını değiştirebileceğimiz bir prosedür oluşturun.
	
	
	20) Öğrenci adı ve soyadını "Ad Soyad" olarak birleştirip, ad soyada göre kolayca arama yapmayı sağlayan bir prosedür yazın.
	
	
	21) Daha önceden oluşturduğunu tüm prosedürleri silin.
	
	
	#Esnek görevler (Esnek görevlerin hepsini Select in Select ile gerçekleştirmeniz beklenmektedir.)
	22) Select in select yöntemiyle dram türündeki kitapları listeleyiniz.
	
	
	23) Adı e harfi ile başlayan yazarların kitaplarını listeleyin.
	
	
	24) Kitap okumayan öğrencileri listeleyiniz.
	
	
	25) Okunmayan kitapları listeleyiniz

	
	26) Mayıs ayında okunmayan kitapları listeleyiniz.

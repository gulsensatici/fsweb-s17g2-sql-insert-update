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
	
      insert into yazar(yazarad, yazarsoyad) values ( "kemal", "uymaz")
	
	2) Biyografi türünü tür tablosuna ekleyiniz.
	 
	  insert into tur(turadi) values ('biyografi');

	3) 10A sınıfı olan ÇAĞLAR ÜZÜMCÜ isimli erkek, sınıfı 9B olan LEYLA ALAGÖZ isimli kız ve sınıfı 11C olan Ayşe Bektaş isimli kız öğrencileri tek sorguda ekleyin. 
	 
	  insert into ogrenci(sinif, cinsiyet, ograd, ogrsoyad) values('10A', 'E','ÇAĞLAR', 'ÜZÜMCÜ'),('9B' ,'K' ,'LEYLA', 'ALAGÖZ'), ('11C','K','AYŞE','BEKTAŞ');
	 
	4) Öğrenci tablosundaki rastgele bir öğrenciyi yazarlar tablosuna yazar olarak ekleyiniz.
	
	   insert into yazar(yazarad, yazarsoyad) select ograd, ogrsoyad from ogrenci order by rand() limit 1;

	
	5) Öğrenci numarası 10 ile 30 arasındaki öğrencileri yazar olarak ekleyiniz.
	    
		insert into yazar(yazarad,yyazarsoyad) select ograd,ogrsoyad from ogrenci where ogrno>=10 and ogrno<=30;
	
	
	6) Nurettin Belek isimli yazarı ekleyip yazar numarasını yazdırınız.
	(Not: Otomatik arttırmada son arttırılan değer @@IDENTITY değişkeni içinde tutulur.)
	   
	    insert into yazar(yazarad,yazarsoyad) values( 'nurettin', 'belek');
		SELECT @@IDENTITY;
	
	7) 10B sınıfındaki öğrenci numarası 3 olan öğrenciyi 10C sınıfına geçirin.

	    UPDATE ogrenci SET sinif='10C' WHERE  ogrno='3'
	
	
	8) 9A sınıfındaki tüm öğrencileri 10A sınıfına aktarın
	  
	    UPDATE ogrenci SET sinif='10A' WHERE sinif='9A'
	
	9) Tüm öğrencilerin puanını 5 puan arttırın.
	 
	   UPDATE ogrenci SET puan=puan+5 
	
	10) 25 numaralı yazarı silin.

       DELETE FFROM yazar where yazarno='25'

	11) Doğum tarihi null olan öğrencileri listeleyin. (insert sorgusu ile girilen 3 öğrenci listelenecektir)
	  
	  select * from ogrenci where dtarih is null
	    
	
	12) Doğum tarihi null olan öğrencileri silin. 
	
	  DELETE FROM ogrenci WHERE dtarih IS null
	
	13) Kitap tablosunda adı a ile başlayan kitapların puanlarını 2 artırın.
	 
	  UPDATE kitap SET puan=puan+2 WHERE kitapadi LIKE 'A%'
	
	14) Kişisel Gelişim isimli bir tür oluşturun.
	
	  INSERT INTO tur(turadi) VALUES ('kişisel gelişim')
	
	15) Kitap tablosundaki Başarı Rehberi kitabının türünü bu tür ile değiştirin.
	
	    UPDATE kitap SET turno=(SELECT turno FROM tur where turadi='kişisel gelişim') WHERE kitapadi='Başarı rehberi';
	
	16) Öğrenci tablosunu kontrol etmek amaçlı tüm öğrencileri görüntüleyen "ogrencilistesi" adında bir prosedür oluşturun.
	
	    CREATE PROCEDURE ogrencilistesi()
		LANGUAGE 'sql'
		AS $BODY$
          select * from ogrenci
		$BODY$

	 
	17) Öğrenci tablosuna yeni öğrenci eklemek için "ekle" adında bir prosedür oluşturun.
	    
		CREATE PROCEDURE ekle(no smallint,name character varying,lastname character varying,gender character varying, birthdate int ,class character varying,point smallint )
		LANGUAGE 'sql'
		AS $BODY$
          INSER INTO ogrenci(ogrno,ograd,ogrsoyad,cinsiyet,dtraih,sinif,puan) VALUES(no,name,lastname,gender,birthday,class,point)
		$BODY$

	
	18) Öğrenci noya göre öğrenci silebilmeyi sağlayan "sil" adında bir prosedür oluşturun.
	
	    CREATE PROCEDURE sil(no smallint)
		LANGUAGE 'sql'
		AS $BODY$
            DELETE FROM ogrenci(ogrno) where ogrno=no
		$BODY$
	
	19) Öğrenci numarasını kullanarak kolay bir biçimde öğrencinin sınıfını değiştirebileceğimiz bir prosedür oluşturun.
	
	    CREATE PROCEDURE ogrsınıf(no smallint,class character varying)
		LANGUAGE 'sql'
		AS $BODY$
          UPDATE ogrenci(ogrno) SET sinif=class WHERE no=ogrno 
		$BODY$
	
	20) Öğrenci adı ve soyadını "Ad Soyad" olarak birleştirip, ad soyada göre kolayca arama yapmayı sağlayan bir prosedür yazın.
	
	    
	    CREATE PROCEDURE ogrname(no smallint, name character varying, surname character varying)
		LANGUAGE 'sql'
		AS $BODY$
          SELECT CONCAT (name,' ', surnmae) AS 'ad soyad' FROM ogrenci where ograd=name AND ogrsoyad=surname 
		$BODY$
	
	21) Daha önceden oluşturduğunu tüm prosedürleri silin.
	  
	    DROP PROCEDURE
	
	#Esnek görevler (Esnek görevlerin hepsini Select in Select ile gerçekleştirmeniz beklenmektedir.)
	22) Select in select yöntemiyle dram türündeki kitapları listeleyiniz.
	
	    SELECT * FROM kitap where turno IN (SELECT turno FROM tur where turadi=DRAM);

	23) Adı e harfi ile başlayan yazarların kitaplarını listeleyin.
	
	    SELECT * FROM kitap WHERE yazarno IN(SELECT yazarno FROM yazar WHERE yazarad LIKE 'E%')
	    
	24) Kitap okumayan öğrencileri listeleyiniz.
	  
	    SELECT * FROM ogrenci WHERE ogrno NOT IN(SELECT ogrno FROM islem)
	
	25) Okunmayan kitapları listeleyiniz
 
        SELECT * FROM kitap WHERE kitapno NOT IN( SELECT kitapno FROM islem)
	
	26) Mayıs ayında okunmayan kitapları listeleyiniz.

	   SELECT * FROM kitap WHERE kitapno IN(SELECT kitapno FROM islem WHERE atarih NOT LIKE'%-05-%')

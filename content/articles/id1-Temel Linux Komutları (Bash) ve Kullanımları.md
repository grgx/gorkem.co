---
date: 2020-01-14T18:00:00+03:00
lastmod: 2020-02-22T18:53:00+03:00
title: "Temel Linux Komutları (Bash) ve Kullanımları"
authors: ["grkmgry"]
cover: 
  image: /images/bash.webp
  style: normal
  
categories:

tags:
  - bash
  - bash komut
  - linux
  - linux komut
  - piping
  - shell
  - stdin
  - stdout
slug: temel-linux-komutlari-bash-ve-kullanimlari
toc: true
---

Günümüzde hitap ettiği alana bağlı olarak, karşımıza farklı işletim sistemleri çıkmaktadır. Windows, macOS, Linux dağıtımları vs. Maalesef ki birini çok iyi biliyor oluşumuz, diğerlerini pek de etkilemiyor. Bu yüzden eğer bir VPS (Virtual Private Server) yönetiyorsanız veya bilgisayarınızda bir Linux dağıtımı yüklü ise temel derecede linux komutları bilmelisiniz.

## Linux’un Temel Birimi : “Shell”

Shell (terminal, konsol veya komut satırı olarak da bilinir), komutların makineye gönderildiği metin tabanlı bir kullanıcı arabirimidir. Linux’ta Shell’in varsayılan dili  **bash**  olarak adlandırılır. Pencerelerin içine tıklayıp duran Windows kullanıcılarının aksine, Linux geliştiricileri klavyelerine yapışır ve komutları shell içine yazarlar. Bu durum, programlama geçmişine sahip olmayanlar için ilk başlarda biraz zor gibi dursa da, ileriye dönük iyi bir alıştırma olacak.

## Linux Komutları İçin Önemli Birkaç Kavramın Öğrenilmesi

Bir programlama dili ile karşılaştırıldığında, bash’ın öğrenilmesi gereken birkaç önemli kavramı vardır. Bunlar ele alındığında, bash’ın geri kalan kısmı ezberdir. Açık konuşmak için yeniden yazacağım: bash’da iyi olmak, yaklaşık 20 – 30 komut ve en yaygın argümanlarını ezberlemektir. Daha karmaşık şeyler için Google danışmaya devam yani.

### Linux Komutları Sözdizimi

Komutlar büyük-küçük harf duyarlıdır, ve genel yapısı şu şekildedir: {komut} {argümanlar}

Örneğin `grep -inr` sözdiziminde, _grep_ bir komut, _-inr_ ise bu komutun aldığı argümandır. (grep komutu, metin içinde bir ifade aramak için kullanılır.) Komutların aldığı argümanları ezberlemek hem külfet hem de gereksiz bir eylem. Bunun yerine Google’da  _“man grep”_  olarak bir arama yaparsanız tüm argümanlara rahatlıkla ulaşabilirsiniz.

### Dizin Takma Adları

-   Mevcut dizin (yani ben neredeyim) : . (bir nokta)
-   Mevcut dizinin üst dizini : .. (iki nokta)
-   Kullanıcının ev dizini : ~
-   Dosya sistemi kökü (root) : /

Örneğin, geçerli dizinden bir üst dizine geçmek için şu komut kullanılır : `cd ..` Benzer şekilde, “path/to/file.txt” dizininde bulunan bir dosyayı mevcut dizine kopyalamak için `cp /path/to/file.txt .` (komutun sonundaki noktaya dikkat edin) kullanılır.

## STDIN/STDOUT

Terminale yazdığınız ve ENTER ile gönderdiğiniz herhangi bir şey standart girdi (STDIN) olarak adlandırılır.

Bir programın terminale yazdırdığı herhangi bir şey (örneğin, bir dosyanın içinden metin) standart çıktı (STDOUT) olarak adlandırılır.

### Piping

#### 1. |

Pipe öncesinde kullandığınız komutun veya işlemin sonucunu, sonrasındaki komuta aktarır. Yani pipe’ın solundakilerin STDOUT olarak alır ve sağındakine STDIN olarak aktarır.Örnek olarak;

“echo” komutu ekrana yazı yazdırmak için kullanılır. “wc -w” komutu ise kelime sayısını verir.

Şimdi bu iki komutu ile birleştirelim `echo 'text text' | wc -w`

Çıktı : `2` olacak. Çünkü ekrandaki kelime sayısını saymış olduk.

#### 2. >

Büyüktür işareti, sol tarafındaki komutun STDOUT’unu alır, sağdaki yeni dosyaya veya  **mevcut dosyanın üzerine**  yazar. Örnek olarak;

ls -l komutu bulunan dizindeki dosyaları listeler. `ls -l > tmp.txt` komutu ise dizinde bulunan dosyaların isimlerini tmp.txt dosyasına yazar.

#### 3. »

İki tane büyüktür işareti ise 2 numaradaki kullanıma benzer olarak, sol tarafındaki komutun STDOUT’unu alır ve sağdaki mevcut  **dosyaya ekler**  veya yeni dosyaya yazar.

date komutu o andaki tarih ve saati veririr. `date >> tmp.txt` komutu ise tarih ve saati tmp.txt dosyasına ekler.

### Joker Karakter (Wildcard)

Bir klasörde “.json” ile biten tüm dosyaları listelemek için `ls *.json` komutu kullanılır.

## Otomatik Tamamlama

Bash’da, bir komut yazmaya başlayın ve SEKME (Tab) tuşuna basın. Komutun sizin için akıllıca tamamlandığını göreceksiniz.

Açıkçası tüm komut ve parametleri hatırlamak zordur. Komutların tamamını yazmak yerine bu tip işlevleri kullanmalısınız.

## Çıkış

Bazen bir program içersinde sıkışıp kalabilir ve dışarı çıkamayabilirsiniz. Bu durum Linux’e yebi başlayanlar için sık karşılaşılan ve moral bozucu bir durum olabilir. Aşağıda bazı ortamlardan çıkış yollarını listeledim.

### **Bash**

-   CTRL+c
-   q
-   exit

### **Python**

-   quit()
-   CTRL+d

### **Nano**

CTRL+x

### **Vim**

:q!

## Temel Linux Komutları

### Sık Kullanılan Linux Komutları

Çoğunlukla kullanılan bash komutları aşağıda verilmiştir. Daha önce de belirtildiği gibi, bir avuç komutu bilmek gerçekleştirmek istediğiniz işlerin çoğu için yeterlidir.

-   **cd {dizin} :** Dizini değiştirir.
-   **ls -lha :** Gizli dosyalar da dahil, dizindeki dosyaları listeler.
-   **nano veya vim :** Terminal de kullanılabilen metin editörü.
-   **touch {file} :** Boş dosya açar.
-   **cp -R {orjinal isim} {yeni isim} :** Bir dosyayı başka bir yere kopyalar.
-   **mv {orjinal isim} {yeni isim} :** Dosya taşıma veya yeniden adalandırma için kullanılır.
-   **rm {dosya} :** dosyayı siler.
-   **rm -rf {dosya/dizin} :** Dosyayı veya dizini kalıcı olarak siler.
-   **pwd :** Bulunulan dizini gösterir.
-   **cat, less, tail, head :** bir dosyanın içeriğini STDOUT olarask verir.
-   **mkdir {dizin} :** Boş bir dizin oluşturur.
-   **grep -inr {ifade} :** Bir dizinde bulunan herhangi bir dosyada istenen “ifade” yi arar.
-   **column -s,-t {dosya} :** Virgülle ayrılmış bir dosyayı sütunlar halinde gösterir.
-   **ssh {kullanıcıadı@hostname} :** Uzak bir makineye bağlanır.
-   **top (yada htop) :** Görev yöneticisi.
-   **sed -i “s/{bul}/{değiştir}/g” {dosya} :** Belirtilen dosya içerindeki ifadeyi istenilen ile değiştirir.
-   **tmux new -s session, tmux attach -t session :** Yeni pencere açmadan, yeni bir terminal oturumu başlatır.
-   **wget {link} :** Bir web kaynağını indirmeyi sağlar.
-   **find {dizin} :** bir dizinin dosyalarını ve alt dizinlerini listeler.

### Gelişmiş ve Az Kullanılan Linux Komutları

Bazı durumlarda kullanılan bu komutları da yakın yerlerde tutmakta fayda var.

-   **netstat | head -n20 :** açık olan internet/UNIX soketlerini listeler.
-   **nslookup {ip adresi} :** ip adresine ait hostname’i bulur.
-   **ps aux | head -n20 :** aktif işlemleri gösterir.
-   **file {d_osya} :** Dosya tipinin ne olduğunu döndürür. (ASCII-text, binary, vs.)
-   **uname -a :** Kernel bilgisini gösterir.
-   **lsb_release -a :** İşletim Sistemi bilgisini gösterir.
-   **hostname :** Makinenizin hostname’ini gösterir.
-   **pstree :** Göreselleştirilmiş işlemler listesi.
-   **time {komut} :** komutun ne kadar sürede icra edildiğini gösterir.
-   **wc -l {dosya} :** dosyadaki satırları sayar.
-   **zcat {dosya.gz} :** ziplenmiş dosyanın içeriğini gösterir.

> ### Açıklama ###
> 
> Bu yazı ilk olarak 18 Temmuz 2018 tarihinde 
> [Medium’da](https://medium.com/@grkmgry/temel-linux-bash-komutlar%C4%B1-ve-kullan%C4%B1mlar%C4%B1-55636f634606)
> yayınlanmıştır.   Maalesef ki o tarihte yayınlanırken çeviri yapılan
> kaynak gösterilmemiştir. Kaynak bulunabilirse yazıya eklenecektir.



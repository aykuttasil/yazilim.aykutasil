+++
autoThumbnailImage = false
categories = ["yazilim", "test"]
coverImage = "https://c8.staticflickr.com/8/7421/9339731831_9ba94f287c_k.jpg"
date = "2017-01-11T00:27:54+03:00"
desciption = ""
keywords = ["yazilim", "sofware", "unit test"]
metaAlignment = "center"
tags = ["software", "unit test"]
thumbnailImage = ""
thumbnailImagePosition = "top"
title = "Unit Test Nedir ? Niçin ve Nasıl Yapılır ?"
url = "unittest-nedir"

+++

**Unit Test Nedir ? Niçin ve Nasıl Yapılır ?**

Yıl olmuş 2014 hala birim test makalesi mi yazıyorsun diye düşünüyor olabilirsiniz. Ancak, birim testi uzun zamandır kullanılan bir yöntem olmasına rağmen tam olarak ne işe yaradığı, neden yapıldığı ve nasıl yapılması gerektiği konusunda açıklayıcı bir Türkçe yazı bulmak malesef zor. Bu yüzden, yazılım mühendisi adaylarına ve kariyerine yeni başlayan arkadaşlara faydalı olabilmek adına bu yazıyı yazmak uygun olur diye düşündüm.

**Birim Testi Nedir?**

Birim testi adından anlaşıldığı üzere yazılım birimlerinin test edilmesidir. Burada yazılım birimi dediğimiz şey ise test edilebilen en küçük yazılım bileşenidir. Nesneye yönelik programlama yaklaşımını ele alacak olursak, yazılım birimleri sınıflardır diyebiliriz. Yapılan şey basit olarak sınıf davranışlarının (metodlar) belirli girdiler sağlandığı zaman doğru bir şekilde çalışıp, istediğimiz sonucu üretip üretmediğini kontrol etmektir. Bu şekilde yazılımın küçük birimleri test edildiği zaman, bütünü oluşturan parçaların en azından kendi içlerinde çalıştığından emin olmuş oluruz. Buraya kadar söylediklerimiz birim testinin genel tanımıdır, ama yazılım geliştiren kişiler olarak asıl anlamamız gereken şey birim testini niçin yaptığımızdır.

**Birim Test Niçin Yapılır?**

Bu soruyu eminim ki birçok yazılımcı kendi kendine sormuştur. Bir kısmımız tam olarak neye hizmet ettiğini anlamasak da, faydalı olduğunu düşündüğümüz için ve kendimizi daha güvende hissetmek adına birim test yazarız. Bazılarımız ise birim test yazmanın faydalı olduğunu bilmemize rağmen çeşitli bahaneler üreterek birim test yazmaktan kaçarız. Bunun arkasındaki asıl sebep ise birim testlerin ve test odaklı yazılım geliştirme tekniğinin (test-driven development) asıl amacını kavrayamamış olmamızdır. Her şeyden önce şunu söylemek gerekir: Birim testleri yazılımları test etmek için yazılmaz. İsmi “birim test” olan bir yöntem için “asıl amacı yazılımları test etmek değildir” demek ilk başta çok mantıklı gelmeyebilir ama yazıyı okudukça bana hak vereceğinizi düşünüyorum.

**Birim testler hata bulmak için değildir**

Bir yazılım sistemindeki hataları (bug) bulmak birim testler ile mümkün değildir. Çünkü birim testlerin yaptığı iş yazılımın en küçük parçalarını kendi içerisinde test etmektir. Peki bu küçük parçaların kendi içlerinde çalışıyor olması, yazılımın gerçek kullanıcılar tarafından kullanılmaya başladığı zaman bir bütün olarak çalışacağını gösterir mi? Kesinlikle hayır. Bir yazılım sistemi, onu oluşturan parçaların toplamından çok daha fazlasıdır. Dolayısıyla bu bütünü test etmek için farklı yöntemler kullanmak gerekir. İşlevsel test (functional testing), bütünleştirme testi (integration testing) bunlara örnek verilebilir ancak konumuz birim test olduğu için bunlara değinmeyeceğim.

**Hataları bulamıyorsa birim testler ne işe yarıyor?**

Birim test yazmanın sağladığı gerçek fayda, bizi kaliteli kod yazmaya teşvik etmesidir. Peki bu nasıl olur? Öncelikle şunu söylemek gerekir ki, birim test yazmanın birinci kuralı test etmekte olduğumuz sınıfı, bağımlı olduğu diğer bütün bileşenlerden izole etmektir. Örnek verecek olursak, test ettiğiniz sınıfın bir Google servisine bağlanarak veri çektiğini düşünün. Ancak birim test esnasında bu sınıfın Google servisine bağlanıp veri çekmesini istemeyiz. Çünkü birim testin amacı yazılımın Google servisleriyle çalışabildiğini kanıtlamak değildir. Birim test yazarken, bağlantılı olduğumuz diğer bütün parçaların sorunsuz biçimde çalıştığını varsayarak yazarız, çünkü odaklandığımız şey sınıfın kendisidir, bağımlı olduğu diğer bileşenler değil. Bu varsayımı yapabilmek için de, mocking dediğimiz tekniği kullanarak test esnasında gerçek Google servisine bağlanmak yerine bizim yarattığımız sahte bir servise (mock object) bağlanıp sınıfın ihtiyacı olan veriyi döndürürüz.  Bu şekilde test ettiğimiz sınıf dışarıda bir servise bağlanmadan ihtiyacı olan veriyi alır ve işletimini tamamlar.

Şimdi test etmekte olduğumuz bu sınıfın dışarıdaki Google servisiyle sıkı sıkıya bağlı (tightly coupled) olduğunu düşünün. Sınıf Google servisiyle ilgili bütün bilgileri içinde barındırıyor ve bağlantıyı yaratıp kullanıyor, veri alışverişini yapıyor. Biz bu sınıfa gerçek Google servisine değil de bizim belirlediğimiz sahte servise (mock object) bağlanmasını nasıl söyleyeceğiz? Bu şekilde birbirine sıkıca bağlanmış yazılım bileşenlerini birbirlerinden bağımsız bir şekilde test etmek mümkün değildir. Ancak bu bileşenler gevşek bağlı (loosely coupled) olsaydı, biz sınıfımıza test esnasında sahte servisi, gerçek işletim esnasında ise Google servisini kullanmasını söyleyebilirdik. Bu şekilde yazılım bileşenlerini birbirlerine gevşek bir biçimde bağlamak Dependency Injection tekniğiyle mümkündür ve gevşek bağlı sistemler çok daha kolay bakım yapılabilen, test edilebilen ve eklemeler yapması çok daha kolay olan sistemlerdir.

Test odaklı yazılım geliştirme yapıyorsak (test-driven development), birim testleri sınıfın kendisinden önce yazmamız gerektiği için bu tarz tasarım detaylarını henüz işin başındayken doğru bir şekilde belirlemiş oluruz. Doğru biçimde birim test yazmak, yazılım bileşenlerini birbirlerine sıkı sıkıya bağlamamızı engelleyerek daha tasarım aşamasındayken daha kaliteli bir yazılım çıkarmamıza yardımcı olur. Özet olarak şunu söylemekte fayda var, bütün bileşenleri birbirinden bağımsız olarak test edilebilen yazılımlar, bakımı nispeten daha kolay olan ve kaliteli yazılımlardır. İşe birim testleri yazarak başlamak da bunu başarmamıza yardımcı olur.

**Birim test yazmak kodda iyileştirme yapmayı (refactoring) kolaylaştırır**

Birim test yazmanın bir diğer büyük faydası da kodda iyileştirme yaparken (refactoring) ortaya çıkar. Hiçbir kod mükemmel değildir ve iyileştirme her zaman bir ihtiyaçtır. Ancak birçok yazılımcı çalışan sistemi bozmaktan korktuğu için iyileştirme yapmaz. Ancak kapsamlı birim testleriniz varsa, değişiklik yaptığınız sınıfın hala çalışıp çalışmadığını anlamak için birim testlerinizi kullanabilirsiniz. Daha önce birim testlerin hataları bulmak için kullanılmadığını söylemiş olsak da iyileştirme esnasında üzerinde çalıştığımız sınıfı bozup bozmadığımızı anlamak mümkün olabilir. Dolayısıyla birim test yazmak sadece kodu yazarken kaliteli yazmaya teşvik etmekle kalmaz, aynı zamanda ileride kodu iyileştirmemize de yardımcı olur.

**Doğru birim test nasıl yazılır?**

Birim testin nasıl yazılması gerektiği de çok önemlidir. Doğru yazılmayan birim testler bize hiçbir şey kazandırmayacağı gibi en ufak değişiklikte hatalar vermeye başlayıp başımızı ağrıtırlar. Üstüne bir de testlere bakım yapmakla uğraşmak zorunda kalacağımız için de fayda sağlamanın aksine zararlı olabilirler. O yüzden birim test yazarken aşağıdaki noktalara dikkat etmekte fayda var:

Tek bir şeye odaklanın: Her testin tek bir şeyi test ettiğinden emin olun. Çok gerekli değilse aynı test içerisine birden fazla assert ifadesi koymayın.
Bağımlılıkları (dependency) değil, tek bir sınıfı test edin: Yazıda daha önce de değindiğimiz gibi, bir sınıfı test ederken o sınıfı bağımlı olduğu diğer yazılım bileşenlerinden izole edin, aksi taktirde yazdığınız test birim test değildir.
Yazdığınız testler birbirini etkilemesin: Yazdığınız her test birbirinden bağımsız bir şekilde tek başına sorunsuz çalışabilmelidir. Eğer yazdığınız bir birim test başka bir birim testin üreteceği veriye bağımlıysa yanlış yapıyorsunuz demektir.
Testlerinizi doğru isimlendirin: Test sayısı arttıkça isimlendirmenin önemi de artar. Kafa karıştırıcı test isimleri kullanmak ileride problemlere yol açar. Açıklayıcı olması için test isimlerini uzun tutmanız gerekiyorsa öyle yapın, uzun isimler yanlış isimlerden daha faydalıdır.
Test koduna ikinci sınıf kod muamelesi yapmayın: Testler de yazılımın bir parçasıdır. Dolayısıyla normal program kodunu yazarken ne kadar özen gösteriyorsanız test kodlarına da aynı özeni gösterin, kod tekrarlarından kaçının, okunabilir test kodu yazın.

## Kaynak

- <http://www.seckintozlu.com/etiketler/unit-test>
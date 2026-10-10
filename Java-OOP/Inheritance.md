
## <mark>1.2 Kalıtım (Inheritance)</mark>
Kalıtım (Inheritance), bir sınıfın başka bir sınıfın özelliklerini ve metotlarını devralmasını sağlayan nesne yönelimli programlama prensibidir.
Java'da kalıtım sayesinde ortak özellikleri tek bir sınıfta tanımlayabilir ve bu özellikleri diğer sınıflarda yeniden kullanabiliriz. Böylece kod tekrarını azaltabilir ve daha düzenli bir yapı oluşturabiliriz.
####  Kalıtım nasıl yapılır?
Java'da kalıtım oluşturmak için <mark>extends</mark> anahtar kelimesi kullanılır.
Örneğin, bir Hayvan sınıfımız ve bu sınıftan türeyen Kopek sınıfımız olsun.

<table>
<tr>
<td width="50%" valign="top">
<img src="https://github.com/user-attachments/assets/0bab7f50-15ed-423b-9060-6308bdb95f6a" alt="image" width="100%">
</td>
<td width="50%" valign="top">

```java
class Hayvan {
    String isim;
    public void sesCikar() {
        System.out.println("Hayvan ses çıkarıyor.");
    }
}
class Kopek extends Hayvan {
    public void havla() {
        System.out.println("Köpek havlıyor!");
    }
}
```
</td>
</tr>
</table>

#### Kodun açıklaması
+ Hayvan: Üst sınıftır (superclass).
+ Kopek: Alt sınıftır (subclass).
+ extends Hayvan: Kopek sınıfının Hayvan sınıfından türediğini belirtir.
+ isim ve sesCikar(): Kopek nesneleri tarafından da kullanılabilir.
+ havla(): Yalnızca Kopek sınıfında tanımlanmış bir metottur.
#### Nasıl kullanılır?
```java
public class Main {
    public static void main(String[] args) {
        Kopek kopek = new Kopek();
        kopek.isim = "Kopek";
        System.out.println(kopek.isim);
        kopek.sesCikar();
        kopek.havla();
    }
}
```
#### Çıktı
Kopek <br/>
Hayvan ses çıkarıyor.<br/>
Köpek havlıyor!<br/><br/>
Gördüğün gibi Kopek sınıfında isim veya sesCikar() metotlarını yeniden yazmadık. Bunları Hayvan sınıfından devraldık

#### <mark>Kalıtımda super anahtar kelimesi</mark>
super, alt sınıftan üst sınıfın erişilebilir üyelerine ulaşmak için kullanılır. Üst sınıfın kurucusunu çağırmak için de kullanılabilir.
```java
class Hayvan {
    public void sesCikar() {
        System.out.println("Hayvan ses çıkarıyor.");
    }
}

class Kedi extends Hayvan {
    @Override
    public void sesCikar() {
        super.sesCikar();
        System.out.println("Miyav!");
    }
}
```
Burada <mark>super</mark>.sesCikar() üst sınıftaki metodu çağırır. <mark>@Override</mark>ise alt sınıfta üst sınıftan gelen metodun yeniden tanımlandığını belirtir.

#### Kalıtımın avantajları
- <strong>Kod tekrarını azaltır</strong>: Ortak özellikler üst sınıfta tutulabilir.
- <strong>Kodun yeniden kullanılmasını sağlar</strong>: Alt sınıflar üst sınıfın erişilebilir üyelerini kullanabilir.
- <strong>Genişletilebilirlik sağlar</strong>: Alt sınıflara yeni özellikler eklenebilir.
- <strong>Polimorfizmi destekler</strong>: Üst sınıf referansları üzerinden alt sınıf nesneleri kullanılabilir.
#### Java'da kalıtım kuralları
+ <i>Bir sınıf, <mark>extends</mark> ile yalnızca bir sınıftan doğrudan kalıtım alabilir.</i>
+ <i>Bir sınıf birden fazla arayüzü (interface) <mark>implements</mark> ile uygulayabilir.</i>
+ <i><mark>private</mark> üyeler alt sınıfta doğrudan erişilebilir değildir.</i>
+ <i><mark>final</mark> olarak tanımlanan bir sınıftan kalıtım alınamaz.</i>
+ <i>Kurucular (constructors) kalıtılmaz; alt sınıf kurucuları üst sınıf kurucularını çağırabilir.</i>

#### Kısa özet
Kalıtımı şu şekilde düşünebilirsin:

###### <i>Hayvan → Üst sınıf</i>
###### <i>Kopek → Alt sınıf</i>
###### <i>extends → Kalıtım kurmak için kullanılan anahtar kelime</i>
###### <i>super → Üst sınıfın erişilebilir üyelerine ulaşmak için kullanılan anahtar kelime</i>
###### <i>@Override → Devralınan bir metodun yeniden tanımlandığını belirtir</i>

 GitHub dokümantasyonunda sıradaki konu: Soyutlama (Abstraction). Kalıtım ile soyutlamayı öğrendikten sonra çok biçimlilik (Polymorphism) konusunu ele alabilirsin.
 ###### <p align="center"><i>Teşekkür ederim...<i/></p>

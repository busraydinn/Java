## <mark>1.3.4 Polymorphism (Çok Biçimlilik)</mark>
Çok biçimlilik (Polymorphism), nesne yönelimli programlamada aynı metot çağrısının, nesnenin türüne veya kullanılan parametrelere bağlı olarak farklı davranışlar gösterebilmesini sağlayan prensiptir.

Java'da polimorfizm sayesinde ortak bir üst sınıf veya arayüz üzerinden farklı nesnelerle çalışabiliriz. Böylece kodumuzu daha esnek, genişletilebilir ve yönetilebilir hâle getirebiliriz.

#### <i>Java'da polimorfizm iki temel başlık altında incelenir:</i>

+ <strong>Compile-time Polymorphism (Derleme zamanı)</strong>: Method Overloading (Metot aşırı yükleme)
+ <strong>Runtime Polymorphism (Çalışma zamanı)</strong>: Method Overriding (Metot ezme)

### <mark> Runtime Polymorphism (Çalışma zamanı polimorfizmi)</mark>
Çalışma zamanı polimorfizmi, alt sınıfların üst sınıftan gelen bir metodu kendi davranışlarına uygun şekilde yeniden tanımlamasıyla ortaya çıkar.
Örneğin, Hayvan sınıfından türeyen Kopek ve Kedi sınıflarını ele alalım.
```java
class Hayvan {
    public void sesCikar() {
        System.out.println("Hayvan ses çıkarıyor.");
    }
}
class Kopek extends Hayvan {
    @Override
    public void sesCikar() {
        System.out.println("Köpek havlıyor.");
    }
}

class Kedi extends Hayvan {
    @Override
    public void sesCikar() {
        System.out.println("Kedi miyavlıyor.");
    }
}
```
#### Nasıl kullanılır?
```java
public class Main {
    public static void main(String[] args) {
        Hayvan hayvan1 = new Kopek();
        Hayvan hayvan2 = new Kedi();
        hayvan1.sesCikar();
        hayvan2.sesCikar();
    }
}
```
#### Çıktı:
```text
Köpek havlıyor.
Kedi miyavlıyor.
```
#### Burada ne oldu?
+ Hayvan hayvan1 = new Kopek(); ifadesinde referans türü Hayvan, gerçek nesne türü Kopek olur.
+ hayvan1.sesCikar() çağrıldığında Kopek sınıfındaki metot çalışır.
+ Aynı şekilde hayvan2.sesCikar() çağrıldığında Kedi sınıfındaki metot çalışır.

<i>Önemli nokta: Override edilmiş bir örnek metodu çağrıldığında, çalıştırılacak uygulama nesnenin gerçek türüne göre belirlenir.</i>

### <mark>Compile-time Polymorphism (Derleme zamanı polimorfizmi)</mark>
Java'da metot aşırı yükleme (Method Overloading), aynı sınıfta aynı isimli fakat farklı parametre listelerine sahip birden fazla metot tanımlamamızı sağlar.
```java
class Hesaplama {
    public int topla(int a, int b) {
        return a + b;
    }
    public int topla(int a, int b, int c) {
        return a + b + c;
    }
    public double topla(double a, double b) {
        return a + b;
    }
}
```
#### Kullanımı:
```java
public class Main {
    public static void main(String[] args) {
        Hesaplama hesap = new Hesaplama();
        System.out.println(hesap.topla(5, 10));
        System.out.println(hesap.topla(5, 10, 15));
        System.out.println(hesap.topla(2.5, 3.5));
    }
}
```
#### Çıktı:
```text
15
30
6.0
```
Java, hangi metodun çağrılacağını metot adı ve argümanların türleri ile sayısı gibi parametre listesine ilişkin bilgilere göre derleme sırasında belirler.

<i>Dikkat: Yalnızca dönüş türünü değiştirmek, metot aşırı yüklemek için yeterli değildir.</i>

## <mark> Polimorfizmin soyutlama ve kalıtımla ilişkisi</mark>
Polimorfizm, önceki iki konuyla birlikte kullanıldığında daha anlamlı hâle gelir.
```java

abstract class Sekil {

    abstract double alanHesapla();
}

class Kare extends Sekil {

    private double kenar;

    public Kare(double kenar) {
        this.kenar = kenar;
    }

    @Override
    double alanHesapla() {
        return kenar * kenar;
    }
}

class Daire extends Sekil {

    private double yaricap;

    public Daire(double yaricap) {
        this.yaricap = yaricap;
    }

    @Override
    double alanHesapla() {
        return Math.PI * yaricap * yaricap;
    }
}
```
Farklı şekillerin alanlarını aynı metot üzerinden hesaplayabiliriz:

```java

public class Main {

    public static void main(String[] args) {

        Sekil[] sekiller = {
            new Kare(5),
            new Daire(3)
        };

        for (Sekil sekil : sekiller) {
            System.out.println(sekil.alanHesapla());
        }
    }
}
```
#### Çıktı:
```text
25.0
28.274333882308138
```
Burada:
+ Soyutlama: Sekil sınıfı, şekillerin alan hesaplaması gerektiğini belirtir.
+ Kalıtım: Kare ve Daire, Sekil sınıfından türetilir.
+ Polimorfizm: Aynı alanHesapla() çağrısı, farklı nesnelerde farklı sonuçlar üretir.

#### Polimorfizmin avantajları
- Esneklik: Farklı nesneler ortak bir üst tür üzerinden kullanılabilir.
- Genişletilebilirlik: Yeni sınıflar eklenirken mevcut kodda daha az değişiklik gerekebilir.
- Kod tekrarını azaltma: Ortak işlemler tek bir metot veya döngü üzerinden yürütülebilir.
- Bakım kolaylığı: Her sınıf kendi davranışının sorumluluğunu üstlenir.

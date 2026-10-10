
## <mark>1.1 Kapsülleme (Encapsulation)</mark>
+ Kapsülleme (Encapsulation), bir sınıfın verilerini ve bu veriler üzerinde işlem yapan metotları bir arada tutarak verilere erişimi kontrol etme prensibidir.
+ Java'da kapsülleme genellikle private değişkenler ve bu değişkenlere kontrollü erişim sağlayan public metotlar (getter ve setter) ile uygulanır.

###### Örnek:
Bir Araba sınıfımız olsun. Arabanın hızına herkesin doğrudan müdahale etmesini istemiyoruz.

```java
public class Araba {
    private int hiz;
    public int getHiz(){
        return this.hiz;
    }
    public void setHiz(int hiz)
    {
        if(hiz>=0&&hiz<=300)
        {
            this.hiz=hiz;
        }
    }
}
```
##### Kodun açıklaması
+ private int hiz; — hiz değişkenine sınıf dışından doğrudan erişilmesini engeller.
+ getHiz() — mevcut hızı okumayı sağlar.
+ setHiz(int hiz) — hız değerini belirli koşullara göre değiştirmeyi sağlar.
+ this.hiz — mevcut nesnenin hiz değişkenini ifade eder.
##### Kullanım

```java
public class Main {
    public static void main(String[] args) {
        Araba araba = new Araba();

        araba.setHiz(120);
        System.out.println(araba.getHiz()); // 120

        araba.setHiz(-50);
        System.out.println(araba.getHiz()); // 120
    }
}
```
###### Çıktı
<img width="402" height="140" alt="image" src="https://github.com/user-attachments/assets/ff56eab5-a37e-45b4-aaa6-f3e8f29288a0" />

Neden sonuç 120 olarak kalıyor? Çünkü setHiz() metodu negatif hız değerini kabul etmiyor. Böylece nesnenin verisi kontrollü biçimde korunuyor.
###### Kapsülleme olmasaydı ne olurdu?
Kapsülleme kullanılmadan
```java
public int hiz;
```
Bu durumda sınıf dışından şu şekilde erişilebilir:

```java
araba.hiz = -50;
```
Negatif bir değer doğrudan atanabilir ve sınıfın belirlediği kurallar atlanabilir.

####  Kapsüllemenin avantajları
+ <strong>Veri güvenliği</strong>: Değişkenlere doğrudan erişimi sınırlar.
+ <strong>Kontrollü erişim</strong>: Verilerin hangi koşullarda değiştirileceğini belirler.
+ <strong>Bakım kolaylığı</strong>: İç uygulamayı değiştirmeyi kolaylaştırır.
+ <strong>Doğrulama</strong>: Geçersiz değerlerin atanmasını önlemeye yardımcı olur.

<i><strong>Önemli</strong>: Kapsülleme yalnızca getter ve setter yazmak değildir. Asıl amaç, nesnenin durumunu korumak ve erişimi gerektiği kadar sınırlandırmaktır. Her değişken için setter oluşturmak zorunlu değildir.</i>

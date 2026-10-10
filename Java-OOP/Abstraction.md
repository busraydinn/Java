## <mark>1.3 Abstraction (Soyutlama)</mark>
Soyutlama (Abstraction), bir nesnenin nasıl çalıştığına ilişkin gereksiz uygulama ayrıntılarını gizleyerek kullanıcıya yalnızca gerekli özellikleri ve davranışları sunma prensibidir.

Günlük hayattan bir örnek düşünelim: Bir araba kullanırken gaz pedalına basarsın ve araba hızlanır. Motorun yakıtı nasıl işlediğini veya enjeksiyon sisteminin nasıl çalıştığını bilmen gerekmez. Bu ayrıntılar gizlenirken sana gerekli olan kullanım sunulur. İşte bu, soyutlama fikrini anlamak için güzel bir örnektir.

Java'da soyutlama temel olarak iki yöntemle uygulanabilir:
+ Abstract class (Soyut sınıf)
+ Interface (Arayüz)

##### <mark>1.3.1 Abstract class (Soyut sınıf)</mark>
Soyut sınıflar, abstract anahtar kelimesiyle tanımlanır. Hem gövdeli metotlar hem de gövdesiz, alt sınıfların uygulaması gereken soyut metotlar içerebilirler.

Örneğin farklı hayvanların ses çıkarma davranışını ele alalım.
```java
abstract class Hayvan {
    abstract void sesCikar();
    public void uyu() {
        System.out.println("Hayvan uyuyor.");
    }
}
class Kopek extends Hayvan {
    @Override
    void sesCikar() {
        System.out.println("Köpek havlıyor.");
    }
}
class Kedi extends Hayvan {
    @Override
    void sesCikar() {
        System.out.println("Kedi miyavlıyor.");
    }
}
```
#### Kodun açıklaması
+ <strong>abstract class Hayvan</strong>: Soyut bir sınıf tanımlar.
+ <strong>abstract void sesCikar();</strong>: Gövdesi olmayan soyut bir metottur.
+ <strong>Kopek ve Kedi</strong>: Soyut metodu kendi davranışlarına uygun şekilde uygular.
+ <strong>uyu()</strong>: Gövdeli, yani doğrudan uygulanmış bir metottur ve alt sınıflar tarafından kullanılabilir.

<i><strong>Önemli:</strong> Soyut bir sınıftan doğrudan nesne oluşturulamaz. Örneğin new Hayvan() kullanılamaz.<i>

#### Nasıl kullanılır?
```java
public class Main {
    public static void main(String[] args) {
        Hayvan kopek = new Kopek();
        Hayvan kedi = new Kedi();
        kopek.sesCikar();
        kedi.sesCikar();
        kopek.uyu();
    }
}
```
###### Çıktı:
```text
Köpek havlıyor.
Kedi miyavlıyor.
Hayvan uyuyor.
```
Burada Hayvan sınıfı, her hayvanın nasıl ses çıkaracağını belirlemez. Bunun yerine, alt sınıfların sesCikar() davranışını uygulamasını zorunlu kılar.

#### <mark>1.3.2 Interface (Arayüz) ile soyutlama</mark>
Java'da soyutlama için interface de kullanılabilir. Arayüz, sınıfların hangi davranışları sunması gerektiğini tanımlayan bir sözleşme oluşturur.
```java
interface Tasit {
    void hareketEt();
}
class Araba implements Tasit {
    @Override
    public void hareketEt() {
        System.out.println("Araba yolda ilerliyor.");
    }
}
class Ucak implements Tasit {
    @Override
    public void hareketEt() {
        System.out.println("Uçak havada ilerliyor.");
    }
}
```
Burada Tasit arayüzü, taşıtların hareketEt() davranışına sahip olmasını ister. Ancak hareketin nasıl gerçekleştirileceğini her sınıf kendisi belirler.
Kullanım örneği:

```java
Tasit tasit = new Araba();
tasit.hareketEt();
```
###### Çıktı:
```text
Araba yolda ilerliyor.
```
 
## 4. Abstract Class ve Interface Arasındaki Farklar

| Özellik | Abstract Class | Interface |
|---|---|---|
| Tanımlama | `abstract class` | `interface` |
| Kullanım | `extends` | `implements` |
| Nesne oluşturma | Doğrudan oluşturulamaz. | Doğrudan oluşturulamaz. |
| Metotlar | Soyut ve gövdeli metotlar içerebilir. | Soyut, `default`, `static` ve uygun durumlarda `private` metotlar içerebilir. |
| Alanlar | Örnek değişkenleri içerebilir. | Alanlar örtük olarak `public static final` olur. |
| Bir sınıfın kullanımı | Yalnızca bir sınıfı genişletebilir. | Birden fazla arayüz uygulayabilir. |

## 5. Soyutlamanın Avantajları

- **Karmaşıklığı azaltır:** Kullanıcı yalnızca gerekli davranışlarla ilgilenir.
- **Esneklik sağlar:** Uygulama ayrıntıları değişse bile ortak arayüz korunabilir.
- **Bakımı kolaylaştırır:** Kodun sorumlulukları daha net ayrılır.
- **Genişletilebilirliği artırır:** Aynı soyut yapıya farklı uygulamalar eklenebilir.

## 6. Soyutlama ve Kapsülleme Arasındaki Fark

Bu iki kavram sıklıkla karıştırılır:

- **Kapsülleme (Encapsulation):** Verilere erişimi kontrol eder ve nesnenin iç durumunu korumaya yardımcı olur.
- **Soyutlama (Abstraction):** Gereksiz uygulama ayrıntılarını gizler ve önemli davranışları ön plana çıkarır.

Kısaca, kapsülleme veriye nasıl erişildiğiyle, soyutlama ise hangi davranışların sunulduğu ve uygulama ayrıntılarının nasıl gizlendiğiyle ilgilidir.


 

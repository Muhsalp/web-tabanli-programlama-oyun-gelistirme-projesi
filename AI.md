## The transform() method replaces the transformation matrix, and multiplies it with a matrix described by:<br/><br/>a c e<br/>b d f<br/>0 0 1<br/><br/>ne demek?
Bu ifade, genellikle HTML5 Canvas API'sindeki transform(a, b, c, d, e, f) metodunun nasıl çalıştığını açıklamak için kullanılır. Şimdi bunu adım adım Türkçeye çevireyim ve açıklayayım:<br/><br/>📌 İngilizce İfade:<br/>The transform() method replaces the transformation matrix, and multiplies it with a matrix described by:
```css
a c e
b d f
0 0 1
```
🇹🇷 Türkçesi:<br/>transform() metodu, geçerli dönüşüm matrisini değiştirir ve bunu aşağıdaki matrisle çarpar:
```css
a c e  
b d f  
0 0 1
```
🔍 Ne Anlama Geliyor?<br/>Canvas'ta çizim yaparken, şekilleri döndürmek, ölçeklendirmek, kaydırmak gibi işlemler için bir dönüşüm matrisi (transformation matrix) kullanılır. Bu matris, tüm çizimlerinizi nasıl değiştireceğinizi belirler.<br/><br/>transform(a, b, c, d, e, f) fonksiyonu, sizin verdiğiniz bu altı parametreyle bir 3x3 matris oluşturur:
```less
| a  c  e |
| b  d  f |
| 0  0  1 |
```
Bu matris:<br/><br/>a, d: ölçekleme (scale)<br/><br/>b, c: eğme (skew)<br/><br/>e, f: çevirme (translate)<br/><br/>gibi işlemleri temsil eder.<br/><br/>Bu matris, mevcut dönüşüm matrisiyle çarpılarak, yeni dönüşüm matrisini oluşturur. Yani eski matris * yeni matris = güncel matris olur.<br/><br/>🔧 Örnek:
```javascript
ctx.transform(1, 0, 0, 1, 100, 0);
```
Bu, X ekseninde çizimleri 100 birim sağa kaydırır (çünkü e = 100). Diğer değerler varsayılan dönüşüm anlamına gelir (hiçbir ölçekleme, döndürme vs. yok).<br/><br/>Eğer istersen, bu matrislerin nasıl çalıştığını görsel olarak da anlatabilirim.
## Son satır neden 0 0 1?
Harika bir soru! 👇 Bu kısmı iyi anlarsan 2D dönüşümleri ve matris mantığını çok daha net kavrarsın.<br/><br/>✅ Kısaca cevap:<br/>Son satırın 0 0 1 olması, bu matrisin homojen koordinatlar (homogeneous coordinates) kullanan bir 2D dönüşüm matrisi olduğunu gösterir.<br/><br/>Bu yapı sayesinde:<br/><br/>Çevirme (translation) işlemleri matrisle ifade edilebilir.<br/><br/>Dönüşüm işlemleri tek bir matris çarpımı ile birleştirilebilir.<br/><br/>Hesaplama işlemleri daha sistematik hale gelir.<br/><br/>🔍 Detaylı Açıklama:<br/>Bilgisayarda 2D grafiklerde, genelde bir nokta şöyle ifade edilir:
```scss
(x, y)
```
Ama dönüşüm matrisleri ile çevirme (translate) işlemi yapmak için bu yetmez. Bunun yerine homojen koordinatlar denilen yöntemi kullanırız ve noktayı şu şekilde yazarız:
```csharp
[x, y, 1]
```
Bu sayede çevirme (translation) işlemi de matrisle yapılabilir. Normal 2x2 matrisle sadece döndürme, ölçekleme, eğme yapılabilir; ama çevirme yapılamaz. Bu yüzden 3x3'lük matris kullanılır.<br/><br/>🧮 Matrisin Tam Yapısı:<br/>Dönüşüm matrisi:
```less
| a  c  e |
| b  d  f |
| 0  0  1 |
```
Ve bir nokta vektörü:
```
| x |
| y |
| 1 |
```
Bu ikisi çarpıldığında:
```vbnet
x' = a * x + c * y + e  
y' = b * x + d * y + f
```
Bu formül sayesinde:<br/><br/>a, d ile ölçekleme<br/><br/>b, c ile eğme/döndürme<br/><br/>e, f ile kaydırma (çevirme) yapılır.<br/><br/>📌 Özet:<br/>Son satır 0 0 1, bu matrisin homojen koordinatlara göre tanımlandığını gösterir.<br/><br/>Bu yapı, çevirme (translation) gibi işlemleri de matrisle yapabilmemizi sağlar.<br/><br/>Bilgisayar grafiklerinde bu, standart bir tekniktir.<br/><br/>İstersen bu matrisle adım adım bir örnek dönüşüm yapabiliriz.
## Olur.
Süper! O zaman adım adım bir örnek dönüşüm işlemi yapalım. 🎯<br/><br/>🎨 Senaryo:<br/>Diyelim ki elimizde bir nokta var:
```
(x, y) = (10, 20)
```
Bu noktayı şu işlemlerden geçirmek istiyoruz:<br/><br/>X ekseninde 2 kat büyüt (scale)<br/><br/>Y ekseninde 3 kat büyüt (scale)<br/><br/>X ekseninde 5 birim sağa kaydır (translate)<br/><br/>🧮 Adım 1: Matrisin Oluşturulması<br/>Bu işlemler için uygun matris:
```r
| a  c  e |    =   | 2  0  5 |
| b  d  f |        | 0  3  0 |
| 0  0  1 |        | 0  0  1 |
```
Buradaki değerlerin anlamı:<br/><br/>a = 2 → X ekseninde 2x ölçekleme<br/><br/>d = 3 → Y ekseninde 3x ölçekleme<br/><br/>e = 5 → X ekseninde 5 birim sağa kaydırma<br/><br/>b, c = 0 → Eğme yok<br/><br/>🔢 Adım 2: Nokta Vektörünü Oluşturalım<br/>Homojen koordinatlarda noktamız:
```
| x |     | 10 |
| y |  =  | 20 |
| 1 |     |  1 |
```
➗ Adım 3: Matris Çarpımı
```markdown
| 2  0  5 |     | 10 |     =     | (2*10 + 0*20 + 5) = 25 |
| 0  3  0 |  x  | 20 |     =     | (0*10 + 3*20 + 0) = 60 |
| 0  0  1 |     |  1 |     =     | 1                      |
```
✅ Sonuç:<br/>Yeni nokta:
```bash
(x', y') = (25, 60)
```
Yani:<br/><br/>X ekseninde 2x ölçekleme: 10 → 20<br/><br/>Sonra 5 birim sağa kaydırma: 20 → 25<br/><br/>Y ekseninde 3x ölçekleme: 20 → 60<br/><br/>İstersen:<br/>Eğme (skew) veya döndürme (rotate) içeren bir örnek de yapabiliriz.<br/><br/>Veya bunu JavaScript kodu olarak yazabiliriz (canvas.transform() şeklinde).<br/><br/>Hangisini istersin?
## Eğme (skew) ve döndürme (rotate) içeren bir örnek olsun.
Harika! Şimdi bir örnek üzerinden hem eğme (skew) hem de döndürme (rotate) içeren bir dönüşüm yapalım. Bunlar biraz daha soyut ama çok güçlü dönüşümlerdir. Adım adım açıklayacağım. 🚀<br/><br/>🎯 Senaryo:<br/>Elimizde bir nokta var:
```
(x, y) = (10, 5)
```
Bu noktaya iki işlem uygulayalım:<br/><br/>X ekseninde 30 derece döndür (rotate)<br/><br/>Y eksenine göre biraz eğ (skew X = 1)<br/><br/>🔧 1. Dönüşüm: Döndürme (Rotate)<br/>Bir 2D döndürme matrisi şöyle tanımlanır:
```cpp
| cos(θ)  -sin(θ)  0 |
| sin(θ)   cos(θ)  0 |
|   0        0     1 |
```
30 derece = π/6 rad → yaklaşık 0.5236 radyan<br/><br/>cos(30°) ≈ 0.866<br/><br/>sin(30°) ≈ 0.5<br/><br/>Matrisi yazalım:
```
| 0.866  -0.5    0 |
| 0.5     0.866  0 |
| 0       0      1 |
```
🔧 2. Dönüşüm: X Ekseninde Eğme (SkewX)<br/>Eğme için matris:
```cpp
| 1  tan(α)  0 |
| 0    1     0 |
| 0    0     1 |
```
Diyelim ki α = 45° yani tan(45°) = 1, o zaman:
```
| 1  1  0 |
| 0  1  0 |
| 0  0  1 |
```
🧮 3. İki Matrisi Birleştirelim<br/>Toplam dönüşüm = SkewX * Rotate<br/>(Bu sıraya dikkat! Son yapılan işlem başa yazılır)<br/>SkewX:
```
| 1   1     0 |
| 0   1     0 |
| 0   0     1 |
```
Rotate:
```
| 0.866  -0.5    0 |
| 0.5     0.866  0 |
| 0       0      1 |
```
Matris Çarpımı (SkewX * Rotate):
```markdown
| 1*0.866 + 1*0.5      1*(-0.5) + 1*0.866     0 |
| 0*0.866 + 1*0.5      0*(-0.5) + 1*0.866     0 |
|        0                    0              1 |
```
Sonuç:
```
| 1.366   0.366   0 |
| 0.5     0.866   0 |
| 0       0       1 |
```
🔢 4. Nokta Üzerinde Uygulama<br/>Nokta: (10, 5) → homojen haliyle [10, 5, 1]<br/><br/>Çarpalım:
```vbnet
x' = 1.366 * 10 + 0.366 * 5 = 13.66 + 1.83 = 15.49  
y' = 0.5 * 10 + 0.866 * 5 = 5 + 4.33 = 9.33
```
✅ Sonuç:<br/>Yeni konumu:
```scss
(x', y') ≈ (15.49, 9.33)
```
Yani:<br/><br/>Önce 30° döndürdük,<br/><br/>Sonra X ekseni boyunca 45° eğdik,<br/><br/>Sonuç olarak nokta kaydı ve yön değiştirdi.<br/><br/>İstersen:<br/>Bu işlemi gerçek bir canvas örneği ile kodda da gösterebilirim. İlgin varsa yazayım mı?

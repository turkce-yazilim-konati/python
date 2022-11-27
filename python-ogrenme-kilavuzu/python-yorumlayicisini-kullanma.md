# Python Yorumlayıcısını Kullanma

### 2.1. Yorumlayıcıyı&#x20;

Python yorumlayıcısı genellikle `/usr/local/bin/python3.10` mevcut olduğu makinelerde olduğu gibi kurulur; Unix `/usr/local/bin`kabuğunuzun arama yolunu girmek, şu komutu yazarak başlatmayı mümkün kılar:

```
python3.10
```

kabuğa. [1](https://docs.python.org/3.10/tutorial/interpreter.html#id2) Tercümanın yaşadığı dizinin seçimi bir kurulum seçeneği olduğundan, başka yerler de mümkündür; yerel Python gurunuza veya sistem yöneticinize danışın. (Örneğin, `/usr/local/python`popüler bir alternatif konumdur.)

[Python'u Microsoft Store'dan](https://docs.python.org/3.10/using/windows.html#windows-store) yüklediğiniz Windows makinelerinde komut `python3.10`kullanılabilir olacaktır. py.exe [başlatıcısı](https://docs.python.org/3.10/using/windows.html#launcher) kuruluysa, `py` komutu kullanabilirsiniz. Python'u başlatmanın diğer yolları için [Arasöz: Ortam değişkenlerini ayarlama](https://docs.python.org/3.10/using/windows.html#setting-envvars) konusuna bakın .

Birincil istemde bir dosya sonu karakteri ( Unix'te, Windows'ta) yazmak, yorumlayıcının sıfır çıkış durumuyla çıkmasına neden olur. Bu işe yaramazsa, aşağıdaki komutu yazarak yorumlayıcıdan çıkabilirsiniz: .Control-DControl-Z`quit()`

[Yorumlayıcının satır düzenleme özellikleri, GNU Readline](https://tiswww.case.edu/php/chet/readline/rltop.html) kitaplığını destekleyen sistemlerde etkileşimli düzenleme, geçmiş değiştirme ve kod tamamlamayı içerir . Komut satırı düzenlemenin desteklenip desteklenmediğini görmek için belki de en hızlı kontrol, aldığınız ilk Python istemine yazmaktır. Bip sesi çıkarırsa, komut satırı düzenlemeniz vardır; tuşlara giriş için Ek [Etkileşimli Giriş Düzenleme ve Geçmiş Değiştirme bölümüne bakın. ](https://docs.python.org/3.10/tutorial/interactive.html#tut-interacting)Hiçbir şey görünmüyorsa veya yankılanıyorsa, komut satırı düzenlemesi kullanılamaz; sadece mevcut satırdan karakterleri kaldırmak için geri al tuşunu kullanabileceksiniz.Control-P`^P`

Yorumlayıcı bir şekilde Unix kabuğu gibi çalışır: bir tty aygıtına bağlı standart girdi ile çağrıldığında, komutları etkileşimli olarak okur ve yürütür; bir dosya adı argümanıyla veya standart girdi olarak bir dosyayla çağrıldığında, o dosyadan bir _komut dosyası_ okur ve yürütür .

Yorumlayıcıyı başlatmanın ikinci bir yolu , kabuğun seçeneğine benzer şekilde _komuttaki_ ifadeleri yürüten . Python deyimleri genellikle kabuğa özel boşluklar veya diğer karakterler içerdiğinden, genellikle _komutun_ tamamının alıntılanması önerilir.`python -c command [arg] ...`[`-c`](https://docs.python.org/3.10/using/cmdline.html#cmdoption-c)

Bazı Python modülleri betik olarak da kullanışlıdır. _Bunlar, modülün_ kaynak dosyasını komut satırında tam adını yazmışsınız gibi çalıştıran kullanılarak çağrılabilir .`python -m module [arg] ...`

Bir komut dosyası kullanıldığında, komut dosyasını çalıştırabilmek ve daha sonra etkileşimli moda girebilmek bazen yararlıdır. [`-i`](https://docs.python.org/3.10/using/cmdline.html#cmdoption-i) Bu , komut dosyasından önce geçerek yapılabilir .

Tüm komut satırı seçenekleri [Komut satırı ve ortamda](https://docs.python.org/3.10/using/cmdline.html#using-on-general) açıklanmıştır .

#### 2.1.1. Argüman Geçişi&#x20;

Yorumlayıcı tarafından bilindiğinde, komut dosyası adı ve bundan sonraki ek argümanlar bir diziler listesine dönüştürülür ve modüldeki `argv` değişkene atanır. `sys`Yürüterek bu listeye erişebilirsiniz . Listenin uzunluğu en az birdir; hiçbir komut dosyası ve hiçbir argüman verilmediğinde, boş bir dizedir. Komut dosyası adı (standart girdi anlamında) olarak verildiğinde, olarak ayarlanır . _Komut_ kullanıldığında, olarak ayarlanır . _Modül_ kullanıldığında, bulunan modülün tam adına ayarlanır. _Komut_ veya _modülden_ sonra bulunan seçenekler , Python yorumlayıcısının seçenek işlemesi tarafından tüketilmez, ancak bırakılır.`import syssys.argv[0]'-'sys.argv[0]'-'`[`-c`](https://docs.python.org/3.10/using/cmdline.html#cmdoption-c) `sys.argv[0]'-c'`[`-m`](https://docs.python.org/3.10/using/cmdline.html#cmdoption-m) `sys.argv[0]`[`-c`](https://docs.python.org/3.10/using/cmdline.html#cmdoption-c) [`-m`](https://docs.python.org/3.10/using/cmdline.html#cmdoption-m) `sys.argv`işlemek için komut veya modül için.

#### 2.1.2. Etkileşimli Mod&#x20;

_Komutlar bir tty'den okunduğunda, yorumlayıcının etkileşimli modda_ olduğu söylenir . Bu modda, _birincil komut_ istemiyle bir sonraki komutu ister , genellikle üç büyüktür işareti ( `>>>`); devam satırları için varsayılan olarak üç nokta ( ) olmak üzere _ikincil bilgi istemiyle ister ._ `...`Tercüman, ilk istemi yazdırmadan önce sürüm numarasını ve telif hakkı bildirimini belirten bir karşılama mesajı yazdırır:

```
$ python3.10
Python 3.10 (default, June 4 2019, 09:25:04)
[GCC 4.8.2] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

Çok satırlı bir yapıya girerken devam satırlarına ihtiyaç vardır. Örnek olarak, şu açıklamaya bir göz atın [`if`](https://docs.python.org/3.10/reference/compound\_stmts.html#if):

\>>>

```
>>> the_world_is_flat = True
>>> if the_world_is_flat:
...     print("Be careful not to fall off!")
...
Be careful not to fall off!
```

Etkileşimli mod hakkında daha fazla bilgi için bkz . [Etkileşimli Mod](https://docs.python.org/3.10/tutorial/appendix.html#tut-interac) .

### 2.2. Yorumlayıcı ve Ortamı&#x20;

#### 2.2.1. Kaynak Kodu Kodlaması&#x20;

Varsayılan olarak, Python kaynak dosyaları UTF-8'de kodlanmış olarak kabul edilir. Bu kodlamada, dünyadaki çoğu dilin karakterleri, dize değişmezlerinde, tanımlayıcılarda ve yorumlarda aynı anda kullanılabilir - standart kitaplık tanımlayıcılar için yalnızca ASCII karakterlerini kullansa da, herhangi bir taşınabilir kodun izlemesi gereken bir kuraldır. Tüm bu karakterleri düzgün bir şekilde görüntülemek için editörünüzün dosyanın UTF-8 olduğunu bilmesi ve dosyadaki tüm karakterleri destekleyen bir yazı tipi kullanması gerekir.

Varsayılandan farklı bir kodlama bildirmek için , dosyanın _ilk_ satırı olarak özel bir yorum satırı eklenmelidir . Sözdizimi aşağıdaki gibidir:

```
# -*- coding: encoding -*-
```

burada _kodlama_[`codecs`](https://docs.python.org/3.10/library/codecs.html#module-codecs) Python tarafından desteklenen geçerli kodlardan biridir .

Örneğin, Windows-1252 kodlamasının kullanılacağını bildirmek için kaynak kod dosyanızın ilk satırı şöyle olmalıdır:

```
# -*- coding: cp1252 -*-
```

_İlk satır_ kuralının bir istisnası , kaynak kodun bir [UNIX "shebang" satırıyla](https://docs.python.org/3.10/tutorial/appendix.html#tut-scripts) başlamasıdır . Bu durumda, kodlama bildirimi dosyanın ikinci satırı olarak eklenmelidir. Örneğin:

```
#!/usr/bin/env python3
# -*- coding: cp1252 -*-
```

Dipnotlar

[1](https://docs.python.org/3.10/tutorial/interpreter.html#id1)

Unix'te Python 3.x yorumlayıcısı varsayılan olarak adlı yürütülebilir dosyayla birlikte yüklenmez `python`, böylece aynı anda yüklenen Python 2.x yürütülebilir dosyasıyla çakışmaz.
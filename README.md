# discordpyturkce
Bu, Discord API’ını kullanan uygulamalar oluşturmaya yardımcı olacak bir Python kitaplığı olan discord.py’ın Türkçe kılavuzudur.
Orijinal adres: https://discordpy.readthedocs.io/en/latest/
## Başlangıç

### Ön Koşullar
discord.py kütüphanesi Python’ın 3.5.3 ve daha üst sürümlerinde çalışmaktadır. Python’un önceki sürümleri için destek sağlanmamaktadır. Python 2.7 ve altı sürümler desteklenmemektedir. Python 3.4’ü desteklemeyen birleşimlerden biri (aiohttp) nedeniyle Python 3.4 veya daha düşük sürümler desteklenmez.
### Kurulum
PyPI (pip) kullarak direkt kütüphaneyi edinebilirsiniz.
```python
python3 -m pip install -U discord.py
```

Eğer Windows kullanıcısı iseniz, bu şekilde farklı bir kullanımdan da yararlanabilirsiniz.
```python
py -3 -m pip install -U discord.py
```

Ses desteği için discord.py içinden discord.py[voice]’ı kullanmanız gereklidir.
```python
py -3 -m pip install -U discord.py
```

### Basit Konseptler
discord.py Olay (event) konseptini sıkça kullanır. "event" herhangi bir şeyin dinlenmesi ve cevap verilmesi durumudur. Örneğin: bir mesaj geldiğinde bunu "event" ile takip edebilir ve cevap verebilirsiniz. 

"Events" (olayların) nasıl çalıştığını gösteren hızlı bir örnek:
```python
import discord

class MyClient(discord.Client):
    async def on_ready(self):
        print('Olarak giriş yaptık: {0}!'.format(self.user))

    async def on_message(self, message):
        print('Mesaj şundan geldi: {0.author}: {0.content}'.format(message))

client = MyClient()
client.run('my token goes here')
```

## Hızlı Başlangıç

### Minik Bir Bot
Belirli bir mesajı yanıtlayan ve size yol gösteren bir bot yapalım.

Şuna benzer:
```python
import discord

client = discord.Client()

@client.event
async def on_ready():
    print('Olarak giriş yaptık: {0.user}'.format(client))

@client.event
async def on_message(message):
    if message.author == client.user:
        return

    if message.content.startswith('$merhaba'):
        await message.channel.send('Hello!')

client.run('token burada yer alır')
```
* Bu dosyayı ornek_bot.py olarak adlandıralım. Kitaplıkla çelişeceğinden dolayı dosya ismini **discord.py** vermemeye dikkat edin.
Burada birçok şey oluyor. Bu yüzden size gerçekleşen işlemleri adım adım göstereceğim.
İlk satır sadece kütüphaneyi içe aktarır. Eğer burada **ModuleNotFoundError** veya **ImportError** hatası ile karşılaşırsanız, bu kütüphaneyi doğru yüklemediğiniz anlamına gelir. Bunun için [**KURULUM**](https://github.com/Berkayerenemin/discordpyturkce#kurulum) kısmına bakın.

* Ardından, bir İstemci (Client) örneği oluşturuyoruz. Bu Client bizim Discord ile bağlantımızı sağlayacaktır.

* Daha sonra bir olayı kaydetmek için ```Client.event()``` görünümünü kullanırız. Bu kütüphane çok fazla olay (event) içermekte. Aynı zaman bu kütüphane eşzamansız (asynchronous) olduğu için, işleri geri arama (callback) tarzında yapıyoruz. Geri arama, aslına bir şey olduğu zaman çağrılan bir işlevdir. Yazdığımız kodda ```on_ready()``` olayı bot oturum açmayı ve işlerini ayarlamayı bitirdiğinde çağrılır. Bot bir mesaj aldığında ise ```on_message()``` olayı çağrılır.

* ```on_message()``` olayı alıan her mesaj için tektiklendiğinden dolayı kendimizden gelen mesajları görmezden geldiğimize emin olmalıyız. Bunu ```message.author```'un ```client.user``` ile aynı olup olmadığını kontrol ederek yaparız. 

* Daha sonra ```Message.content``` ögesinin '$merhaba' ile başlayıp başlamadığını kontrol ediyoruz. Öyleyse kullanıldığı kanalda 'Merhaba!' diye cevap veriyoruz.

* Son olarak botu giriş jetonumuz (token) ile çalıştırıyoruz. Jetonunuzu alma veya bir bot oluşturma konusunda yardıma ihtiyacınız varsa arama motorunda 'Discord Bott Hesabı Oluşturma' şeklinde arayabilirsiniz.

Artık bir botumuz olduğuna göre bunu çalıştırabiliriz. Neyse ki sadece bir Python betiği (script) olduğu için basitçe, direkt çalıştırabiliriz.
Windows'ta
```python
$ py -3 example_bot.py
```
Yahut başka sistemlerde
```python
$ python3 example_bot.py
```
Artık temel botunuzla oynamayı deneyebilirsiniz.

## V1.0'a Geçiş

### Python Sürüm Değişikliği

### Başlıca Model Değişiklikleri

#### Snowflakes Tam Sayı

#### Sunucu Artık Guild

#### Modeller Artık Durum Bilgili

#### Nitelik Değişimleri

#### Ses Durumu Değişiklikleri

#### Kullanıcı ve Üye Türü Ayrımı

#### Kanal Tipi Bölme

#### Çeşitli Model Değişiklikleri

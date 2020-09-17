# discordpyturkce
Bu, Discord API’ını kullanan uygulamalar oluşturmaya yardımcı olacak bir Python kitaplığı olan discord.py’ın Türkçe kılavuzudur.
Orijinal adres: https://discordpy.readthedocs.io/en/latest/
## Başlangıç

### Ön Koşullar
discord.py kütüphanesi Python’ın 3.5.3 ve daha üst sürümlerinde çalışmaktadır. Python’un önceki sürümleri için destek sağlanmamaktadır. Python 2.7 ve altı sürümler desteklenmemektedir. Python 3.4’ü desteklemeyen birleşimlerden biri (aiohttp) nedeniyle Python 3.4 veya daha düşük sürümler desteklenmez.
### Kurulum
PyPI (pip) kullarak direkt kütüphaneyi edinebilirsiniz.
```
python3 -m pip install -U discord.py
```

Eğer Windows kullanıcısı iseniz, bu şekilde farklı bir kullanımdan da yararlanabilirsiniz.
```
py -3 -m pip install -U discord.py
```

Ses desteği için discord.py içinden discord.py[voice]’ı kullanmanız gereklidir.
```
py -3 -m pip install -U discord.py
```

### Basit Konseptler
discord.py "event" (olay) konseptini sıkça kullanır. "event" herhangi bir şeyin dinlenmesi ve cevap verilmesi durumudur. Örneğin: bir mesaj geldiğinde bunu "event" ile takip edebilir ve cevap verebilirsiniz. 

"Events" (olayların) nasıl çalıştığını gösteren hızlı bir örnek:
```
import discord

class MyClient(discord.Client):
    async def on_ready(self):
        print('Logged on as {0}!'.format(self.user))

    async def on_message(self, message):
        print('Message from {0.author}: {0.content}'.format(message))

client = MyClient()
client.run('my token goes here')
```

## Hızlı Başlangıç

### Minik Bir Bot

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

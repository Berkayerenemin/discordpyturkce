![discordpytürkçe](https://img.shields.io/github/issues/Berkayerenemin/discordpyturkce)
![forks](https://img.shields.io/github/forks/Berkayerenemin/discordpyturkce)
![stars](https://img.shields.io/github/stars/Berkayerenemin/discordpyturkce)
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
python3 -m pip install -U discord.py[voice]
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
client.run('token burada yer alır')
```

## Hızlı Başlangıç

### Minik Bir Bot
Belirli bir mesajı yanıtlayan ve size yol gösteren bir bot yapalım.

Örneğin:
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
        await message.channel.send('Merhaba!')

client.run('token burada yer alır')
```
* Bu dosyayı ornek_bot.py olarak adlandıralım. Kitaplıkla çelişeceğinden dolayı dosya ismini **discord.py** vermemeye dikkat edin.
Burada birçok şey oluyor. Bu yüzden size gerçekleşen işlemleri adım adım göstereceğim.
İlk satır sadece kütüphaneyi içe aktarır. Eğer burada **ModuleNotFoundError** veya **ImportError** hatası ile karşılaşırsanız, bu kütüphaneyi doğru yüklemediğiniz anlamına gelir. Bunun için [**KURULUM**](https://github.com/Berkayerenemin/discordpyturkce#kurulum) kısmına bakın.

* Ardından, bir İstemci (client) örneği oluşturuyoruz. Bu client bizim Discord ile bağlantımızı sağlayacaktır.

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

v1.0 tam ve yeniden tasarım yapılması nedeniyle kütüphanedeki en önemli güncellemelerden birisidir. Yapılan değişiklikler o kadar büyük ve uzundur ki tüm niyet ve amaçlar için tamamiyle yeni bir kütüphanedir. Yeniden tasarımın bir kısmı, işleri daha kolay ve doğal hale getirmeyi amaçlar. Herhangi bir işi yapmak için bir istemci (client) gerektirmiyor bunun yerine modeller üzerinde işlem yapılıyor. 

### Python Sürüm Değişikliği

Geliştirmeyi kolaylaştırmak ve ayrıca bağımlılıklarımızın 3.7 veya daha yüksek kullanıma izin verecek şekilde yükseltilmesine izin vermek için 3.5.3'ten düşük Python sürümleri için desteği kaldırmak zorunda kaldık. Böylece Python 3.4 sürümü için de verdiğimiz desteği kaldırmış bulunuyoruz.

### Başlıca Model Değişiklikleri
v1.0'da gerçekleşen önemli model değişiklikleri aşağıdadır.

#### Snowflakes (İd Niteliği) Tam Sayı
v1.0'dan önce Snowflakes / İd Niteliği ("the ```id``` attiributes")'ler diziydi (```strings```) Bu güncelleme ile ```int```'e (Tamsayı) çevrildiler.
Kısa bir örnekle bunu görebiliriz.
```python
# önce
ch = client.get_channel('84319995256905728')
if message.author.id == '80528701850124288':
    ...

# sonra
ch = client.get_channel(84319995256905728)
if message.author.id == 80528701850124288:
    ...
```
Bu değişiklik kimliği kopyala özelliğini kullanırken daha az hataya neden olur çünkü artık bu tür ifadeleri tırnak içine almanız gerekmez. Aynı zamanda JSON yerine EFT'nin kullanılmasına izin vererek optimizasyon için daha uygun bir hale getirir.
#### Sunucu Artık Guild
Resmi API dokümantasyonu "Sunucu (Server)" yerine "Lonca (Guild)" konseptini kullanır. API dokümantasyonu ile gerektiğinde daha tutarlı olması açısından model ```Guild``` olarak yeniden adlandırıldı ve buna atıfta bulunan tüm örnekler de değiştirlmiş oldu. 

Değişikliklerin listesi aşağıdaki gibidir:
| Öncesi | Sonrası  |
| :---:   | :-: |
| ```Message.server``` | 	```Message.guild``` |
| ```Channel.server``` | 	```GuildChannel.guild``` |
| ```Client.servers``` | 	```Client.guilds``` |
| ```Client.get_server``` | 	```Client.get_guild()``` |
| ```Emoji.server``` | ```Emoji.guild``` |
| ```Role.server``` | ```Role.guild``` |
| ```Invite.server``` | ```Invite.guild``` |
| ```Member.server``` | ```Member.guild``` |
| ```Permissions.manage_server``` | ```Permissions.manage_guild``` |
| ```VoiceClient.server``` | 	```VoiceClient.guild``` |
| ```Client.create_server``` | ```Client.create_guild()``` |

#### Modeller Artık Durum Bilgili
Daha önce de bahsettiğimiz gibi birçok özellik İstemci (Client) dışına taşındı ve ilgili modellerine yerleştirildi.

Yapılan değişikliklerin bir listesini aşağıda bulabilirsiniz.
| Öncesi | Sonrası  |
| :---:   | :-: |
| ```Client.add_reaction``` | 	```Message.add_reaction()``` |
| ```Client.add_roles``` | 	```Member.add_roles()``` |
| ```Client.ban``` | 	```	Member.ban() or Guild.ban()``` |
| ```Client.change_nickname``` | 	```Member.edit()``` |
| ```Client.clear_reactions``` | 	```	Message.clear_reactions()``` |
| ```Client.create_channel``` | 	```Guild.create_text_channel() and Guild.create_voice_channel()``` |
| ```Client.create_custom_emoji``` | 	```Guild.create_custom_emoji()``` |
| ```Client.create_invite``` | 	```abc.GuildChannel.create_invite()``` |
| ```Client.create_role``` | 	```Guild.create_role()``` |
| ```Client.delete_channel``` | 	```abc.GuildChannel.delete()``` |
| ```Client.delete_channel_permissions```|     ```abc.GuildChannel.set_permissions()``` |
| ```Client.delete_custom_emoji```|     ```Emoji.delete()```|
| ```Client.delete_invite```|    ```Invite.delete() veya Client.delete_invite()```|
| ```Client.delete_message```|    ```Message.delete()```|
| ```Client.delete_messages```|    ```TextChannel.delete_messages()```|
| ```Client.delete_role```|    ```Role.delete()```|
| ```Client.delete_server``` | 	```Guild.delete()``` |
| ```Client.edit_channel``` | 	```TextChannel.edit() veya VoiceChannel.edit()``` |
| ```Client.edit_channel_permissions``` | 	```abc.GuildChannel.set_permissions()``` |
| ```Client.edit_custom_emoji``` | 	```Emoji.edit()``` |
| ```Client.edit_message``` | 	```Message.edit()``` |
| ```Client.edit_profile``` | 	```ClientUser.edit()``` |
| ```Client.edit_role``` | 	```Role.edit()``` |
| ```Client.edit_server``` | 	```Guild.edit()``` |
| ```Client.estimate_pruned_members``` | 	```Guild.estimate_pruned_members()``` |
| ```Client.get_all_emojis``` | 	```Client.emojis``` |
| ```Client.get_bans``` | 	```Guild.bans()``` |
| ```Client.get_invite``` | 	```Client.fetch_invite()``` |
| ```Client.get_message``` | 	```abc.Messageable.fetch_message()``` |
| ```Client.get_reaction_users``` | 	```Reaction.users()``` |
| ```Client.get_user_info``` | 	```Client.fetch_user()``` |
| ```Client.invites_from``` | 	```abc.GuildChannel.invites() veya Guild.invites()``` |
| ```Client.join_voice_channel``` | 	```VoiceChannel.connect()``` |
| ```Client.kick``` | 	```Guild.kick() veya Member.kick()``` |
| ```Client.leave_server``` | 	```Guild.leave()``` |
| ```Client.logs_from``` | 	```abc.Messageable.history()``` |
| ```Client.move_channel``` | 	```TextChannel.edit() veya VoiceChannel.edit()``` |
| ```Client.move_member``` | 	```Member.edit()``` |
| ```Client.move_role``` | 	```Role.edit()``` |
| ```Client.pin_message``` | 	```Message.pin()``` |
| ```Client.prune_members``` | 	```Guild.prune_members()``` |
| ```Client.purge_from``` | 	```TextChannel.purge()``` |
| ```Client.remove_reaction``` | 	```Message.remove_reaction()``` |
| ```Client.remove_roles``` | 	```Message.remove_roles()``` |
| ```Client.replace_roles``` | 	```Member.edit()``` |
| ```Client.send_file``` | 	```abc.Messageable.send()``` |
| ```Client.send_message``` | 	```abc.Messageable.send()``` |
| ```Client.send_typing``` | 	```abc.Messageable.trigger_typing() veya abc.Messageable.typing()``` |
| ```Client.server_voice_state``` | 	```Member.edit()``` |
| ```Client.start_private_message``` | 	```User.crate_dm()``` |
| ```Client.unban``` | 	```Guild.unban() veya Member.unban()``` |
| ```Client.unpin message``` | 	```Message.unpin()``` |
| ```Client.wait_for_message``` | 	```Client.wait_for()``` |
| ```Client.wait_for_reaction``` | 	```Client.wait_for()``` |
| ```Client.wait_until_login``` | 	```Kaldırıldı``` |
| ```Client.wait_until_ready``` | 	```Değiştirilmedi``` |

#### Nitelik Değişimleri
Biraz daha tutarlı olması açısından, özellik saydığımız bazı şeyleri yöntemlerle değiştirdik. 
Aşağıda özellik yerine kullanılan yöntemleri görüyorsunuz. (parantez gerektirir)

* Role.is_default()
* Client.is_ready()
* Client.is_closed()

#### Sözlük Değeri Değişimleri
Versiyon 1.0'dan önce, modellerin yerini alan bazı toplama özellikleri ```dict view``` nesneleri döndürüyordu.
Sonuç olarak, siz üzerinde yenileme işlemi yaptığınızda sözlüğün boyutu değiştiğinden dolayı bir RuntimeError hatası alıyordunuz. Bu olayı kısmen gidermek için ```dict view``` nesneleri listelere dönüştürüldü.

Aşağıda listeye çevirilen özellikler bulunmaktadır.

* Client.guilds
* Client.users
* Client.emojis
* Guild.channels
* Guild.text_channels
* Guild.voice_channels
* Guild.emojis
* Guild.members

#### Ses Durumu Değişiklikleri
Daha önce versiyon 0.11.0'da, ses durumlarına başvurmak için bir Momber.voice özniteliğile birlikte bir VoiceState sınıfı eklenmişti. Ancak kullanıcı için şeffaftı. Kitaplığın bellekten daha fazla tasarruf etmesini sağlamak amacıyla, ses durumu değişikliği artık daha görünür.

Ses özelliklerine erişmenin tek yolu Member.voice özelliğidir. Üyenin ses durumu yoksa bu özniteliğin yok olabileceğini unutmayın. 

Hızlı bir örnek yapalım;
```python
# önce
member.deaf
member.voice.voice_channel

# sonra
if member.voice:
    member.voice.deaf
    member.voice.channel
```

#### Kullanıcı ve Üye Türü Ayrımı

#### Kanal Tipi Bölme

#### Çeşitli Model Değişiklikleri

## Mesaj Gönderimi
Yapılan değişikliklerden biri, önceki ```Client.send_message``` ve ```Client.send_file``` işlevlerinin ```send()``` adı verilen tek bir yöntemde birleştirilmediydi.

Basitçe örnek verecek olursak;
```python 
# önce
await client.send_message(channel, "Hello")

# sonra
await client.send("Hello")
```
Tabiki bu yeni yöntem, eski ```send_message``` işlevlerinin desteklediği her şeyi destekler. Örneğin gömme mesajlar (Embed'ler)
```python
e = discord.Embed(title="foo")
await channel.send("Hello", embed=e)
```
Dosya göndermek ile iligil küçük bir uyarımız var, ancak bu işlevsellik birden fazla dosya ekini desteklemek için genişletildiğinden, artık tek bir dosya yüklemek için sözde adlandırılmış dosya çiftini kullanmanız gerekir.
```python
# önce 
await client.send_file(channel, "cool.png", filename="testing.png", content="Hello")

# sonra
await channel.send("Hello", file=discord.File("cool.png", "testing.png"))
```
Bu değişiklik birden çok dosya yüklemesini kolaylaştırmak içindi.
```python
my_files = [
    discord.File('cool.png', 'testing.png'),
    discord.File(some_fp, 'cool_filename.png'),
]

await channel.send('Resimleriniz:', files=my_files)
```

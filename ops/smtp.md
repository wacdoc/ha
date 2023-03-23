# Gina sabar aika saƙon SMTP naku

## gabatarwa

SMTP na iya siyan sabis kai tsaye daga masu siyar da girgije, kamar:

* [Amazon SES SMTP](https://docs.aws.amazon.com/ses/latest/dg/send-email-smtp.html)
* [Ali girgije email tura](https://www.alibabacloud.com/help/directmail/latest/three-mail-sending-methods)

Hakanan zaka iya gina sabar saƙon ku - unlimited aikawa, ƙarancin farashi gabaɗaya.

A ƙasa, muna nuna mataki-mataki yadda ake gina sabar saƙon mu.

## Zaɓin uwar garken

Sabar SMTP mai ɗaukar nauyin kai tana buƙatar IP na jama'a tare da bude tashoshin jiragen ruwa 25, 456, da 587.

Gizagizai da aka saba amfani da su sun toshe waɗannan tashoshin jiragen ruwa ta hanyar tsohuwa, kuma yana iya yiwuwa a buɗe su ta hanyar ba da odar aiki, amma yana da wahala sosai.

Ina ba da shawarar siye daga rundunar da ke buɗe waɗannan tashoshin jiragen ruwa kuma suna goyan bayan kafa sunayen yanki na baya.

Anan, ina ba da shawarar [Contabo](https://contabo.com) .

Contabo mai ba da sabis ne wanda ke zaune a Munich, Jamus, wanda aka kafa a cikin 2003 tare da farashi masu gasa.

Idan ka zaɓi Yuro a matsayin kudin siyan kuɗi, farashin zai zama mai rahusa (sabar da ke da ƙwaƙwalwar ajiyar 8GB da CPUs 4 tana kashe kusan yuan 529 a kowace shekara, kuma kuɗin shigarwa na farko kyauta ne na shekara guda).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/UoAQkwY.webp)

Lokacin yin oda, magana `prefer AMD` , kuma uwar garken tare da AMD CPU zai sami kyakkyawan aiki.

A cikin masu zuwa, zan ɗauki VPS na Contabo a matsayin misali don nuna yadda ake gina sabar saƙon ku.

## Tsarin tsarin Ubuntu

Tsarin aiki anan shine Ubuntu 22.04

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/smpIu1F.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/m7Mwjwr.webp)

Idan uwar garken akan ssh ya nuna `Welcome to TinyCore 13!` (kamar yadda aka nuna a cikin hoton da ke ƙasa), yana nufin cewa ba a shigar da tsarin ba tukuna. Da fatan za a cire haɗin ssh kuma jira na ƴan mintuna don sake shiga.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/-qKACz9.webp)

Lokacin da `Welcome to Ubuntu 22.04.1 LTS` ya bayyana, farawa ya cika, kuma zaku iya ci gaba da matakai masu zuwa.

### [Na zaɓi] Fara yanayin ci gaba

Wannan mataki na zaɓi ne.

Don dacewa, na sanya shigarwa da tsarin tsarin software na ubuntu a [github.com/wactax/ops.os/tree/main/ubuntu](https://github.com/wactax/ops.os/tree/main/ubuntu) .

Gudun umarni mai zuwa don shigarwa tare da dannawa ɗaya.

```
bash <(curl -s https://raw.githubusercontent.com/wactax/ops.os/main/ubuntu/boot.sh)
```

Masu amfani da Sinanci, da fatan za a yi amfani da umarni mai zuwa maimakon, kuma harshe, yankin lokaci, da sauransu za a saita ta atomatik.

```
CN=1 bash <(curl -s https://ghproxy.com/https://raw.githubusercontent.com/wactax/ops.os/main/ubuntu/boot.sh)
```

### Contabo yana kunna IPV6

Kunna IPV6 don haka SMTP zai iya aika imel tare da adiresoshin IPV6.

gyara `/etc/sysctl.conf`

Gyara ko ƙara layin masu zuwa

```
net.ipv6.conf.all.disable_ipv6 = 0
net.ipv6.conf.default.disable_ipv6 = 0
net.ipv6.conf.lo.disable_ipv6 = 0
```

Bi tare da [koyawan contabo: Ƙara haɗin IPv6 zuwa uwar garken ku](https://contabo.com/blog/adding-ipv6-connectivity-to-your-server/)

Shirya `/etc/netplan/01-netcfg.yaml` , ƙara 'yan layi kamar yadda aka nuna a cikin adadi da ke ƙasa (fayil ɗin tsoho na Contabo VPS ya riga ya sami waɗannan layin, kawai ba da amsa ba).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/5MEi41I.webp)

Sa'an nan `netplan apply` don sa gyaran da aka gyara ya yi tasiri.

Bayan tsarin ya yi nasara, zaku iya amfani da `curl 6.ipw.cn` don duba adireshin ipv6 na hanyar sadarwar ku ta waje.

## Rufe ops na ma'ajin saitin

```
git clone https://github.com/wactax/ops.soft.git
```

## Ƙirƙirar takardar shaidar SSL kyauta don sunan yankinku

Aika saƙo yana buƙatar takardar shaidar SSL don ɓoyewa da sa hannu.

Muna amfani da [acme.sh](https://github.com/acmesh-official/acme.sh) don samar da takaddun shaida.

acme.sh kayan aikin sa hannu ne mai sarrafa kansa mai tushe,

Shigar da sito ops.soft, gudu `./ssl.sh` , kuma za a ƙirƙiri babban fayil na `conf` a cikin **babban directory** .

Nemo mai ba da DNS ɗin ku daga [acme.sh dnsapi](https://github.com/acmesh-official/acme.sh/wiki/dnsapi) , gyara `conf/conf.sh` .

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/Qjq1C1i.webp)

Sannan gudanar da `./ssl.sh 123.com` don samar da takaddun shaida `123.com` da `*.123.com` don sunan yankinku.

Gudun farko zai shigar da [acme.sh](https://github.com/acmesh-official/acme.sh) ta atomatik kuma ya ƙara aikin da aka tsara don sabuntawa ta atomatik. Kuna iya ganin `crontab -l` , akwai irin wannan layi kamar haka.

```
52 0 * * * "/mnt/www/.acme.sh"/acme.sh --cron --home "/mnt/www/.acme.sh" > /dev/null
```

Hanya don takardar shaidar da aka samar wani abu ne kamar `/mnt/www/.acme.sh/123.com_ecc。`

Sabunta takaddun shaida zai kira rubutun `conf/reload/123.com.sh` , gyara wannan rubutun, zaku iya ƙara umarni kamar `nginx -s reload` don sabunta cache takardar shaidar aikace-aikace masu alaƙa.

## Gina uwar garken SMTP tare da chasquid

[chasquid](https://github.com/albertito/chasquid) buɗaɗɗen tushen sabar SMTP ce da aka rubuta cikin harshen Go.

A matsayin madadin tsoffin shirye-shiryen sabar sabar kamar Postfix da Sendmail, chasquid ya fi sauƙi kuma mai sauƙin amfani, kuma yana da sauƙin haɓakawa na sakandare.

Run `./chasquid/init.sh 123.com` za a shigar ta atomatik tare da dannawa ɗaya (maye gurbin 123.com tare da sunan yankin da kake aikawa).

## Sanya Sa hannun Imel DKIM

Ana amfani da DKIM don aika sa hannun imel don hana haruffa daga ɗaukar su azaman spam.

Bayan umarnin ya yi nasara, za a sa ka saita rikodin DKIM (kamar yadda aka nuna a ƙasa).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/LJWGsmI.webp)

Kawai ƙara rikodin TXT zuwa DNS ɗin ku (kamar yadda aka nuna a ƙasa).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/0szKWqV.webp)

## Duba matsayin sabis & rajistan ayyukan

 `systemctl status chasquid` Duba matsayin sabis.

Yanayin aiki na yau da kullun yana kamar yadda aka nuna a cikin hoton da ke ƙasa

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/CAwyY4E.webp)

 `grep chasquid /var/log/syslog` ko `journalctl -xeu chasquid` na iya duba log ɗin kuskure.

## Juya tsarin sunan yankin

Sunan yankin baya shine don ba da damar adireshin IP don warwarewa zuwa sunan yankin daidai.

Saita sunan yankin baya na iya hana imel daga tantance su azaman spam.

Lokacin da aka karɓi saƙon, uwar garken mai karɓa zai yi nazarin sunan yankin baya akan adireshin IP na sabar mai aikawa don tabbatar da ko uwar garken yana da ingantaccen sunan yankin baya.

Idan uwar garken aika ba shi da sunan yankin baya ko kuma idan sunan yankin baya bai dace da adireshin IP na sabar mai aikawa ba, uwar garken mai karɓa na iya gane imel ɗin a matsayin spam ko ƙin yarda da shi.

Ziyarci [https://my.contabo.com/rdns](https://my.contabo.com/rdns) kuma saita kamar yadda aka nuna a ƙasa

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/IIPdBk_.webp)

Bayan saita sunan yankin baya, tuna don saita ƙudurin gaba na sunan yankin ipv4 da ipv6 zuwa uwar garken.

## Shirya sunan mai masaukin baki na chasquid.conf

Gyara `conf/chasquid/chasquid.conf` zuwa ƙimar sunan yankin baya.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/6Fw4SQi.webp)

Sannan kunna `systemctl restart chasquid` don sake kunna sabis ɗin.

## Ajiye conf zuwa ma'ajiyar git

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/Fier9uv.webp)

Misali, Ina adana babban fayil ɗin conf zuwa tsarin github na kamar haka

Ƙirƙiri ɗakin ajiya mai zaman kansa da farko

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/ZSCT1t1.webp)

Shigar da kundin adireshi kuma aika zuwa sito

```
git init
git add .
git commit -m "init"
git branch -M main
git remote add origin git@github.com:wac-tax-key/conf.git
git push -u origin main
```

## Ƙara mai aikawa

gudu

```
chasquid-util user-add i@wac.tax
```

Za a iya ƙara mai aikawa

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/khHjLof.webp)

### Tabbatar cewa an saita kalmar wucewa daidai

```
chasquid-util authenticate i@wac.tax --password=xxxxxxx
```

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/e92JHXq.webp)

Bayan ƙara mai amfani, `chasquid/domains/wac.tax/users` za a sabunta, ku tuna ƙaddamar da shi zuwa sito.

## DNS ƙara rikodin SPF

SPF (Tsarin Manufofin Masu aikawa) fasaha ce ta tabbatar da imel da ake amfani da ita don hana zamba ta imel.

Yana tabbatar da ainihin mai aikawa da wasiku ta hanyar bincika cewa adireshin IP ɗin mai aikawa ya dace da bayanan DNS na sunan yankin da yake ikirarin shi ne, yana hana masu zamba daga aika saƙon imel na bogi.

Ƙara bayanan SPF na iya hana imel daga gano su azaman spam kamar yadda zai yiwu.

Idan uwar garken sunan yankinku baya goyan bayan nau'in SPF, kawai ƙara rikodin nau'in TXT.

Misali, SPF na `wac.tax` shine kamar haka

`v=spf1 a mx include:_spf.wac.tax include:_spf.google.com ~all`

SPF don `_spf.wac.tax`

`v=spf1 a:smtp.wac.tax ~all`

Lura cewa ina `include:_spf.google.com` anan, wannan saboda zan saita `i@wac.tax` azaman adireshin aikawa a cikin akwatin wasiku na Google daga baya.

## Tsarin DNS na DMARC

DMRC ita ce gajarta (Tabbacin Saƙo na tushen yanki, Rahoto & Amincewa).

Ana amfani da shi don kama bounces SPF (wataƙila kurakuran daidaitawa ya haifar da shi, ko wani yana riya cewa kai ne aika spam).

Ƙara rikodin TXT `_dmarc` ,

Abinda ke ciki shine kamar haka

```
v=DMARC1; p=quarantine; fo=1; ruf=mailto:ruf@wac.tax; rua=mailto:rua@wac.tax
```

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/k44P7O3.webp)

Ma'anar kowace siga shine kamar haka

### p (Manufa)

Yana Nuna yadda ake sarrafa imel ɗin da suka gaza SPF (Tsarin Manufofin Aika) ko tabbatarwa DKIM (DomainKeys Identified Mail). Ana iya saita ma'aunin p zuwa ɗaya daga cikin ƙima guda uku:

* Babu ko ɗaya: Ba a ɗauki mataki ba, kawai sakamakon tabbatarwa ana mayar da shi ga mai aikawa ta hanyar hanyar ba da rahoton imel.
* Keɓewa: Saka saƙon da bai wuce tabbatarwa ba cikin babban fayil ɗin spam, amma ba zai ƙi saƙon kai tsaye ba.
* reject: Karɓar imel kai tsaye waɗanda suka gaza tabbatarwa.

### fo (Zaɓuɓɓukan gazawa)

Yana ƙayyadaddun adadin bayanan da tsarin bayar da rahoto ya dawo. Ana iya saita shi zuwa ɗaya daga cikin dabi'u masu zuwa:

* 0: Bayar da sakamakon tabbatarwa ga duk saƙonni
* 1: Ba da rahoton saƙon da ya gaza tabbatarwa kawai
* d: Ba da rahoton gazawar tantance sunan yankin kawai
* s: kawai bayar da rahoton gazawar tabbatarwar SPF
* l: Kawai bayar da rahoton gazawar tabbatarwar DKIM

### rufa & rufa

* rua (Rahoton URI don Rahoton Tara): Adireshin imel don karɓar tara rahotanni
* ruf (Rahoton URI don rahotannin Forensic): adireshin imel don karɓar cikakkun rahotanni

## Ƙara bayanan MX don tura imel zuwa Google Mail

Saboda ban sami akwatin saƙo na kamfani kyauta wanda ke goyan bayan adiresoshin duniya (Catch-All, na iya karɓar duk wani imel da aka aika zuwa wannan sunan yankin, ba tare da hani akan prefixes ba), na yi amfani da chasquid don tura duk imel zuwa akwatin saƙo na Gmail.

**Idan kuna da akwatin saƙon kasuwanci da ake biya na ku, don Allah kar a gyara MX kuma ku tsallake wannan matakin.**

Shirya `conf/chasquid/domains/wac.tax/aliases` , saita akwatin saƙo mai aikawa

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/OBDl2gw.webp)

`*` yana nuna duk imel, `i` ne prefix ɗin adireshin imel na mai amfani da aka ƙirƙira a sama. Don tura wasiku, kowane mai amfani yana buƙatar ƙara layi.

Sannan ƙara rikodin MX (Na nuna kai tsaye zuwa adireshin sunan yankin baya a nan, kamar yadda aka nuna a layin farko a cikin adadi a ƙasa).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/7__KrU8.webp)

Bayan daidaitawar ta cika, zaku iya amfani da wasu adiresoshin imel don aika imel zuwa `i@wac.tax` da `any123@wac.tax` don ganin ko kuna iya karɓar imel a cikin Gmel.

Idan ba haka ba, duba log ɗin chasquid ( `grep chasquid /var/log/syslog` ).

## Aika imel zuwa i@wac.tax tare da Google Mail

Bayan Google Mail ya karɓi wasiƙar, a zahiri ina fatan in ba da amsa da `i@wac.tax` maimakon i.wac.tax@gmail.com.

Ziyarci [https://mail.google.com/mail/u/1/#settings/accounts](https://mail.google.com/mail/u/1/#settings/accounts) kuma danna "Ƙara wani adireshin imel".

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/PAvyE3C.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/_OgLsPT.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/XIUf6Dc.webp)

Sannan, shigar da lambar tabbatarwa da aka karɓa ta imel ɗin da aka tura zuwa gare ta.

A ƙarshe, ana iya saita shi azaman adireshin mai aikawa na asali (tare da zaɓin amsa da adireshin iri ɗaya).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/a95dO60.webp)

Ta wannan hanyar, mun kammala kafa sabar saƙon SMTP kuma a lokaci guda muna amfani da Google Mail don aikawa da karɓar imel.

## Aika imel ɗin gwaji don bincika ko daidaitawar ta yi nasara

Shigar da `ops/chasquid`

Gudun `direnv allow` shigar da abubuwan dogaro (an shigar da direnv a cikin tsarin fara maɓallin maɓalli ɗaya na baya kuma an ƙara ƙugiya zuwa harsashi)

sannan gudu

```
user=i@wac.tax pass=xxxx to=iuser.link@gmail.com ./sendmail.coffee
```

Ma'anar sigogi shine kamar haka

* mai amfani: SMTP sunan mai amfani
* Pass: SMTP kalmar sirri
* zuwa: mai karɓa

Kuna iya aika imel ɗin gwaji.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/ae1iWyM.webp)

Ana ba da shawarar yin amfani da Gmel don karɓar imel ɗin gwaji don bincika ko daidaitawar sun yi nasara.

### TLS daidaitaccen ɓoyewa

Kamar yadda aka nuna a cikin hoton da ke ƙasa, akwai wannan ƙaramin kulle, wanda ke nufin cewa an sami nasarar kunna takardar shaidar SSL.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/SrdbAwh.webp)

Sannan danna "Nuna Asalin Imel"

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/qQQsdxg.webp)

### DKIM

Kamar yadda aka nuna a hoton da ke ƙasa, ainihin shafin saƙo na Gmail yana nuna DKIM, wanda ke nufin cewa tsarin DKIM ya yi nasara.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/an6aXK6.webp)

Duba abin da aka karɓa a cikin taken ainihin imel ɗin, kuma za ku ga cewa adireshin mai aikawa IPV6 ne, wanda ke nufin cewa IPV6 kuma an daidaita shi cikin nasara.

---
title:
  "Kompüter Elmləri Nəzəriyyəsindən Real İş Mühitinə: Arxitektura və Performans
  (Hissə 2)"
author: murad-nurubayli
description:
  "Clean Code, SOLID prinsipləri, dizayn pattern-ləri, arxitektura və performans
  qərarlarının real iş mühitindəki əhəmiyyəti."
date: 2026-05-25
categories: ["Təhsil", "Arxitektura"]
resource: true
resource_audiences: ["Universitet Tələbələri", "Proqramçılar"]
---

_Bu məqalə [[mühəndislik]] düşüncəsi haqqında silsilənin ikinci hissəsidir.
Birinci hissədə biz [[sintaksis]] əzbərləməklə sistem dizaynı qurmaq arasındakı
fərqi, [[abstraksiya]]ları, modelləri və [[obyekt-yönümlü proqramlaşdırma]]/
[[funksional proqramlaşdırma]] kimi [[paradiqma]]ları incələdik. İndi isə həmin
düşüncə tərzinin real [[kod bazası]]na, arxitekturaya və performansa necə təsir
etdiyinə baxaq._

---

## **V bölüm — [[Clean Code]], [[SOLID]], high [[cohesion]] və low [[coupling]]: yaxşı görünən kod yox, idarə oluna bilən sistem**

[[Proqramlaşdırma]] haqqında danışanda “yaxşı kod” ifadəsi çox tez-tez
işlədilir. Amma bu ifadə o qədər çox təkrar olunur ki, bir müddətdən sonra
mənasını itirməyə başlayır. Bəziləri üçün yaxşı kod səliqəli formatlanmış
koddur. Bəziləri üçün qısa koddur. Bəziləri üçün pattern-lərlə dolu koddur.
Bəziləri üçün isə sadəcə işləyən koddur. Real iş mühitində bunların heç biri
təkbaşına kifayət etmir. Çünki yaxşı kod anlayışı təkcə görünüşlə bağlı deyil.
Onun əsas dəyəri idarə olunma qabiliyyətindədir.

Bu mövzuya görə Clean Code, SOLID, high cohesion, low coupling kimi anlayışlar
illərdir proqram mühəndisliyinin mərkəzindədir. Amma praktikada bu anlayışların
iki fərqli aqibəti olur. Ya onlar həddindən artıq romantikləşdirilir, sanki hər
problemi avtomatik həll edən sehrli düsturlardır; ya da tam əksinə, “kitabi
söhbətlər” kimi kənara itələnir. Hər iki yanaşma səhvdir. Çünki bu prinsiplər nə
kod estetikası klubunun qaydalarıdır, nə də yalnız akademik müzakirə mövzusudur.
Onlar uzunömürlü sistemlərdə dəyişiklik xərcini azaltmaq, təsir radiusunu
daraltmaq və texniki qərarları daha şəffaf etmək üçün yaranıb.

Ən vacib məqam da budur: bu prinsipləri başa düşmədən yazılan kod bəzən ilk gün
özünü normal aparır, amma sistem böyüdükcə bir növ daxildən ağırlaşmağa
başlayır. Hər yeni dəyişiklik əvvəlkindən daha riskli olur. Kiçik bir düzəliş
gözlənilməz yerlərdə qırılma yaradır. Bir modulun içində baş verən dəyişiklik
başqa beş modula yayılır. Kod bazası işlək qalır, amma çevikliyini itirir. Bu
mərhələdə problem “pis proqramçılar” deyil. Problem odur ki, sistemin daxili
quruluşu dəyişiklik üçün baha formalaşıb.

### **Clean Code estetik qayda toplusu deyil**

Clean Code çox vaxt adından dolayı yanlış başa düşülür. İnsanlar elə düşünür ki,
bu mövzu əsasən kodun oxunaqlı görünməsi, səliqəli adlandırılması və
formatlanması ilə bağlıdır. Bunlar, əlbəttə, vacibdir. Amma məsələ bundan
qat-qat dərindir.

Kodun “clean” olması ilk növbədə onun niyyətini aydın ifadə etməsi ilə bağlıdır.
Yəni kod yalnız işləməməli, həm də nə etdiyini, niyə etdiyini və harada
məsuliyyət daşıdığını göstərməlidir. Bu, çox praktik dəyərdir. Çünki real
sistemdə kodu ən çox yazan adam yox, onu sonradan oxuyan, dəyişən, səhvini
axtaran və genişləndirən adam görür. Yaxşı kodun əsas keyfiyyətlərindən biri də
budur: o, başqa bir mühəndisin zehnində lazımsız yük yaratmır.

Burada sadəlik anlayışı ön plana çıxır. Amma sadəlik heç vaxt uşaqlıq
səviyyəsində bəsitlik demək deyil. Əsl sadəlik onu yazanın çox düşünməsi
nəticəsində yaranır. Məsuliyyətlər qarışmayanda, adlar semantik dəyər daşıyanda,
[[yan təsir]]lər gizlənməyəndə, control flow lazımsız dolaşıqlıq yaratmayanda
sistem daha rahat oxunur. Bu oxunaqlılıq estetik rahatlıq üçün deyil; o,
qərarvermə yükünü azaltmaq üçündür.

Əksinə, “dirty” kodun əsas problemi çox vaxt onun çirkin görünməsi deyil. Onun
problemi zehni duman yaratmasıdır. Məsələn, bir metodun adı bir şey deyir, amma
daxilində beş başqa məsələ həll olunur. Bir [[service]] [[business logic]]
daşımalı olduğu halda həm mapper, həm [[cache]] manager, həm [[authorization]]
checker, həm də [[repository]] koordinasiyaçısına çevrilib. [[Controller]]
[[HTTP]] sərhədi olmalıykən [[domain]] qərarları ilə doludur. Bir [[entity]] həm
persistence modeli, həm validation qaydası, həm presentation formatı kimi
istifadə olunur. Bu qarışıqlıq artıq sadəcə “pis üslub” deyil. Bu, sistemin özü
haqqında aydın düşünməyi çətinləşdirir.

Ona görə Clean Code-un dəyəri kodu gözəl göstərməkdə deyil. Onun dəyəri sistemi
daha düşünülə bilən etməkdədir.

### **SOLID niyə bu qədər yayılıb?**

SOLID prinsiplərinin bu qədər məşhur olmasının səbəbi onların nəzəri olaraq
gözəl görünməsi deyil. Bu prinsiplər eyni tip problemlərin təkrar-təkrar
yaşanmasından doğub. Yəni onlar idealist dizayn oyunu deyil, istehsal mühitində
görünən ağrıların ümumiləşdirilmiş formasıdır.

Amma SOLID-in problemi də məhz populyarlığından başlayır. Çox adam bu
prinsipləri ad səviyyəsində öyrənir, mahiyyət səviyyəsində yox. Nəticədə SOLID
bəzən sistemə yön vermək əvəzinə, dekorativ qayda siyahısına çevrilir. Bir
layihədə yüzlərlə interface görüb düşünmək olar ki, burada [[DIP]] tətbiq
olunub. Çox sayda kiçik [[class]] görüb demək olar ki, [[SRP]] qorunub. Lakin
bir az dərinə baxanda aydın olur ki, məsuliyyətlər yenə də dumanlıdır,
dəyişiklik yenə də hər tərəfə yayılır və abstraksiyalar həqiqi sərhəd yox,
formal qat rolunu oynayır.

Bu səbəbdən SOLID-i hərf-hərf tətbiq olunan resept kimi yox, sistemdə dəyişiklik
gərginliyinin harada toplandığını anlamaq üçün bir lens kimi görmək daha
doğrudur.

### **Single Responsibility Principle ən çox yanlış izah olunan prinsipdir**

SRP çox vaxt “bir class bir iş görməlidir” kimi sadələşdirilir. Bu cümlə tam
səhv olmasa da, çox təhlükəli dərəcədə natamamdır. Çünki “bir iş” ifadəsi
həddindən artıq qeyri-dəqiqdir. Bir sistemdə nəyin “bir iş” sayıldığı
kontekstdən asılıdır.

SRP-nin daha yetkin izahı budur: bir modulun dəyişməsi üçün bir əsas səbəb
olmalıdır. Yəni eyni vahidin içinə bir-biri ilə əlaqəsi zəif olan müxtəlif
dəyişiklik səbəbləri yığılmamalıdır. Bu, çox vacib fərqdir. Çünki məsələ “metod
sayı az olsun” və ya “class kiçik olsun” deyil. Məsələ budur ki, fərqli
istiqamətdən gələn dəyişikliklər eyni yerdə toqquşmasın.

Məsələn, bir komponent həm business qaydalarını hesablayır, həm email formatını
qurur, həm database yazır, həm də [[audit log]] yaradırsa, problem təkcə onun
böyük olması deyil. Problem odur ki, bu vahidə müxtəlif növ dəyişikliklər
toxunacaq. Sabah business qaydası dəyişəcək, o biri gün email formatı
yenilənəcək, sonra persistence strategiyası dəyişəcək, daha sonra audit tələbi
artacaq. Hamısı eyni yerdə yaşayırsa, sistemin içində gərginlik yığılır.

SRP-nin real gücü də buradadır. O, sistemi xırda hissələrə bölmək üçün yox,
dəyişiklik enerjisini düzgün sahələrə yönəltmək üçündür.

### **Open/Closed Principle genişlənmə ilə sərtliyin arasındakı tarazlıqdır**

[[OCP]] də tez-tez şüar formasında qalır. “Kod dəyişiklik üçün bağlı, genişlənmə
üçün açıq olmalıdır” cümləsi gözəl səslənir, amma kontekstsiz qalanda demək olar
ki, heç nə ifadə etmir. Praktikada bu prinsipin mənası ondan ibarətdir ki, sabit
məntiqin üzərinə yeni davranış əlavə etmək üçün həmişə mövcud kodu söküb yenidən
qurmaq məcburiyyəti yaranmasın.

Amma burada da mühəndislik hissi lazımdır. Çünki OCP-ni səhv başa düşən
komandalar bəzən hələ mövcud olmayan gələcəklər üçün nəhəng extension point-lər
qururlar. Nəticədə sistem həqiqi çevik deyil, sadəcə generik görünən bir
mexanizmə çevrilir. Belə kod ilk baxışda “çox professional” görünür, amma
əslində reallıqdan uzaq abstraksiyalar daşıyır.

OCP ən yaxşı o vaxt işləyir ki, sistemdə həqiqətən təkrarlanan dəyişiklik oxları
görünür. Məsələn, fərqli ödəniş provayderləri, dəyişən qiymət hesablamaları,
müxtəlif notification kanalları, fərqli scoring strategiyaları. Bu cür sahələrdə
davranışı extension vasitəsilə genişləndirmək doğrudan da dəyər yarada bilər.
Amma hər yeri gələcəkdə bəlkə lazım olar deyə abstraktlaşdırmaq sistemi
gücləndirmir. Sadəcə onu daha ağır edir.

Burada yenə eyni nəticəyə gəlirik: prinsipin özü doğru olsa da, onun faydası
yalnız kontekstdə açılır.

### **Liskov Substitution Principle sintaksisdən çox etibar məsələsidir**

[[LSP]] adətən [[inheritance]] müzakirələrində çəkilir, amma onun real dəyəri
“alt sinif üst sinifi əvəz edə bilməlidir” cümləsindən daha dərindir. Bu prinsip
əslində müqavilə sabitliyi ilə bağlıdır. Yəni bir abstraksiyaya etibar
edirsənsə, onun müxtəlif implementasiyaları sənin gözlədiyin davranış sərhədini
qırmamalıdır.

Bu, çox nəzəri görünə bilər, amma real iş mühitində çox praktikdir. Məsələn, bir
repository interfeysi var və onun birdən çox implementasiyası mövcuddur. Əgər bu
implementasiyalardan biri null qaytarır, digəri exception atır, üçüncüsü səssiz
fallback edir, dördüncüsü eager load davranışı ilə tam başqa cost yaradırsa,
burada məsələ sadəcə [[polymorphism]] deyil. Burada abstraksiyaya güvən
sarsılır.

Eyni problem API ([[tətbiqi proqramlaşdırma interfeysi]]) [[contract]]-larda,
service interface-lərində, [[strategy pattern]] implementasiyalarında, hətta
cache provider-larda da yaşana bilər. Kağız üzərində “əvəzlənə bilən” görünən
komponentlər əslində eyni semantik müqaviləni daşımırsa, sistem davranışı
sürprizlərlə dolur.

LSP-nin bu tərəfi çox vacibdir. Çünki yaxşı dizayn yalnız hissələri ayırmaqla
yaranmır. O hissələrin davranış sərhədləri də etibarlı olmalıdır.

### **Interface Segregation Principle və Dependency Inversion Principle formalizm üçün deyil**

[[ISP]] və DIP də bəzən müəmmalı prinsiplər kimi təqdim olunur, xüsusilə yeni
başlayanlar üçün. Amma real iş mühitində onların kökündə çox sadə bir fikir
yatır: asılılıqlar mümkün qədər dəqiq və məqsədyönlü olmalıdır.

Bir modulun ehtiyac duymadığı funksionallıqla yüklənməsi onun zehni yükünü
artırır. Bir interfeys çox şey təklif edirsə, onu istifadə edənlər də lazımsız
seçimlərlə qarşılaşır. Bu, təkcə dizayn səliqəsi məsələsi deyil. Zamanla
sistemdəki asılılıqların sərhədi bulanır. Hər kəs hər şeydən az-çox xəbərdar
olur. Nəticədə lokal dəyişikliklər belə daha geniş təsir yaratmağa başlayır.

DIP də eyni xəttdə dəyərlidir. Burada məqsəd interface kolleksiyası toplamaq
deyil. Məqsəd yüksək səviyyəli qaydaların aşağı səviyyəli texniki detallara
bağlanmamasıdır. Yəni biznes qərarı database texnologiyasının konkret
detalından, cache provider seçiminin spesifikasından, [[framework]]-ün birbaşa
mexanizmindən asılı qalmamalıdır. Bu ayrım düzgün qurulanda texniki
dəyişikliklər business məntiqini daha az silkələyir.

Amma bunun da formal versiyası var və o çox zərərlidir. Hər class üçün interface
yazmaq DIP deyil. Hər dependency-ni abstraktlaşdırmaq da mature design demək
deyil. Əgər sistemdə real dəyişiklik nöqtəsi, test sərhədi və ya texnoloji
dəyişmə ehtimalı yoxdursa, abstraksiyanın özü əlavə yükə çevrilə bilər. Bu halda
prinsip tətbiq edilmir, təqlid olunur.

### **High cohesion sistemi içəridən gücləndirir**

Cohesion anlayışı çox vaxt coupling qədər diqqət görmür, halbuki sistem
keyfiyyəti üçün bəlkə də daha səssiz, amma daha dərin göstəricidir. High
cohesion o deməkdir ki, bir modulun daxilində yerləşən hissələr məna baxımından
bir-birinə yaxındır. Onlar təsadüfi yox, təbii birlik təşkil edir.

Bu, çox sadə görünə bilər, amma əslində sistemin daxili dürüstlüyü bununla
ölçülür. Əgər bir class, service və ya modul daxilindəki şeylər eyni mövzunun
fərqli tərəfləridirsə, onu başa düşmək və dəyişmək daha asan olur. Orada zehni
konsentrasiya pozulmur. Mühəndis bir classi açanda təxminən nə gözləməli
olduğunu bilir.

Low cohesion isə fərqli məntiq sahələrinin eyni qabın içinə yığılmasıdır. Bunun
ən geniş yayılmış forması “utility culture”dir. Müxtəlif yerlərə aid
davranışların eyni service və ya helper altında toplanması qısa müddətdə sürətli
görünə bilər, amma zamanla sistemi tanınmaz edir. Çünki həmin vahid artıq öz
mövzusu ilə seçilmir; o, sadəcə əl altında olan boş konteynerə çevrilir.

High cohesion-in praktik üstünlüyü odur ki, sistemin daxilində semantik xəritə
yaradır. Hər hissənin nəyi daşıdığı aydın görünür. Bu da [[refactoring]], test
yazmaq, ownership müəyyənləşdirmək və gələcək genişlənmələri planlamaq üçün çox
vacibdir.

### **Low coupling çeviklik və təhlükəsizlik arasındakı gizli körpüdür**

Coupling çox vaxt yalnız texniki asılılıq kimi düşünülür, amma onun real təsiri
daha genişdir. Bir-birinə çox sıx bağlı modullar yalnız çətin dəyişmir; onlar
eyni zamanda bir-birinin riskini daşıyır. Yəni bir hissədəki qərar və ya səhv
asanlıqla digər hissəyə keçir.

Low coupling sistemdə sərhəd hissini qoruyur. Bir komponentin davranışı və
daxili quruluşu dəyişəndə bunun təsiri mümkün qədər lokal qalmalıdır. Bu,
xüsusilə böyük komandalarda və uzunömürlü məhsullarda son dərəcə dəyərlidir.
Çünki sistem yalnız koddan ibarət deyil; o, həm də insanlar arası koordinasiya
modelidir. Çox sıx coupling texniki problem olmaqla yanaşı, komanda daxilində
qərarvermə və inkişaf sürəti probleminə də çevrilir.

Burada coupling-in yalnız compile-time və ya direct dependency səviyyəsində
deyil, semantik səviyyədə də izlənməsi vacibdir. İki modul bir-birinin daxili
davranışına həddindən artıq güvənirsə, hətta formal interface olsa belə,
coupling yüksək ola bilər. Eyni şəkildə, eyni business qaydasının müxtəlif
yerlərdə səpələnməsi görünməyən coupling yaradır. Çünki o qayda dəyişəndə hamısı
birlikdə dəyişməlidir.

Low coupling buna görə sadəcə texniki “best practice” deyil. Bu, dəyişiklik
radiusunu daraltmaq və sistemin içində riskin yayılma sürətini azaltmaq
üsuludur.

### **Naming, sərhəd və yan təsirlər: yaxşı kodun sakit təməli**

Clean Code və SOLID mövzusunda çox vaxt böyük prinsiplər danışılır, amma
sistemin gündəlik sağlamlığını qoruyan bir neçə daha sakit mövzu da var.
Onlardan biri naming-dir. Adlandırma çox adamın düşündüyündən daha mühüm
məsələdir. Çünki adlar yalnız etiket deyil; onlar modelin dilidir. Əgər
sistemdəki adlar domain-lə uyğun gəlmirsə, orada düşüncə ilə kod arasında
sürtünmə yaranır.

Digər vacib məqam sərhədlərin aydınlığıdır. Hər qatın, hər modulun, hər
service-in daxil olmaq və çıxmaq nöqtələri nə qədər aydın olsa, sistem bir o
qədər proqnozlaşdırıla bilən olur. Bu aydınlıq olmadan hətta yaxşı niyyətlə
yazılmış kod da tez qarışa bilər.

Yan təsirlər də eyni dərəcədə vacibdir. Bir funksiya yalnız məlumat qaytarır
kimi görünür, amma daxilində state dəyişdirir, log yazır, cache yeniləyir və ya
network çağırışı edirsə, bu artıq oxucu ilə sistem arasında gizli müqavilə
yaradır. Belə gizli müqavilələr zamanla bug və anlaşılmazlıq istehsal edir.
Güclü mühəndislik mümkün qədər explicit davranışı üstün tutur. Bu, functional
yanaşmanın da ən dəyərli dərslərindən biridir və Clean Code ilə çox yaxşı
kəsişir.

### **Yaxşı kodun həqiqi məqsədi dəyişiklik dəyərini aşağı salmaqdır**

Bu hissənin əsas nəticəsi burada toplanır. Clean Code, SOLID, high cohesion və
low coupling kodu “gözəl” etmək üçün yox, sistemi dəyişiklik qarşısında daha
dözümlü etmək üçün lazımdır. Yaxşı kodun dəyəri onun ilk gün necə görünməsi ilə
yox, altıncı ayda necə davranması ilə ölçülür.

Yeni business qaydası gələndə sistem qırılmadan uyğunlaşa bilirsə, bu yaxşı
dizayndır. Bir komanda üzvü başqa komandanın kodunu açanda oradakı məntiqi rahat
izləyə bilirsə, bu yaxşı dizayndır. Bir feature genişlənəndə mövcud kodu tam
söküb yenidən qurmağa ehtiyac yaranmırsa, bu yaxşı dizayndır. Kiçik bir
dəyişiklik bütün sistemi silkələmir, yalnız aid olduğu zonada qalırsa, bu yaxşı
dizayndır.

Mühəndislik prinsiplərinin real dəyəri də məhz bu gündəlik müqavimətdə ortaya
çıxır. Onlar kodu “ideal” etməyə yox, sistemi uzun müddət işlək, aydın və
etibarlı saxlamağa xidmət edir.

## **VI bölüm — [[Design pattern]], [[architectural pattern]] və [[architectural style]]: eyni sözlər kimi görünən, amma eyni səviyyədə yaşamayan anlayışlar**

Proqram mühəndisliyində ən çox qarışdırılan mövzulardan biri terminlərin özü
olur. Maraqlısı da budur ki, bu qarışıqlıq bəzən sırf söz problemi kimi görünür,
amma əslində düşüncə problemidir. İnsan design pattern, [[architecture]],
architectural pattern, architectural style, [[MVC]], [[clean architecture]],
[[hexagonal]], [[microservices]], [[REST]], layered architecture kimi
anlayışları eyni səbətdə düşünməyə başlayanda, sistem haqqında qərarlar da
bulanıqlaşır. Çünki fərqli miqyasda olan alətləri sanki eyni tip seçimlər imiş
kimi istifadə etməyə çalışır.

Bu qarışıqlığın nəticəsi real iş mühitində çox aydın hiss olunur. Komanda “bizdə
arxitektura var” deyir, amma əslində yalnız qovluq strukturu var. Biri “MVC
istifadə edirik” deyir, amma bu, sistemin yalnız presentation qatına aid olur.
Başqası “pattern tətbiq etmişik” deyir, amma tətbiq olunan şey konkret bir
obyekt əməkdaşlığına aid deyil, daha geniş application structuring qərarıdır.
Digəri “bizim arxitekturamız microservice-dir” deyir, halbuki microservice
yanaşması sistemin bütün daxili dizaynını avtomatik həll etmir. Beləcə terminlər
çoxalır, aydınlıq isə azalır.

Kompüter elmləri nəzəriyyəsindən real iş mühitinə keçiddə bu cür fərqləri düzgün
hiss etmək çox vacibdir. Çünki güclü mühəndislik yalnız texniki vasitələri
tanımaq deyil, onların hansı səviyyədə işlədiyini də ayırd edə bilməkdir. Hər
anlayışın öz miqyası, öz məqsədi və öz həll etdiyi problem tipi var. Bunlar
qarışanda sistem ya həddindən artıq sadələşdirilir, ya da lazımsız dərəcədə
mistikləşdirilir.

### **Pattern anlayışının həqiqi dəyəri**

Pattern-lər proqramlaşdırma dünyasında çox vaxt “hazır həll” kimi təqdim olunur.
Bu təqdimat rahatdır, amma yarımçıqdır. Pattern əslində copy-paste ediləcək bir
şablon deyil. O, təkrarlanan problemin arxasındakı struktur məntiqinin
adlandırılmış formasıdır. Yəni pattern-in dəyəri konkret kod parçasında deyil,
müəyyən tip problemi tanımaq və ona artıq düşünülmüş struktur reaksiyası vermək
imkanı yaratmasındadır.

Bu baxımdan design pattern-lər daha lokal səviyyədə işləyir. Onlar adətən
siniflər, obyektlər, məsuliyyət bölgüsü və əməkdaşlıq mexanizmləri səviyyəsində
kömək edir. Strategy, Factory Method, Adapter, Decorator, Observer, Composite
kimi pattern-lər sistemin ümumi taleyini təkbaşına həll etmir. Onlar daha çox
lokal mürəkkəbliyi idarə etmək üçün düşüncə aləti rolunu oynayır.

Məsələn, Strategy pattern o halda faydalıdır ki, eyni davranış ailəsinin
müxtəlif variantlarını sərt [[if]]-else blokları ilə idarə etmək əvəzinə, onları
ayrılmış strategiyalar kimi modelləşdirirsən. Decorator o halda dəyər yaradır
ki, davranışı inheritance zənciri yaratmadan mərhələli şəkildə genişləndirmək
istəyirsən. Adapter fərqli interfeyslər arasında uyğunluq körpüsü qurur. Factory
object creation məsuliyyətini çağıran tərəfdən ayırır. Bunlar çox praktik
şeylərdir, amma onların miqyası lokaldır. Onlar sistemin bütöv memarlığını təyin
etmir.

Ən böyük səhvlərdən biri də burada yaranır: pattern bilmək ilə pattern-dən
düzgün istifadə etmək eyni şey deyil. Bir çox layihədə pattern-lər problem
görünməzdən əvvəl tətbiq olunur. Sanki pattern istifadə etmək peşəkarlığın
əlamətidir. Halbuki pattern yalnız o zaman dəyər yaradır ki, o, həqiqətən
görünən bir gərginliyi yüngülləşdirsin. Əks halda pattern həll deyil, əlavə
formalizmə çevrilir.

### **Design pattern-lər lokal qərarlardır, arxitektura isə istiqamət qərarıdır**

Bu fərqi düzgün hiss etmək vacibdir. Design pattern çox vaxt sistemin müəyyən
bir hissəsində təkrarlanan struktur problemi həll edir. Arxitektura isə sistemin
əsas quruluşunu, məsuliyyət sərhədlərini, dependency istiqamətlərini, məlumat
[[axın]]ını və zamanla genişlənmə formasını müəyyən edir.

Bu səbəbdən arxitekturanı pattern-lə eyniləşdirmək mümkün deyil. Pattern bir
otağın içindəki mebel düzümünə bənzəyirsə, arxitektura bütöv binanın necə təşkil
olunduğu ilə bağlıdır. Hər ikisi vacibdir, amma eyni səviyyədə deyil.

Real iş mühitində bu fərqi hiss etməyən komanda çox vaxt yanlış yerdə
optimallaşdırma edir. Məsələn, sistemin modul sərhədləri zəifdir, business logic
presentation qatına sızır, data access qaydaları hər yerdə təkrarlanır, amma
komanda buna baxmaq əvəzinə lokal design pattern-lərlə “təmizlik” yaratmağa
çalışır. Nəticədə daxili problem qalır, yalnız üzərinə struktur görüntüsü əlavə
olunur.

Başqa tərəfdən, arxitektura problemi olan yerdə design pattern-lər kömək etməyə
bilər. Əgər dependency istiqamətləri qarışıbsa, bütün sistem [[ORM]]
obyektlərinin ətrafında fırlanırsa, domain qaydaları transaction sərhədləri ilə
çarpazlaşıbsa, burada Adapter və ya Factory tətbiq etməklə məsələ həll olunmur.
Burada daha yuxarı səviyyəli düşüncə lazımdır.

### **Architectural pattern daha geniş təkrarlanan təşkil formasıdır**

Architectural pattern anlayışı design pattern-dən daha böyük miqyasda işləyir.
Burada artıq məsələ tək obyekt əməkdaşlığı deyil, sistem hissələrinin bir-biri
ilə necə təşkil olunmasıdır. Layered architecture, Hexagonal Architecture, Clean
Architecture, Pipes and Filters, CQRS kimi yanaşmalar bu səviyyədə düşünülür.
Bunlar sistemin hansı hissələrinin hansı məsuliyyət daşıdığını, hansı dependency
axınının qəbul edildiyini və texniki detalların business qaydalardan necə
ayrıldığını formalaşdırır.

Məsələn, layered architecture klassik olaraq presentation, application, domain,
data access kimi qatlar arasında məsuliyyət bölgüsü qurmağa çalışır. Hexagonal
yanaşma domain-i mərkəzdə saxlayıb xarici sistemlərlə port-adapter sərhədləri
qurur. Clean Architecture da dependency-lərin daxil istiqamətdə axmasını,
business qaydalarının texniki detalların təsirindən qorunmasını hədəfləyir. CQRS
isə oxu və yazı məsuliyyətlərini ayrı düşünərək bəzi sistemlərdə miqyas və
[[model]] aydınlığı yarada bilir.

Bunların hamısı bir dizayn pattern-i kimi lokal problem həll etmir. Onlar daha
geniş təşkil prinsipidir. Hətta bəzən eyni sistemdə bir neçə design pattern
istifadə olunsa da, hamısı bir architectural pattern sərhədində yaşayır.

Burada vacib bir incəlik də var: architectural pattern seçmək sistemi avtomatik
yaxşı etmir. Bir çox komanda yalnız terminoloji səviyyədə “clean architecture”
və ya “hexagonal” danışır, amma real dependency axını yenə də xaricdən içəri
yox, içəridən xaricə qarışıq gedir. Controller-lər application service-lərlə
birlikdə domain qərarı verir, infrastructure qatında yazılmalı şeylər business
logic-i təyin edir, interface-lər sırf formalizm naminə yaradılır. Kağız
üzərində pattern seçilib, amma davranış səviyyəsində o pattern-in fəlsəfəsi
yaşamır.

Yəni architectural pattern qovluq strukturu deyil. O, sistemin hansı
gərginliklərə qarşı necə mövqe tutduğudur.

### **Architectural style daha da yuxarı səviyyəli məhdudiyyətlər toplusudur**

Architectural style anlayışı bir qədər də genişdir. Burada artıq konkret daxili
təşkilat modelindən çox, sistemin ümumi forması və ünsiyyət qaydaları önə çıxır.
Client-server, monolith, [[modular monolith]], microservices, [[event-driven]],
pipe-and-filter, REST kimi yanaşmalar adətən architectural style kimi düşünülür.
Onlar sistemin hansı tip topologiyada qurulduğunu, hissələrin necə ünsiyyət
qurduğunu və hansı ümumi qaydalar daxilində yaşadığını müəyyən edir.

Bu səviyyədə düşünəndə sistem artıq yalnız kod bazası deyil, deploy olunan,
monitor olunan, şəbəkə üzərindən danışan, bəzən ayrıca verilənlər bazaları və ya
mesaj broker-lər vasitəsilə əlaqələnən canlı bir struktur olur. Məsələn,
microservices seçimi yalnız kod təşkilatı məsələsi deyil. O, deployment
müstəqilliyi, data ownership, network [[latency]], distributed tracing, partial
failure, [[consistency]] [[trade-off]]-ları, DevOps yükü və əməliyyat
mürəkkəbliyi ilə gəlir. Event-driven style də sadəcə “queue əlavə etmək” deyil.
O, sistemdə zamanın, ardıcıllığın, eventual consistency-nin və
[[observability]]-nin fərqli cür qurulması deməkdir.

REST isə burada xüsusi maraqlı nümunədir. Çox adam onu sadəcə HTTP üzərində JSON
qaytaran API forması kimi düşünür. Halbuki REST-in özü architectural style kimi
yaranıb və müəyyən məhdudiyyətlər üzərində qurulub: stateless interaction,
uniform interface, resource orientation və s. Praktikada bir çox API “REST API”
adlandırılır, amma əslində yalnız HTTP [[endpoint]] toplusudur. Bu, problem
deyil, amma termin fərqini bilmək vacibdir. Çünki architectural style dedikdə
yalnız format yox, davranış prinsipləri də nəzərdə tutulur.

Burada əsas fikir belədir: style sistemi ümumi davranış formasına salır,
architectural pattern onun daxilində struktur təşkilini formalaşdırır, design
pattern isə daha lokal problemləri həll edir. Bunların hər biri faydalıdır, amma
eyni miqyasda deyil.

### **Architecture bütün bu seçimlərin canlı kombinasiyasıdır**

Çox vacib bir nöqtə də budur ki, “architecture” ilə “architectural style” eyni
şey deyil. Architecture adətən konkret sistemin real dünyadakı qərarlar
toplusudur. Yəni o, nəinki hansı style və ya pattern-lərin seçildiyini, həm də
niyə seçildiyini, hansı məhdudiyyətlər altında seçildiyini, komandanın
yetkinliyi, məhsulun mərhələsi, performans tələbləri, texnoloji risklər və
əməliyyat imkanları ilə birlikdə formalaşan ümumi sistem qərarını ifadə edir.

Məsələn, bir məhsul architectural style olaraq modular monolith seçə bilər,
daxildə bəzi hissələr üçün layered və ya hexagonal təşkilat istifadə edə bilər,
daha sonra konkret biznes axınlarında Strategy, Factory və Observer kimi design
pattern-lərdən yararlana bilər. Bunların hamısı birlikdə həmin sistemin memarlıq
reallığını yaradar. Deməli, architecture təkcə bir etiket deyil. O, canlı
kompromislər toplusudur.

Bu səbəbdən “bizdə clean architecture var” demək hələ çox az şey deyir. Əgər
dependency-lər həqiqətən doğru istiqamətdə axmırsa, domain qaydaları
infrastruktura bağlanıbsa, data modeli business modelin yerinə keçibsə, həmin
etiket sistemin keyfiyyətini xilas etmir. Eyni şəkildə “biz microservice-ik”
demək də yetərli deyil. Əgər xidmət sərhədləri süni qurulubsa, data ownership
yoxdur, sinxron çağırış zəncirləri hər yeri bürüyübsə, burada style seçimi
özlüyündə güc yaratmır.

### **MVC bu xəritədə harada dayanır?**

MVC haqqında danışanda qarışıqlıq daha da artır. Çünki bu termin həm çox məşhur,
həm də çox səthi istifadə olunur. Bir çox insan MVC-ni universal arxitektura
kimi təqdim edir. Başqaları onu design pattern adlandırır. Bəziləri üçün isə MVC
sadəcə web framework qovluq strukturu deməkdir.

Əslində MVC tarixi və funksional baxımdan presentation-oriented structuring
yanaşmasıdır. O, model, view və controller arasında məsuliyyət ayırmağa çalışır.
Bu, xüsusilə UI və request handling kontekstlərində dəyərlidir. Controller
input-u qəbul edir, müəyyən koordinasiya aparır, model data və davranış daşıyır,
view isə təqdimatla məşğul olur. Bu ayrım müəyyən qarışıqlığın qarşısını alır və
presentation flow-u daha anlaşılan edir.

Amma MVC-ni tam sistem arxitekturası kimi qəbul etmək çox vaxt səhv istiqamət
verir. Çünki o, business domain-in sərhədlərini, data ownership-i, integration
strategiyasını, [[background processing]] modelini, distributed communication
qaydalarını və ya sistemin ümumi dependency fəlsəfəsini təkbaşına təyin etmir.
MVC bir tətbiqin müəyyən hissəsini daha səliqəli təşkil edə bilər, amma bütöv
sistem memarlığının yerini tutmur.

Bu səbəbdən bir çox komanda “biz MVC qurmuşuq” deyəndə əslində yalnız
request-handling qatını təsvir edir. Halbuki onların içərisində business logic
controller-lərə dolub, service-lər koordinasiya ilə domain qərarını qarışdırıb,
data modeli birbaşa UI-ya sızıb. Formal olaraq MVC görünə bilər, amma sistemin
deeper architecture məsələləri həll olunmamış qala bilər.

### **Layered, Hexagonal, Clean, Modular Monolith və Microservices bir-birinin alternativi kimi yox, fərqli səviyyəli cavablar kimi düşünülməlidir**

Real iş mühitində başqa bir qarışıqlıq da bu anlayışların sanki eyni tip
qərarlar imiş kimi müqayisə edilməsidir. Layered architecture, Hexagonal, Clean
Architecture, Modular Monolith, Microservices çox vaxt bir siyahıda yan-yana
düzülür və insan elə düşünür ki, bunlardan birini seçmək lazımdır. Halbuki
bunların bəzisi daxili təşkil prinsipi, bəzisi isə daha yüksək səviyyəli sistem
quruluşudur.

Məsələn, modular monolith ilə microservices daha çox sistemin deployable
boundary-ləri və modul sərhədləri ilə bağlı böyük qərarlardır. Layered,
hexagonal və clean isə daha çox həmin sərhədlərin daxilində dependency və
məsuliyyət təşkilini nizamlayan yanaşmalardır. Yəni modular monolith seçmiş bir
sistem daxilində clean və ya hexagonal prinsiplərdən yararlana bilər. Eyni
şəkildə bəzi microservice-lərin daxilində layered yanaşma istifadə oluna bilər.
Bunlar tamamilə ayrı miqyaslarda qərarlardır.

Bu fərqi bilməmək komandanı yanlış mübahisələrə aparır. Bir komanda “biz clean
architecture seçdik, ona görə microservice-ə ehtiyac yoxdur” deyə bilər. Halbuki
biri daxili dependency fəlsəfəsi, o biri isə deployable system topology
mövzusudur. Başqa komanda “biz microservice-ik, ona görə arxitektura problemimiz
həll olunub” deyə bilər. Halbuki paylanmış sistem olmaq daxili model zəifliyini
avtomatik düzəltmir.

### **API anlayışı da bu xəritədə öz yerini bilməlidir**

API çox vaxt yalnız endpoint-lər toplusu kimi başa düşülür. Amma real iş
mühitində API sistem sərhədidir. O, yalnız məlumat ötürmür; o, müqavilə yaradır.
Bu müqavilənin sabitliyi, versiyalanması, semantikası, [[idempotency]]
xüsusiyyətləri, [[error shape]]-i, authorization sərhədi və performans xərci
bütöv sistem davranışına təsir edir.

Bu səbəbdən API dizaynı pattern məsələsi deyil, daha çox architectural səviyyəli
düşüncə tələb edir. REST, [[RPC]], [[GraphQL]] kimi yanaşmalar burada ünsiyyət
formasına təsir edir. Amma onların hər biri sistemin daxili modelini necə
açdığını, coupling-i necə dəyişdirdiyini və istehlakçı tərəfdə hansı gözlənti
yaratdığını fərqli şəkildə formalaşdırır. Deməli, API yalnız texniki interfeys
deyil; o, arxitekturanın çölə görünən üzüdür.

### **Güclü mühəndis anlayışları qarışdırmır, bir-birinə bağlayır**

Bu hissənin əsas nəticəsi odur ki, design pattern, architectural pattern,
architectural style və architecture eyni şey deyil. Onları eyni səbətdə istifadə
etmək düşüncə miqyasını itirmək deməkdir. Güclü mühəndis bu anlayışları formal
tərif kimi əzbərləmir, onların hansı səviyyədə dəyər yaratdığını hiss edir.

Design pattern lokal təkrarlanan problemi həll edir. Architectural pattern
sistemin daxili təşkilinə istiqamət verir. Architectural style ümumi davranış
məhdudiyyətlərini və topologiyanı müəyyənləşdirir. Concrete architecture isə
bunların real kontekst daxilində verilmiş qərarlar şəklində toplanmış
formasıdır.

Bu fərqi hiss edən komanda daha təmiz qərarlar verir. Onlar hər problemi
pattern-lə həll etməyə çalışmır. Hər strukturu da arxitektura zənn etmir. Onlar
bilirlər ki, MVC faydalı ola bilər, amma bütün sistemin taleyini təkbaşına həll
etmir. Bilirlər ki, microservices güc gətirə bilər, amma yalnız həqiqi sərhədlər
və əməliyyat yetkinliyi varsa. Bilirlər ki, clean architecture faydalı ola
bilər, amma yalnız dependency fəlsəfəsi həqiqətən yaşadıqda.

Mühəndislik prinsipləri də burada yenidən öz yerini tapır. Çünki məsələ termin
toplamaq deyil. Məsələ sistemin hansı problemləri hansı səviyyədə həll etdiyini
ayırd edə bilməkdir.

## **VII bölüm — Data strukturları, [[alqoritm]]ik düşüncə, ORM, [[caching]], [[sync]]/[[async]] və thread-lər: performans sonradan əlavə olunan mövzu deyil**

Proqramlaşdırma öyrənən insanların böyük hissəsi performans mövzusuna çox gec
çatır. Bunun bir səbəbi də odur ki, başlanğıc mərhələsində sistemlər kiçik olur,
data az olur, istifadəçi sayı aşağı olur və bir çox yanlış qərar dərhal cəza
vermir. Bu da təbii olaraq belə bir yanlış hiss yaradır: sanki performans
ayrıca, daha sonra baxılacaq, “sistem böyüyəndə lazım olacaq” bir məsələdir.
Halbuki real iş mühitində performans çox vaxt sonradan optimizasiya edilən
məsələ olmaqdan əvvəl, başlanğıcda verilmiş modelləşdirmə və icra qərarlarının
nəticəsi olur.

Bu nöqtədə kompüter elmləri nəzəriyyəsinin dəyəri bir daha görünür. Data
strukturları, alqoritmik düşüncə, [[execution model]], [[concurrency]], memory
davranışı, I/O gözləməsi, data locality, cache semantics kimi mövzular interview
sualı olmaq üçün yaranmayıb. Onlar sistemin niyə bir yerdə axıcı, başqa yerdə
isə ağır və qırılqan davrandığını anlamaq üçündür. Güclü mühəndis performansı
yalnız “tez işləsin” kimi düşünmür. O, performansı cost modeli kimi görür: nə
qədər CPU, nə qədər yaddaş, nə qədər round-trip, nə qədər gözləmə, nə qədər
contention, nə qədər koordinasiya xərci var və bunlar sistemin doğruluğu,
sadəliyi və genişlənə bilməsi ilə necə toqquşur.

Bu mövzuya səthi baxanda hər şey xırda optimizasiya kimi görünə bilər. Daha
sürətli sorğu, daha az millisaniyə, daha yaxşı cache hit rate və sair. Dərin
baxanda isə görünür ki, bunların bir çoxu əslində sistemin necə düşünülməsi ilə
bağlıdır.

### **Data strukturu seçimi texniki detal deyil, davranış seçimidir**

Bir çox hallarda proqramçı data strukturunu ən yaxın görünən seçimlə müəyyən
edir. Siyahı lazımdırsa list, tez axtarış lazımdırsa dictionary, sıralı məlumat
lazımdırsa array və ya tree tipli strukturlar. Bu qərarlar sadə görünür, amma
sistem böyüdükcə onların təsiri dəyişir. Çünki data strukturu yalnız məlumat
saxlama üsulu deyil; o, sistemin həmin məlumat üzərində necə davrandığını da
müəyyən edir.

Əgər bir kolleksiya üzərində tez-tez axtarış gedirsə, amma struktur sırf ardıcıl
gəzməyə əsaslanırsa, zaman keçdikcə həmin qərarın qiyməti görünür. Əgər eyni
məlumat dəfələrlə transformasiya olunur, lazımsız nüsxələr yaradılırsa, bu
yalnız CPU yox, yaddaş davranışını da təsir edir. Əgər strukturun insertion,
[[lookup]], iteration və ordering xüsusiyyətləri konkret istifadə ssenarisi ilə
uyğun gəlmirsə, kod ilk gün işləyir, amma sistem davranışı getdikcə baha başa
gəlir.

Ən vacib məqam da budur ki, real iş mühitində bu problemlər çox vaxt “algoritm
sualı” formasında gəlmir. Heç kim gündəlik işdə oturub “burada Big-O yanlışdır”
demir. Problem daha səssiz görünür: müəyyən bir endpoint niyə yavaşlayır, niyə
bu background job gözləniləndən artıq yaddaş istifadə edir, niyə bu filter-ləmə
mərhələsi yük altında xətti şəkildə deyil, daha ağır böyüyür, niyə
[[pagination]] bir yerdən sonra pozulmağa başlayır. Bunların kökündə çox vaxt
məhz data təmsili və traversal qərarları dayanır.

Buna görə data strukturlarını bilmək sadəcə klassik nəzəri hazırlıq deyil. Bu
bilik sistemdə hansı əməliyyatın doğrudan da “ucuz”, hansının “bahalı” olduğunu
hiss etməyə kömək edir.

### **Alqoritmik düşüncə yalnız çətin məsələlər üçün deyil**

Alqoritm deyəndə çox adamın ağlına dərhal yarış proqramlaşdırması, [[LeetCode]]
və ya qəribə puzzle tipli suallar gəlir. Bu təsəvvür alqoritmik düşüncənin real
dəyərini xeyli azaldır. Çünki peşəkar iş mühitində alqoritmik düşüncə ən çox
“mürəkkəb sual həlli” kimi yox, mərhələli qərar keyfiyyəti kimi özünü göstərir.

Məsələn, böyük data dəsti üzərində ardıcıl filter, map, group və [[sort]]
əməliyyatları aparırsansa, bunların sırası artıq alqoritmik qərardır. Əgər
bahalı əməliyyatı tez tətbiq edirsənsə, sonrakı bütün axın ağırlaşa bilər. Əgər
lazımi qədər erkən daraltma etmirsənsə, sistem lazımsız elementlər üzərində
işləməyə davam edir. Əgər eyni hesablamanı təkrar edirsənsə və onu memoization,
caching və ya [[batch]] emalı ilə azaltmırsansa, performans problemi qaçılmaz
olur. Əgər bir prosesin düzgün hissələrini stream-ləmək əvəzinə hər şeyi yaddaşa
yığırsansa, algoritmik qərar artıq memory problemə çevrilir.

Bu məsələlərin bir çoxu kitab tərifləri ilə deyil, cost hissi ilə bağlıdır. Yəni
alqoritmik düşüncə daha çox belə bir daxili refleks yaradır: bu əməliyyat nəyi
neçə dəfə edir, nəyin üzərində edir, hansı miqyasda edir və niyə bu qədər edir?

Real mühəndislikdə bu refleks çox qiymətlidir. Çünki sistemlərin böyük hissəsi
qəfil dağılmır. Onlar yavaş-yavaş ağırlaşır. Bu ağırlaşmanın kökü də çox vaxt
elə sadə görünən qərarlarda olur.

### **Dilin sintaksisi vacibdir, amma bu vaciblik sərhədlidir**

Bu mövzu burada təbii şəkildə açılır. Sintaksis vacibdir, amma çox adamın
düşündüyü səbəbə görə yox.

Bir dili yaxşı bilmək lazımdır. Çünki dilin idiom-larını, memory modelinə təsir
edən davranışlarını, async mexanizmlərini, standard library imkanlarını,
generics və type system xüsusiyyətlərini bilmədən o dildə təmiz və təhlükəsiz
kod yazmaq çətindir. Məsələn, C#-da [[async/await]], LINQ, IEnumerable və
IAsyncEnumerable fərqləri, Task-ın necə davrandığı, reference və value
semantics, exception flow, allocation davranışları nəzərə alınmadan “sadəcə
sintaksis” səviyyəsində yazılan kod çox tez səhv istiqamətə gedə bilər. Eyni ilə
JavaScript-də event [[loop]], promise chain-ləri, microtask queue, closure
davranışı başa düşülmədən sintaksis bilmək yetərli olmur.

Amma eyni zamanda sintaksisə həddindən artıq fokuslanmaq böyük risktir. Çünki
dil biliyi insanı məhsuldar edə bilər, amma ona avtomatik olaraq sistem hissi
vermir. Yəni biri bir dilin çox incə sintaktik xüsusiyyətlərini bilə bilər, amma
yenə də zəif sərhədlər qurub ağır coupling yarada bilər. Başqa biri daha az
“clever” kod yazıb, amma çox daha güclü sistem qura bilər.

Bu səbəbdən dil sintaksisi nə kiçildilməlidir, nə də mərkəzə qoyulmalıdır. O,
vacib təməl vasitədir, amma mühəndisliyin özü deyil. Dil sənə ifadə imkanları
verir; hansı şeyi necə ifadə etmək lazım olduğunu isə daha dərin təməl müəyyən
edir.

### **ORM rahatlıq verir, amma reallığı ləğv etmir**

ORM-lər müasir tətbiqlərdə məhsuldarlığı ciddi şəkildə artır. Onlar
[[məlumat bazası]] ilə işləməyi daha rahat, daha ardıcıl və daha sürətli inkişaf
etdirilə bilən hala gətirir. Entity-lərin xəritələnməsi, query [[composition]],
change tracking, migration-lar, repository və unit of work kimi yanaşmaların
tətbiqi bir çox komandaya real dəyər verir. Problem ORM-in özündə deyil. Problem
onun yaratdığı rahatlığın bəzən sistem reallığını görünməz etməsindədir.

Çünki ORM nə qədər güclü olsa da, arxa planda yenə də məlumat bazası var. Join
var, index var, scan var, lock var, transaction var, network round-trip var,
[[serialization]] var. ORM bunları yox etmir. Sadəcə onları daha yüksək
səviyyəli interfeys arxasında təqdim edir. Mühəndis bu pərdə arxasında nə baş
verdiyini hiss etmirsə, rahatlıq tezliklə korluğa çevrilir.

Bunun ən klassik nümunələrindən biri N+1 problemidir. Kod səviyyəsində hər şey
təmiz və idiomatik görünə bilər, amma arxa planda yüzlərlə ayrıca sorğu gedə
bilər. Eyni şəkildə lazımsız eager loading, ağır graph materialization,
həddindən artıq tracking, qeyri-optimal pagination, böyük result set-lərin
memory-yə çəkilməsi kimi problemlər də ORM-in rahat syntax-ı içində gizlənə
bilər.

Bu mövzuda mature yanaşma dual olmalıdır. Bir tərəfdən ORM-dən qorxmaq lazım
deyil; o, çox güclü alətdir. O biri tərəfdən də onu “database məsələlərini artıq
həll edir” kimi görmək yanlışdır. Güclü mühəndis ORM istifadə edərkən də query
plan düşünür, məlumatın haradan necə gəldiyini hiss edir, database-i tətbiqin
arxasında görünməz qara qutu kimi deyil, sistemin əsas komponentlərindən biri
kimi qəbul edir.

Bəzən ORM ən doğru seçim olur. Bəzən müəyyən performans kritik yerlərdə birbaşa
SQL və ya daha incə query nəzarəti lazımdır. Burada da yenə ideologiya yox,
kontekst ön planda olmalıdır.

### **Caching performans həlli olmaqla yanaşı, [[correctness]] problemidir**

Caching çox vaxt sadə optimizasiya addımı kimi təqdim olunur. “Database ağırdır,
response gecikir, gəlin cache əlavə edək.” Bu məntiq ilk baxışda kifayət qədər
sağlam görünür. Amma cache heç vaxt yalnız sürət aləti olmur. O, eyni zamanda
sistemin həqiqət modeli ilə bağlı qərardır.

Çünki cache sistemi sürətləndirməklə yanaşı məlumatın ikinci nüsxəsini yaradır.
İkinci nüsxə yaranan yerdə isə dərhal sual meydana çıxır: hansı nüsxə əsasdır,
hansı anda yenilənir, nə qədər müddət etibarlıdır, hansı hadisə onu etibarsız
edir, paylanmış mühitdə node-lar arasında necə uyğunlaşır, partial failure
zamanı hansı nəticə doğurur?

Bu səbəbdən cache əlavə etmək çox vaxt kod yazmaqdan çox, məlumatın həyat
dövrünü yenidən düşünmək deməkdir. Əgər sistemdə correctness daha vacibdirsə,
bəzi yerlərdə köhnə məlumat göstərmək olmaz. Bəzi hallarda isə müəyyən qısa
[[gecikmə]] qəbul edilə bilər və cache böyük fayda verir. Bəzi ssenarilərdə
read-through və ya write-through yanaşmalar faydalıdır, bəzi yerlərdə isə
event-driven invalidation daha uyğundur. Bəzən yalnız in-memory cache kifayət
edir, bəzən distributed cache lazımdır, bəzən isə cache problemi həll etmir,
sadəcə zəif query modelini gizlədir.

Caching haqqında ən senior baxışlardan biri budur: cache əlavə etməzdən əvvəl
sistem nəyə görə yavaşdır, bunu anlamaq lazımdır. Çünki çox vaxt cache düzgün
qurulmayan data access modelinin, qeyri-dəqiq API contract-ların və ya lazımsız
informasiya ötürülməsinin üzərinə yapışdırılmış müvəqqəti plasterə çevrilir.

### **API performansı yalnız server sürəti ilə ölçülmür**

Sistem performansını yalnız [[backend]] daxilindəki kod sürəti ilə ölçmək də dar
baxışdır. API-lər sistem sərhədi olduğuna görə onların dizaynı birbaşa
performansa təsir edir. Lazımsız böyük [[payload]]-lar, qeyri-dəqiq
contract-lar, həddindən artıq chatty interaction, yanlış pagination
strategiyası, lazımsız round-trip-lər, zəif error semantics, idempotency
çatışmazlığı və ya həddindən artıq [[generic]] response formatları sistemin
ümumi cost modelini ağırlaşdırır.

Məsələn, bir endpoint-in texniki olaraq “tez” işləməsi onun səmərəli olması
demək deyil. Əgər client eyni məlumatı toplamaq üçün beş endpoint
çağırmalıdırsa, ümumi interaction artıq baha başa gəlir. Əgər server lazım
olandan çox data göndərirsə, serialization, network və parsing xərcləri artır.
Əgər pagination offset-based yanaşma ilə böyük datada ağırlaşırsa, problem
yalnız database səviyyəsində deyil, API kontraktı səviyyəsindədir. Əgər hər
request eyni expensive query-ni təkrar çağırırsa, burada da problem təkcə SQL
deyil; resource design və access pattern zəif düşünülüb.

Bu da göstərir ki, performans ayrı modulun problemi deyil. O, sistemin
sərhədlərində də formalaşır.

### **Sync və async məsələsi sürət mübahisəsi deyil, execution model mövzusudur**

Müasir proqramlaşdırmada ən çox yanlış sadələşdirilən mövzulardan biri də
sinxron və [[asinxron]] proqramlaşdırmadır. Çox adam bunu “async daha yaxşıdır”
kimi başa düşür. Bu, təhlükəli dərəcədə primitiv yanaşmadır. Async avtomatik
olaraq faster demək deyil. Async müəyyən tip gözləmələrin daha səmərəli idarə
olunması deməkdir.

Əgər bir sistem çoxlu I/O gözləməsi yaşayırsa — database çağırışları, HTTP
request-lər, fayl oxuma, message broker ilə ünsiyyət — bu gözləmələr zamanı
thread-in boş yerə bloklanmaması vacib ola bilər. Burada async yanaşma
[[throughput]]-u yaxşılaşdıra bilər. Çünki sistem gözləmə müddətində resursları
daha səmərəli idarə edir. Amma əgər iş [[CPU-bound]]-dursa, yəni əsas yük
hesablama üzərindədirsə, async sözünün özü problemi həll etmir. Hətta bəzi
hallarda əlavə mürəkkəblik yaradır.

Bu fərqi hiss etməyən komandalar çox vaxt hər şeyi async etməklə daha müasir və
daha performanslı sistem qurduqlarını düşünürlər. Halbuki əsl məsələ execution
modeldir. Harada gözləmə var, harada iş görülür, hansı mərhələdə thread boş
qalır, hansı mərhələdə tutulur, hansı əməliyyat parallel işləyə bilər, hansında
isə ardıcıllıq qorunmalıdır — bütün bunlar birlikdə düşünülməlidir.

Async bu səbəbdən sintaktik modernlik deyil. O, resursların necə istifadə
olunduğuna dair qərardır.

### **Thread-lər sistemi sürətləndirməkdən çox, mürəkkəbləşdirmək gücünə malikdir**

Thread mövzusu da çox vaxt səthi başa düşülür. İnsan ilk baxışda belə düşünür:
daha çox thread daha çox paralellik, daha çox paralellik isə daha çox sürət.
Praktikada bu zəncir çox nadir hallarda bu qədər sadə işləyir.

Çünki thread-lər təkcə icra vahidi deyil; onlar paylaşılmış resurslar,
koordinasiya, [[context switching]], [[lock contention]], [[memory visibility]]
və [[scheduling]] kimi problemləri də özü ilə gətirir. Sırf paralellik naminə
thread sayını artırmaq çox vaxt gözlənilən faydanı vermir. Bəzən əksinə, sistem
daha da ağırlaşır. Çünki koordinasiya xərci, lock-lar, [[cache invalidation]] və
state paylaşımı artdıqca real qazanc azalır.

Bu səbəbdən concurrency mövzusu yalnız “necə paralel işlədim?” səviyyəsində yox,
“nəyi niyə eyni anda işlətmək istəyirəm və bunun correctness qiyməti nədir?”
səviyyəsində düşünülməlidir. Əgər state paylaşılırsa, onda yarış vəziyyətləri
yaranır. Əgər ardıcıllıq vacibdirsə, lazımsız parallelism nəticəni pozur. Əgər
[[cancellation]], [[timeout]] və [[retry]] birlikdə düşünülmürsə, sistem partial
failure-lar zamanı gözlənilməz davranır.

Real iş mühitində thread-lərdən və concurrency-dən düzgün istifadə, əslində,
paylaşılmış state-i mümkün qədər azaltmaq, iş vahidlərini düzgün ayırmaq və icra
modelini sistemin həqiqi yük profilinə uyğun seçmək deməkdir. Functional
yanaşmanın immutability vurğusu da burada öz praktik dəyərini göstərir.

### **Asinxronluq və background processing sərhədi düzgün seçilməlidir**

Bir çox sistemdə request daxilində görülən işlərin hamısını eyni anda cavaba
bağlamaq düzgün olmur. Bəzi işlər var ki, istifadəçiyə dərhal təsdiq vermək
kifayətdir, daha sonrakı hissələr isə arxa planda işlənə bilər. Notification
göndərilməsi, analytics event-lər, bəzi report yeniləmələri, qeyri-kritik cache
refresh, axtarış indeksinin yenilənməsi kimi məsələlər buna nümunə ola bilər.

Amma bu sərhəd yanlış seçiləndə problem yaranır. Əgər background-a atılan iş
əslində sistemin correctness-i üçün kritikdirsə, istifadəçiyə erkən success
qaytarmaq risklidir. Əgər queue və worker modeli var, amma retry semantics,
dead-letter handling, idempotency və duplicate processing məsələləri
düşünülməyibsə, sistem “müasir” görünə bilər, amma etibarlı olmaz.

Bu da göstərir ki, async və background processing sadəcə performans və UX aləti
deyil. Onlar düzgünlük modelinin bir hissəsidir. Hər şeyin request daxilində
qalması da düzgün deyil, hər şeyi background-a atmaq da. Əsas məsələ business
nəticənin hansı anda etibarlı sayıldığını düzgün seçməkdir.

### **Performans mühəndisliyi əslində sadələşdirmə mühəndisliyidir**

Burada maraqlı bir paradoks var. İnsanlar performans dedikdə çox vaxt “daha
clever kod”, “daha mürəkkəb optimizasiya”, “daha dərin tuning” düşünür. Halbuki
ən güclü performans qərarlarının böyük hissəsi sistemi sadələşdirməkdən gəlir.
Daha az round-trip, daha təmiz data flow, daha dəqiq ownership, daha az lazımsız
serialization, daha düzgün batch ölçüsü, daha yaxşı seçilmiş sərhəd, daha az
redundant computation.

Yəni performans çox vaxt sonradan “sürətləndirmə” yox, əvvəldən “lazımsız işi
etməmə” məsələsidir.

Bu da bizi yenidən məqalənin əsas xəttinə qaytarır. Kompüter elmləri
nəzəriyyəsindən real iş mühitinə keçid insanı məhz buna öyrədir: sistemdə nə baş
verdiyini yalnız sintaksis səviyyəsində yox, cost və behavior səviyyəsində
görməyə. Data strukturunu seçəndə yalnız kod rahatlığını yox, əməliyyat
profilini düşünməyə. ORM istifadə edəndə arxada database-in hələ də gerçək
olduğunu unutmağa. Cache əlavə edəndə sürət qədər doğruluğu da hesaba qatmağa.
Async yazanda yalnız keyword yox, execution model seçdiyini başa düşməyə.
Thread-lərlə işləyəndə sadəcə paralellik deyil, koordinasiya yükü aldığını qəbul
etməyə.

Bu hissənin əsas nəticəsi budur: performans ayrıca mərhələdə toxunulacaq ikinci
dərəcəli mövzu deyil. O, sistemin ilk gündən necə düşünülməsinin təbii
nəticəsidir. Düzgün sistemlər sonradan daha az xilasetmə əməliyyatı tələb edir.
Çünki onların sürəti çox vaxt mikrosəviyyəli “trick”lərdən yox, makrosəviyyəli
düzgün qərarlardan gəlir.

## **VIII bölüm — Optimizasiya, sadəlik, texniki qərarvermə və mühəndis yetkinliyi: sistemləri yalnız qurmaq yox, yaşatmaq bacarığı və yekun Nəticə**

Bu məqalə boyunca bir neçə fərqli mövzuya toxunduq: sintaksisə həddindən artıq
fokuslanmağın riski, proqram yazmaqla sistem qurmaq arasındakı fərq, abstraksiya
və model qurmaq, OOP və FP kimi paradiqmaların real mənası, Clean Code və
SOLID-in həqiqi dəyəri, pattern və arxitektura səviyyələrinin fərqi, data
strukturları, ORM, caching, async və thread-lərin sistem davranışına təsiri. İlk
baxışda bunlar ayrı başlıqlar kimi görünə bilər. Amma əslində onların hamısı bir
mərkəzi həqiqətə bağlanır: real iş mühitində mühəndislik, kod yazmaq
qabiliyyətindən daha geniş bir şeydir. O, qərar vermək qabiliyyətidir.

Bu qərarların ən çətin tərəfi də odur ki, onlar nadir hallarda tam ağ-qara olur.
Mühəndislik çox az halda “düzgün cavab” tapmaqdır. Daha çox halda isə bu,
qeyri-mükəmməl reallıq içində ən sağlam variantı seçməkdir. Məhsul təzyiqi var,
vaxt məhduddur, komandanın səviyyəsi fərqlidir, biznes tələbləri dəyişir,
texniki borc yığılır, bir tərəfdə performans, o biri tərəfdə sadəlik, başqa
tərəfdə isə çeviklik tələbi dayanır. Məhz belə şəraitdə nəzəri biliklə praktik
qərarın həqiqi münasibəti görünür.

Bu səbəbdən “seniorluq” sadəcə daha çox framework bilmək deyil. Seniorluq,
sistemi hansı dərinlikdə gördüyünlə bağlıdır. Eyni koda iki nəfər baxa bilər;
biri yalnız işləyən hissəni görər, digəri isə onun gələcək dəyişiklik xərcini,
risk daşıyan sərhədlərini, coupling nöqtələrini, məlumat axınının zəif yerlərini
və performansın harada tıxanacağını da hiss edər. Aradakı fərq çox vaxt yazılan
sətir sayında deyil, görünən və görünməyən nəticələri birlikdə düşünmək
qabiliyyətində olur.

### **Optimizasiya tezlikdən əvvəl qərar keyfiyyətidir**

Optimizasiya mövzusu proqramlaşdırmada ən çox sui-istifadə olunan anlayışlardan
biridir. Bir tərəfdə hər şeyi əvvəlcədən optimallaşdırmağa çalışan yanaşma var;
o, çox vaxt sistemi həddindən artıq mürəkkəbləşdirir. Digər tərəfdə isə
optimizasiyanı tamamilə sonrakı mərhələyə atan yanaşma var; bu da çox vaxt səhv
başlanğıc qərarlarını “hələ sonra baxarıq” adı ilə gizlədir. Hər iki mövqedə
problem var.

Güclü mühəndislik optimizasiyanı yalnız mikro səviyyədə sürət artırmaq kimi
görmür. Ən mühüm optimizasiya çox vaxt sistemin içində lazımsız işi ümumiyyətlə
etməməkdir. Bu, daha az query, daha dəqiq data flow, daha düzgün ownership, daha
az coupling, daha təmiz sərhəd, daha aydın müqavilə deməkdir. Bir çox hallarda
performans problemi sonradan yazılan yavaş kodun yox, əvvəldən zəif seçilmiş
modelin nəticəsi olur.

Burada “[[premature optimization]]” ifadəsini də düzgün başa düşmək lazımdır. Bu
cümlə çox vaxt sanki performans haqqında erkən düşünmək ümumiyyətlə səhvdir kimi
yozulur. Əslində bunun mənası odur ki, qeyri-real və sübut olunmamış gələcək
üçün sistemi ağırlaşdırmaq risklidir. Yoxsa execution model, data access xərci,
cache semantics, concurrency riski, API sərhədləri, məlumatın həcmi və əməliyyat
profili kimi məsələləri əvvəldən düşünmək yanlış deyil. Əksinə, bu, yetkin
mühəndisliyin bir hissəsidir.

Daha sadə desək, performans fetişizmi ilə performans korluğu arasında bir orta
xətt var. Senior qərarvermə məhz o xətti tutmaqdır.

### **Sadəlik ucuz həll deyil, ağır düşüncənin nəticəsidir**

Mühəndislikdə sadəlik çox dəyərli anlayışdır, amma onu əldə etmək çox vaxt
düşündüyümüzdən çətindir. Çünki sadə görünən həll həmişə sadə olmur, mürəkkəb
görünən həll də həmişə yanlış olmur. Sadəliyin həqiqi ölçüsü onun zehni
yükündədir.

Əgər sistemdə bir qərarın səbəbini izah etmək mümkündürsə, dəyişiklik zamanı
təsir radiusu təxmin edilə bilirsə, bir modulun niyə mövcud olduğu aydın
görünürsə, müxtəlif hissələr bir-birinin içini bilmədən birlikdə işləyə bilirsə,
o zaman orada sadəlik var. Bu sadəlik bəzən az kodla gəlir, bəzən daha çox
strukturla. Məsələ səthdə nə qədər “light” görünməsi deyil; əsas məsələ sistemin
iç dünyasında nə qədər aydın olmasıdır.

Buna görə də sadəliklə bəsitlik eyni deyil. Bəsit sistem tez qurula bilər, amma
tez də qırılar. Sadə sistem isə adətən daha çox düşünülmüş olur. O, lazım
olmayan abstraksiyanı kənarda saxlayır, amma lazım olan sərhədləri də qurban
vermir. O, pattern-dən yalnız doğrudan gərginlik yarandığı yerdə istifadə edir.
O, “[[future-proof]]” görünmək üçün hər şeyi generic etmir. Eyni zamanda hər
şeyi bir faylda saxlayıb “mən sadə saxladım” bəhanəsinə də sığınmır.

Bu çox incə tarazlıqdır. Bir çox mühəndisin yetişməsi də məhz bu nöqtədə baş
verir. O, yavaş-yavaş anlayır ki, həqiqi sadəlik minimal görünmək yox, aydın
qalmaqdır.

### **Refactoring texniki zövq yox, sistemin nəfəs almasıdır**

Uzunömürlü sistemlərdə refactoring qaçılmazdır. Hətta bunu daha sərt demək olar:
refactoring etməyən sistemlər bir müddət sonra yalnız texniki borcla deyil,
düşüncə borcu ilə də yaşamağa başlayır. Çünki sistemin içində köhnə qərarlar,
müvəqqəti həllər, dəyişən biznes qaydaları, yeni texnologiya qatları və yarımçıq
abstraksiyalar toplanır. Onlar birlikdə əvvəl işləyən, amma getdikcə daha çətin
dəyişən bir struktur yaradır.

Refactoring-in problemi odur ki, o, çox vaxt xaricdən görünən business dəyəri
daşımır. Buna görə bir çox komandada təxirə salınır. Amma refactoring kodu
“gözəlləşdirmək” üçün edilən estetik düzəliş deyil. Onun ən böyük məqsədi
sistemin gələcəkdə düşünülə və dəyişdirilə bilməsini qorumaqdır. Yəni
refactoring həm texniki borcun, həm də semantik qarışıqlığın qarşısını alır.

Burada da yetkin yanaşma vacibdir. Hər narahatlıq refactoring tələb etmir. Hər
narahatlıq da “indi dəyməyək” deyə ötürülməməlidir. Güclü mühəndis hansı
hissənin sadəcə zövq problemi, hansı hissənin isə gələcəkdə ciddi dəyişiklik
xərci yaradacaq struktur problemi olduğunu ayırd etməlidir. Yəni refactoring də
ideoloji refleks yox, kontekstual qərardır.

### **Uzunömürlü sistemlər ideal sistemlər deyil**

Çox adam sistem dizaynına başlayanda gizli şəkildə “düzgün arxitektura qurum,
sonra rahat olum” kimi düşünür. Bu, çox insanidir. Amma real iş mühitində
uzunömürlü sistemlər nadir hallarda ideal sistemlər olur. Onlar daha çox davamlı
şəkildə uyğunlaşa bilən sistemlər olur.

Sistemlər yaşayan strukturlardır. Məhsul dəyişir, istifadəçi davranışı dəyişir,
biznes prioritetləri sürüşür, inteqrasiyalar artır, gözlənilməyən use-case-lər
yaranır, komanda böyüyür və ya kiçilir, bəzən texnologiya stack-i belə dəyişir.
Bu qədər dəyişən mühitdə “bir dəfəlik mükəmməl quruluş” anlayışı praktik deyil.
Ona görə yaxşı memarlığın əsas xüsusiyyəti qüsursuz görünmək yox,
dəyişikliklərlə birlikdə deformasiya olmadan yaşaya bilməkdir.

Bu məqam çox vacibdir. Çünki bəzən mühəndislər arxitekturanı sərtlik kimi
qururlar. Hər şeyi əvvəlcədən düşünməyə çalışırlar, hər potensial ehtimal üçün
extension point yaradırlar, çox yüksək abstraksiya qatları qururlar. Bir müddət
sonra sistemin özünü qorumaq məhsulu inkişaf etdirməkdən daha çətin olur.
Halbuki uzunömürlülük çox vaxt elastiklikdən gəlir, sərtlikdən yox.

Deməli, “future-proof” sistem ideyası çox zaman şişirdilmiş təsəvvürdür.
Gələcəyi tam bağlamaq mümkün deyil. Amma dəyişiklik istiqamətlərinə həssas
olmaq, sabit mərkəzi hissəni tanımaq, riskli sərhədləri düzgün qurmaq və sistemi
lazım olduqda refactor oluna bilən vəziyyətdə saxlamaq mümkündür. Yetkin
mühəndislik də məhz buna çalışır.

### **Texniki qərarvermə təkcə kod keyfiyyəti yox, təşkilati yetkinlik də tələb edir**

Real iş mühitində mühəndis heç vaxt boşluqda qərar vermir. Onun qərarları həmişə
komandanın qabiliyyəti, məhsulun mərhələsi, biznes təzyiqi, infrastruktur
imkanları, buraxılış tezliyi, observability səviyyəsi və əməliyyat yükü ilə
bağlı olur. Eyni texniki qərar fərqli mühitlərdə tamamilə fərqli nəticə verə
bilər.

Məsələn, microservices bəzi komandalar üçün düzgün addım ola bilər, çünki
onların deploy müstəqilliyinə, ayrıca ownership-ə və əməliyyat yetkinliyinə
ehtiyacı var. Başqa komanda üçün eyni qərar vaxtından əvvəl mürəkkəblik gətirə
bilər və modular monolith daha sağlam seçim olar. Eyni şəkildə CQRS bəzi
sistemlərdə həqiqətən model aydınlığı və performans faydası verə bilər,
başqalarında isə sadəcə ikiqat [[complexity]] yaradar. Hər şey problemin
formasından başqa, onu daşıyacaq təşkilati reallıqdan da asılıdır.

Bu səbəbdən güclü mühəndislik yalnız “doğru texniki seçim” etməyə çalışmır. O,
həmin seçimin komanda və məhsul reallığı içində yaşayıb-yaşamayacağını da
düşünür. Bu, çox vaxt nəzəri mükəmməllikdən daha vacib olur. Kağız üzərində
ideal görünən arxitektura, onu daşıya bilməyən komanda üçün zəif həll ola bilər.
Əksinə, nisbətən sadə görünən struktur, komandanın hazırkı səviyyəsinə uyğun
olduğu üçün çox daha uğurlu sistemə çevrilə bilər.

Bu da bizi məqalənin ilk hissələrinə qaytarır. Mühəndislik yalnız alət bilmək
deyil. O, sistem, insan və proses reallığını birlikdə düşünməkdir.

### **Nəzəriyyənin son dəyəri: düşüncə keyfiyyəti**

Bu məqalənin başlığında “Kompüter Elmləri Nəzəriyyəsindən Real İş Mühitinə”
ifadəsi təsadüfi seçilməyib. Çünki bu keçid çox vaxt yanlış anlaşılır. Bəziləri
düşünür ki, nəzəriyyə bir mərhələdir, iş həyatı isə ondan tam ayrı başqa
mərhələdir. Halbuki məsələ belə işləmir. Nəzəriyyə ilə praktika arasında divar
yoxdur. Aralarında səviyyə fərqi var.

Nəzəriyyənin əsas dəyəri də burada ortaya çıxır. O, sənə təkcə məlumat vermir;
o, düşüncəni strukturlaşdırır. Abstraksiya hissi verir. Model görməyi öyrədir.
İnvariantı ayırd etməyə kömək edir. State və [[side effect]]-lərə daha ayıq
yanaşma yaradır. Coupling-in təhlükəsini, cohesion-in dəyərini, concurrency-nin
riskini, alqoritmik qərarların cost modelini, arxitektura ilə struktur görüntüsü
arasındakı fərqi sezdirir.

Yəni nəzəriyyə iş həyatında birbaşa kitab tərifi kimi deyil, qərar keyfiyyəti
kimi geri qayıdır.

Məhz buna görə proqramlaşdırma öyrənərkən yalnız sintaksisə fokuslanan yanaşma
uzun müddətdə kifayət etmir. Sintaksis lazımdır, amma o yalnız ifadə
vasitəsidir. Həqiqi dəyər isə nəyin ifadə olunacağını və niyə elə ifadə
olunacağını başa düşməkdədir. Bu fərqi görməyən adam uzun müddət kod yazan biri
ola bilər. Bu fərqi görən adam isə tədricən mühəndisə çevrilir.

### **Nəticə**

Real iş mühitində tələb olunan mühəndislik prinsipləri ayrıca, bir-birindən
qopuq qaydalar toplusu deyil. OOP, FP, SOLID, design pattern-lər, architectural
style-lar, low coupling, high cohesion, data strukturları, ORM, caching, async,
thread-lər, API-lər, optimizasiya — bunların hamısı bir sistemin fərqli
tərəflərinə baxan düşüncə alətləridir. Bunları yalnız termin kimi bilmək kifayət
etmir. Onları hansı səviyyədə, hansı problem üçün və hansı qiymətə istifadə
etdiyini başa düşmək lazımdır.

Ən yaxşı mühəndis hər pattern-i tanıyan, hər texnologiyanı bilən və ya ən
“clever” kod yazan adam deyil. Ən yaxşı mühəndis reallığı düzgün modelləşdirən,
sistemin görünməyən yükünü hiss edən, dəyişiklik xərclərini əvvəlcədən sezən,
sadəliyi qorumağa çalışan və texniki qərarların həm bu günə, həm də sabaha necə
təsir edəcəyini düşünən adamdır.

Kompüter elmləri nəzəriyyəsindən real iş mühitinə keçid də əslində məhz budur:
kod parçalarından sistemlərə, sintaksisdən semantikaya, lokal həllərdən
uzunömürlü qərarlara, “necə işləyir?” sualından “niyə belə qurulmalıdır?”
düşüncəsinə keçid.

Bu keçid asan deyil. Amma mühəndislik də elə burada başlayır.

---

_Bu iki hissəli silsilə boyunca kod parçalarından sistemlərə, sintaksisdən
semantikaya qədər uzanan yolu incələdik. Yaxşı mühəndisin yalnız çox şey bilən
deyil, qərar verməyi və sistemi yaşatmağı bacaran şəxs olduğunu gördük. Ümid
edirik ki, bu yanaşma sizin real iş mühitindəki inkişafınıza kömək edəcək._

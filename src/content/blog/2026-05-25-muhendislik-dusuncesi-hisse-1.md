---
title:
  "Kompüter Elmləri Nəzəriyyəsindən Real İş Mühitinə: Mühəndislik Düşüncəsi
  (Hissə 1)"
author: murad-nurubayli
description:
  "Proqramlaşdırma öyrənməklə mühəndislik düşüncəsi qazanmaq arasındakı fərq,
  sistem qurmaq, modellər və abstraksiyaların rolu."
date: 2026-05-25
categories: ["Təhsil", "Proqramlaşdırma"]
resource: true
resource_audiences: ["Universitet Tələbələri", "Proqramçılar"]
---

_Bu məqalə [[mühəndislik]] düşüncəsi və sistem qurmaq bacarıqları haqqında iki
hissəli silsilənin birinci hissəsidir. Burada biz kod yazmaqdan sistem
düşüncəsinə keçidi, [[paradiqma]]ları və düzgün [[model]] qurmağı müzakirə
edəcəyik._

---

## **I hissə — Niyə çox adam kod yazmağı öyrənir, amma mühəndisliyə keçə bilmir?**

Gəlin məsələni lap əvvəldən aydınlaşdıraq: [[proqramlaşdırma]] öyrənmək ilə
mühəndislik düşüncəsi qazanmaq eyni şey deyil.

Bu iki anlayış bir-birinə çox yaxın görünür. Hətta ilk mərhələdə aralarındakı
fərq demək olar ki, hiss olunmur. İnsan bir dili öyrənir, dəyişənləri anlayır,
[[if]], [[loop]], [[function]], [[class]] yazır, bir neçə kiçik layihə qurur,
API çağırır, [[tətbiqi proqramlaşdırma interfeysi]] ilə işləyir, məlumat
bazasına qoşulur, ekranda nəsə işləyən bir şey görür — və təbii olaraq düşünür
ki, artıq proqramlaşdırmanı bilir. Müəyyən mənada haqlıdır da. O, həqiqətən kod
yazmağı öyrənib. Amma problem də məhz burada başlayır: kod yazmaq bacarığı çox
vaxt mühəndislik bacarığı ilə səhv salınır.

Real iş mühitində isə fərqi məhz bu nöqtə müəyyən edir.

Çünki sənayedə problem heç vaxt yalnız “bu funksiyanı necə yazım?” səviyyəsində
qalmır. Problem daha çox belə olur: bunu necə elə yazaq ki, sabah dəyişəndə
sistem dağılmasın? Komandada başqa adam bunu açanda qorxmasın? Performans yük
altında gözlənilməz davranmasın? Bir hissəyə düzəliş edəndə başqa hissədə səssiz
qırılma yaratmasın? [[Domain]] qaydaları kodun içində itib-batmasın? Yeni
requirement gələndə hər şeyi sıfırdan sökmək məcburiyyəti yaranmasın?

Yəni sual artıq [[sintaksis]] sualı olmur. Sual sistem sualına çevrilir.

Məncə proqramlaşdırmanı öyrənən çox adamın ilişdiyi ən böyük nöqtə də budur:
onlar dili öyrənirlər, amma sistem düşünməyi öyrənmirlər. Onlar [[framework]]
öyrənirlər, amma [[abstraksiya]] qurmağı öyrənmirlər. Onlar feature yazırlar,
amma dəyişiklik xərcini hesablamağı öyrənmirlər. Onlar “nə işləyir?” sualına
cavab axtarırlar, amma “niyə belə qurulmalıdır?” sualını çox gec verirlər.

Bu fərq xırda görünə bilər. Amma peşəkar inkişafın bir müddətdən sonra tam
mərkəzinə keçir.

### **Sintaksis niyə bu qədər çox ön plana çıxır?**

Çünki sintaksis görünəndir.

İnsan ilk dəfə proqramlaşdırmaya başlayanda gözünün qarşısında olan şey dildir.
Sözlər, operatorlar, qaydalar, səhvlər, compiler mesajları, IDE
autocomplete-ləri. Dil konkret görünür, ölçülür, yoxlanır. Doğru yazdınsa keçir,
səhv yazdınsa qırılır. Bu, beyinə çox rahat gəlir. Çünki sərhədi aydındır.

Mühəndislik prinsipləri isə belə deyil.

Məsələn, bir başlanğıc səviyyəli proqramçı üçün for ilə while arasındakı fərq
çox real görünə bilər. Amma “low [[coupling]] nə üçün vacibdir?” sualı ona
abstrakt gəlir. class yazmaq konkret tapşırıqdır. Amma “bu məsuliyyət bu
obyektin içində olmalıdır, ya başqa sərhəddə?” sualı daha çətindir.
[[async/await]] sintaksisini öyrənmək mümkün görünür. Amma “bu əməliyyat niyə
[[blocking]] davranır, [[thread pool]] nə vaxt tıxanır, [[I/O-bound]] və
[[CPU-bound]] işlərin fərqi nədir?” sualı artıq daha dərin düşüncə tələb edir.

Məhz buna görə çox adam görünən hissəyə daha çox enerji verir.

Dil öyrənmək rahatdır, çünki onun sürətli geribildirimi var. Prinsipləri
öyrənmək çətindir, çünki onların dəyəri çox vaxt yalnız sistem böyüyəndə
görünür.

Bu, proqramlaşdırma təhsilində çox fundamental bir problemdir. Çünki insanın
zehni təbii olaraq dərhal nəticə verən şeyə bağlanır. Bir günün içində yeni bir
sintaktik struktur öyrənə bilərsiniz. Bir həftənin içində kiçik bir [[CRUD]]
tətbiqi qura bilərsiniz. Amma məsuliyyətlərin ayrılması, coupling-in idarəsi,
düzgün abstraction səviyyəsi, domain model-in sərhədləri, transaction [[axın]]ı,
[[concurrency]] riskləri, [[caching]]-in [[yan təsir]]ləri, [[ORM]]-in
gizlətdiyi problemlər kimi mövzular ancaq zamanla, səhvlə və sistem davranışını
müşahidə etməklə oturur.

Deməli, problem insanların zəif olması deyil. Problem çox vaxt təhsil və öyrənmə
trayektoriyasının səthi tərəfi mükafatlandırmasıdır.

### **“İşləyir” mühəndislik meyarı deyil**

Başqa bir kritik məsələ də budur: başlanğıc mərhələsində “işləyir” çox vaxt
kifayət meyar kimi görünür.

Bir form submit olunur, məlumat databazaya düşür, response qayıdır, ekranda
nəticə görünür. Hamı razıdır. Amma real iş mühitində “işləyir” sualın ən sadə
hissəsidir. Hətta bəzən ən az vacib hissəsidir.

Çünki kodun işləməsi onun düzgün abstraksiya edildiyini göstərmir. Düzgün
adlandırıldığını göstərmir. Dəyişikliklərə davamlı olduğunu göstərmir. Test
olunmasının asan olduğunu göstərmir. Fərqli komandaların eyni [[kod bazası]]nda
rahat işləyə biləcəyini göstərmir. Hətta bəzən təhlükəsiz olduğunu da göstərmir.

Bir çox zəif sistem ilk baxışda yaxşı işləyir.

Əsas problem sonradan ortaya çıxır. Yeni feature gələndə. Yük artanda. Eyni
business qaydası üç yerdə təkrarlandığı üçün inconsistencies yarananda. Kiçik
dəyişiklik domino effekti verəndə. Məlumat bazasında sorğuların həddindən artıq
ağır olduğu üzə çıxanda. Bir [[endpoint]] sadəcə “tez işləsin” deyə
[[cache]]-lənəndən sonra [[stale data]] problemi partlayanda. [[Async]]
yazıldığı zənn edilən bir axının əslində gizli bloklanmalar yaratdığı görünəndə.
ORM rahatlıq versə də, arxa planda N+1 query fəlakəti baş verəndə.

Bunlar sintaksis problemləri deyil.

Bunlar sistem dizaynı problemləridir.

Yəni mühəndislik, kodun tək bir anda işləməsini yox, zaman içində yaşamasını
düşünməkdir.

Bu cümlə vacibdir: yaxşı mühəndis kodu yalnız yazmır, onun gələcək davranışını
da əvvəlcədən düşünür.

### **Tutorial mədəniyyəti niyə bəzən təhlükəlidir?**

Məsələnin bir tərəfi də müasir öyrənmə formasındadır. İnternetdə proqramlaşdırma
öyrənmək əvvəlkindən xeyli asandır. Bu çox böyük üstünlükdür. Amma onun gizli
bir riski də var: insanlar çox vaxt nəticəni təkrarlamağı anlayışla səhv
salırlar.

Bir tutorial açılır. Müəllim addım-addım gedir. Sən də eyni addımları
təkrarlayırsan. Proyekt ayağa qalxır. Hər şey işləyir. Bu nöqtədə insana elə
gəlir ki, artıq mövzunu başa düşdü. Halbuki çox vaxt o, sadəcə başqa birinin
qərarlarını təqlid edib.

Bu fərq çox böyükdür.

Bir şeyin necə qurulduğunu izləmək ilə niyə məhz belə qurulduğunu anlamaq
arasında uçurum var.

Məsələn, biri sənə [[controller]], [[service]], [[repository]] qatları ilə bir
API qurmağı göstərə bilər. Sən də onu eyni formada yaza bilərsən. Amma sual
budur: niyə bu qatlar var? Hansı məsuliyyət harada bitir? Repository həqiqətən
lazımdır, yoxsa sadəcə pattern kimi təkrarlanır? Service qatında
[[business logic]] var, yoxsa sadəcə metod ötürülür? Controller yalnız [[HTTP]]
sərhədidirmi, yoxsa içinə domain qərarları da qarışıb? ORM istifadə olunur, amma
onun yaratdığı query davranışına nə dərəcədə nəzarət var?

Əgər bunları soruşmursansa, sən pattern tətbiq etmirsən; sən pattern görüntüsü
yaradırsan.

Bu, çox vacib fərqdir.

Senior səviyyə çox vaxt yeni texnologiya bilməkdən yox, qərarların səbəbini görə
bilməkdən başlayır.

### **Kompüter elmləri nəzəriyyəsi niyə real işdə də vacib qalır?**

Bəzən belə bir yanlış təsəvvür olur ki, nəzəriyyə universitet üçündür, iş həyatı
isə tamam başqa şeydir. Sanki [[alqoritm]]lər, data strukturları, operating
systems, concurrency, memory modeli, abstraction, computational thinking kimi
mövzular akademik yükdür; “əsl iş” isə yalnız API yazmaq, framework qurmaq,
ticket bağlamaqdır.

Bu yanaşma çox qısagörəndir.

Çünki real iş mühitində sən hər gün nəzəriyyənin sırf kitab versiyası ilə
qarşılaşmırsan, amma onun nəticələri ilə daim qarşılaşırsan.

Məsələn, düzgün [[data structure]] seçimi sırf alqoritm dərsliyi məsələsi kimi
görünə bilər. Amma böyük kolleksiya üzərində tez-tez [[lookup]] edəcəksənsə, bu
birdən-birə performans və memory davranışı məsələsinə çevrilir. Concurrency
[[əməliyyat sistemi]] mövzusu kimi görünə bilər, amma production-da
[[race condition]] çıxanda bu artıq biznes problemidir. Caching “performans
optimizasiyası” başlığı kimi görünə bilər, amma [[cache invalidation]] səhv
qurulanda problem [[correctness]] səviyyəsinə keçir. ORM “developer rahatlığı”
kimi görünə bilər, amma SQL-in necə işlədiyini bilmirsənsə, abstraction səni
qorumaq əvəzinə korlaşdırır. Async/await rahat sintaksis kimi görünə bilər, amma
[[execution model]]-i başa düşmədən istifadə olunanda sistemə sürət yox,
mürəkkəblik gətirə bilər.

Başqa sözlə, nəzəriyyə iş həyatına birbaşa “dərs adı” kimi gəlmir. O, qərarvermə
qabiliyyəti kimi gəlir.

Kompüter elmləri biliyinin əsas dəyəri də budur. O sənə hər şeyi əzbərlətmir. O
sənə sistemi necə düşünəcəyini öyrədir.

### **Mühəndislik prinsipləri əslində nəyi qoruyur?**

İnsanlar tez-tez [[Clean Code]], [[SOLID]], design patterns, [[architecture]],
separation of concerns, high [[cohesion]], low coupling kimi anlayışları ya çox
romantikləşdirir, ya da tam əksinə, onları lazımsız “teorik şeylər” kimi görür.

Hər iki yanaşma səhvdir.

Bu prinsiplər estetik zövq üçün yaranmayıb. Məqsəd “kod gözəl görünsün” deyil.
Məqsəd dəyişiklik xərci idarə olunsun, risk lokallaşdırılsın, sistemin
anlaşılması ucuzlaşsın, təsir radiusu kiçilsin, davranış proqnozlaşdırıla
bilsin.

Məsələn, low coupling şüar deyil. Bu, bir dəyişiklik edəndə neçə yerin
təsirlənəcəyini idarə etmə cəhdidir.

High cohesion də sırf “məzmun uyğunluğu” kimi yumşaq bir fikir deyil. Bu, bir
modulun həqiqətən bir mövzuya aid olub-olmadığını yoxlamaq üsuludur. Əgər bir
class içində həm validation, həm persistence, həm cache management, həm
notification, həm mapping, həm də [[authorization]] qarışıbsa, problem sadəcə
“kod çirkindir” deyil. Problem odur ki, sən dəyişiklik sərhədini itirmisən.

SOLID prinsipləri də bu səbəbdən vacibdir. Onlar ehkam deyil. Onlar uzunömürlü
sistemlərdə təkrarlanan ağrıların ümumiləşdirilmiş nəticəsidir.

Design patterns də elədir. Pattern o demək deyil ki, hər problemi tanış bir
forma salmalısan. Pattern o deməkdir ki, sən müəyyən tipli problemin daha əvvəl
hansı strukturla həll edildiyini bilirsən. Amma onu kor-koranə yox, kontekstə
uyğun tətbiq edirsən.

Yəni prinsip bilmək, qayda əzbərləmək deyil. Problem görünüşünü tanımaqdır.

### **Niyə bir çox proqramçı müəyyən nöqtədən sonra dayanar?**

Çünki başlanğıcda sürətli inkişafı təmin edən vərdişlər bir müddətdən sonra
insanın qarşısını kəsir.

Əvvəldə tez kod yazmaq üstünlükdür. Sonra düşünmədən tez kod yazmaq problemə
çevrilir.

Əvvəldə hər şeyi bir faylda yığmaq daha sürətli görünür. Sonra bu, dəyişikliyin
qarşısını alır.

Əvvəldə framework-ün “magiyası” rahatlıq verir. Sonra onun arxa planını bilməmək
insanı qərarsız edir.

Əvvəldə copy-paste ilə feature çıxarmaq effektiv görünür. Sonra sistemdə
təkrarlanan məntiq partlayır.

Əvvəldə “çox qatlı arxitektura” yazmaq peşəkar görünür. Sonra məlum olur ki,
qatların yarısı heç bir semantik dəyər daşımır.

Yəni inkişafın növbəti mərhələsi daha çox kod yazmaqdan yox, daha düzgün
sərhədlər görməkdən keçir.

Bu nöqtədə artıq dil biliyi təkbaşına kifayət etmir.

Sənə abstraksiya hissi lazımdır. Sənə sistem düşüncəsi lazımdır. Sənə model
qurmaq bacarığı lazımdır. Sənə [[trade-off]] görmək bacarığı lazımdır. Sənə “nə
işləyir?”dən əlavə, “nə uzunömürlüdür?”, “nə izaholunandır?”, “nə nəzarət
altındadır?” suallarını vermək vərdişi lazımdır.

Mühəndislik bu suallarla başlayır.

### **Bu məqalənin əsas xətti**

Bu yazıda bizim əsas məqsədimiz proqramlaşdırmanı kiçiltmək deyil. Sintaksis
vacibdir. Dillər vacibdir. Framework-lər vacibdir. API-lər, ORM-lər, caching,
concurrency modelləri, memarlıq seçimləri, patternlər — bunların hamısı
vacibdir. Amma bunların hamısı yalnız o halda real dəyər yaradır ki, sən onları
bir sistemin içində görə biləsən.

Çünki real iş mühitində səndən gözlənilən şey yalnız kod yazmaq deyil.

Səndən gözlənilən şey qərar verməkdir.

Nəyi harada yerləşdirmək. Nəyi abstraksiya etmək, nəyi etməmək. Nəyi [[generic]]
qurmaq, nəyi konkret saxlamaq. Nəyi cache-ləmək, nəyi [[source of truth]] kimi
saxlamaq. Harada [[sync]] qalmaq, harada async olmaq. Harada pattern tətbiq
etmək, harada sadə həll seçmək. Harada performance problemi həqiqidir, harada
hələ erkəndir. Harada architecture lazımdır, harada sadə struktur kifayətdir.

Bunların heç biri yalnız sintaksis sualı deyil.

Bunlar mühəndislik suallarıdır.

Və məhz buna görə “Kompüter Elmləri Nəzəriyyəsindən Real İş Mühitinə” keçid
sadəcə akademik bilikdən sənayeyə keçid deyil. Bu, daha dərin bir keçiddir:
alətləri tanımaqdan sistemləri anlamağa, kod parçaları yazmaqdan uzunömürlü
həllər qurmağa, “necə?” sualından “niyə məhz belə?” sualına keçiddir.

Bu məqalənin qalan hissələri də məhz bu keçidi açacaq.

Növbəti hissədə bir addım da irəli gedəcəyik: **proqram yazmaqla sistem qurmaq
arasındakı fərq** harada başlayır və niyə bir çox komanda məhz bu sərhədi
görmədiyi üçün texniki borcun altında qalır.

## **II hissə — Proqram yazmaqla sistem qurmaq arasındakı fərq**

Proqram yazmaq və sistem qurmaq ilk baxışda bir-birinin davamı kimi görünür.
Hətta çox adam uzun müddət bunların ayrı bacarıqlar olduğunu hiss etmir. Çünki
bir neçə feature yazıb işlədən proqramçı təbii olaraq düşünür ki, artıq sistem
də qura bilir. Halbuki real iş mühitində məhz bu nöqtədə böyük fərq ortaya
çıxır: proqram yazmaq lokal nəticə yaratmaqdır, sistem qurmaq isə davranışı
idarə etməkdir.

Bu fərqi düzgün görməyən komandalarda çox maraqlı bir paradoks yaranır. Hər şey
ayrı-ayrılıqda işləyir, amma bütöv sistem rahat yaşamır. Endpoint işləyir, amma
yük altında boğulur. [[Məlumat bazası]] sorğunu qaytarır, amma artan data ilə
[[latency]] yüksəlir. Kod oxunur, amma dəyişəndə hər tərəfə toxunur. Feature tez
çıxır, amma üçüncü iterasiyadan sonra hər yeni dəyişiklik əvvəlkindən daha baha
başa gəlir. Yəni problem artıq “kod yaza bilmirik” deyil. Problem budur ki,
yazdığımız şeyin sistem kimi davranışını əvvəlcədən düşünməmişik.

Bu məqalənin əsas mövzusu da məhz buradadır: kompüter elmləri nəzəriyyəsindən
real iş mühitinə keçid, əslində, təkcə bilik artımı deyil; düşüncə səviyyəsinin
dəyişməsidir. O dəyişiklik də çox vaxt proqram parçasından sistem davranışına
keçidlə başlayır.

### **Proqram parçası konkret məqsədə xidmət edir, sistem isə zaman içində yaşayır**

Sadə desək, proqram parçası bir işi görmək üçündür. Sistem isə o işi sabah da,
gələn ay da, fərqli yüklə də, fərqli istifadəçi davranışı ilə də, yeni
tələblərlə də idarə edə bilməlidir.

Məsələn, bir “login” funksiyası yazmaq çətin görünməyə bilər. İstifadəçi email
və şifrə göndərir, sistem yoxlayır, token qaytarır. Bu, proqram yazmaq
səviyyəsində normal bir məsələdir. Amma real sistemdə login artıq tək bir
funksiya deyil. Orada [[rate limiting]] var, [[brute force]] riskləri var,
[[audit log]] var, [[token expiry]] var, [[refresh token]] strategiyası var,
cache və [[sessiya]] davranışı var, [[device management]] ola bilər,
authorization modeli ilə əlaqə var, [[failure case]]-lər var, [[observability]]
var. Üstəlik, bütün bunlar təhlükəsizlik, performans və maintainability
sərhədləri içində qurulmalıdır.

Burada artıq fərq hiss olunur. Bir endpoint yazmaq başqa şeydir, authentication
subsystem qurmaq başqa şey.

Eyni şeyi sifariş yaratmaq, ödəniş axını, exam session management, inventory
update, notification pipeline, file processing, report generation kimi bütün
real biznes axınlarında görmək olar. İlk versiyada məsələ sadə görünür. Sonra
domain qaydaları artır. Sonra concurrent request-lər gəlir. Sonra [[retry]]-lər,
[[timeout]]-lar, partial failure-lar, [[consistency]] məsələləri, cache
problemləri, [[background processing]] ehtiyacı, transaction sərhədləri,
monitoring tələbi ortaya çıxır. Və birdən məlum olur ki, başlanğıcda sadə
görünən feature əslində sistem davranışının bir hissəsi imiş.

Senior mühəndislik baxışı məhz burada fərqlənir. O, kodu tək bir funksiyanın
uğuru ilə qiymətləndirmir. O baxır ki, bu qərar sabah sistemi necə
təsirləndirəcək.

### **[[Local correctness]] ilə [[system correctness]] eyni şey deyil**

Bir çox proqramçı ilk mərhələdə düzgün olaraq local correctness üzərinə
fokuslanır. Yəni yazdığı metod öz işini düzgün görürmü? Gələn input-a doğru
output verirmi? Null case-ləri nəzərə alırmı? Error qaytarırmı? Bu vacibdir.
Hətta zəruridir. Amma sistem qurmaq üçün yetərli deyil.

Çünki system correctness daha böyük sualdır. Burada artıq tək bir metodun doğru
işləməsi kifayət etmir. Suallar dəyişir:

Bu əməliyyat eyni anda iki dəfə çağırılanda nə baş verir?

Bu data bir yerdə update olunanda başqa yerdə stale qalırmı?

Bu request yarıda qırılanda sistem inconsistent vəziyyətdə qalırmı?

Bu service cavab verməyəndə bütün flow dayanırmı?

Bu cache silinməyəndə istifadəçi köhnə məlumat görürmü?

Bu async əməliyyat bitmədən istifadəçiyə success qaytarılırsa, sonradan
uğursuzluq necə idarə olunur?

Bu ORM query-si data az olanda normaldır, amma milyonlarla sətirdə necə
davranacaq?

Bu API [[contract]]-i dəyişəndə neçə consumer qırılacaq?

Bunlar artıq “kod düz işləyir?” sualı deyil. Bunlar sistemin bütöv halda düzgün
davranıb-davranmadığı suallarıdır.

Kompüter elmləri nəzəriyyəsinin real dəyəri də çox vaxt burada görünür.
Concurrency, consistency, [[complexity]], [[state management]],
[[data modeling]], [[failure handling]] kimi mövzular bir dərs başlığı kimi yox,
sistemin doğru davranışının şərti kimi qarşımıza çıxır.

### **Sistem dizaynı “böyük şirkət mövzusu” deyil**

Bəzən belə düşünülür ki, sistem dizaynı ancaq çox böyük platformalarda,
milyonlarla istifadəçi olan şirkətlərdə lazımdır. Guya kiçik və orta məhsullarda
əsas olan sadəcə feature çıxarmaqdır. Bu fikir praktikada çox baha başa gəlir.

Çünki sistem dizaynı yalnız scale məsələsi deyil. Sistem dizaynı məsuliyyətlərin
necə bölündüyü, komponentlərin necə əlaqə qurduğu, məlumatın necə axdığı,
dəyişikliklərin necə idarə olunduğu, səhvlərin necə lokallaşdırıldığı ilə
bağlıdır. Bunlar isə tətbiq kiçik olanda da vacibdir.

Kiçik bir məhsulda belə əgər business logic controller-lərə səpələnibsə,
validation müxtəlif yerlərdə təkrarlanırsa, data access qaydaları service-lərlə
qarışırsa, caching sonradan “birdən sürət artsın” deyə əlavə olunursa, ORM-in
arxa planda yaratdığı query-lərə heç kim baxmırsa, async əməliyyatlar ardıcıllıq
zəmanəti olmadan qurulursa, sistemin ölçüsü kiçik olsa belə, onun dəyişiklik
xərcini sürətlə böyüdəcəksiniz.

Deməli, sistem dizaynı “böyük trafik”dən əvvəl də lazımdır. Çünki o, ilk növbədə
miqyasdan çox aydınlıq və idarəolunma məsələsidir.

### **Real sistemdə hər texniki qərarın görünməyən yan təsiri olur**

Tutorial layihələrdə qərarlar çox vaxt xərcsiz görünür. İstənilən yerdə bir
service yaratmaq, bir helper əlavə etmək, bir async yazmaq, bir cache qoşmaq,
bir ORM relation-u eager load etmək rahat görünür. Amma real sistemdə qərarın
təkcə birbaşa nəticəsi olmur; onun ikinci və üçüncü dərəcəli təsirləri də olur.

Məsələn, ORM istifadə etmək sürətli development verir. Amma bu, SQL-dən
uzaqlaşmaq demək deyil. Əksinə, SQL-i başa düşməyən komanda ORM altında gizlənən
problemləri daha gec görür. Bir relation-u “sadəcə gətir” deyə açmaq development
zamanı problemsiz görünə bilər, amma sonradan query explosion yarada bilər. N+1
problemi çox vaxt ORM rahatlığının arxasında gizlənir. Burada məsələ ORM-in pis
olması deyil. Məsələ budur ki, sistem qurmaq üçün abstraction-ın altında nə baş
verdiyini bilməlisən.

Eyni şey caching üçün də keçərlidir. Cache performansı xilas edə bilər, amma
eyni anda correctness riskini də artıra bilər. “Məlumatı tez verək” ideyası
yaxşıdır, amma source of truth haradadır? Cache nə vaxt invalid olur? Bir neçə
node varsa, onların davranışı necə sinxronlaşır? Yəni cache sadəcə bir
optimization aləti deyil; o, data flow və consistency qərarıdır.

API dizaynı da elədir. Sadəcə endpoint yazmaq kifayət deyil. Contract-in
sabitliyi, versiyalama ehtiyacı, [[idempotency]], [[pagination]],
[[error shape]], retry təhlükəsizliyi, timeout davranışı, authorization
sərhədləri kimi mövzular birbaşa sistem düşüncəsi tələb edir.

Burada əsas fikir budur: sistem qurmaq o deməkdir ki, sən aləti istifadə etməklə
kifayətlənmirsən, onun sistem daxilində hansı nəticələri doğuracağını da hesaba
qatırsan.

### **Data struktur və alqoritm bilikləri burada niyə yenidən qayıdır?**

Bir çox adam data structure və alqoritm mövzularını yalnız interview aləti kimi
görür. Sanki onlar ancaq [[LeetCode]] tipli suallar üçündür. Əslində isə bu
mövzuların real işdəki dəyəri daha dərin və daha sakit şəkildə ortaya çıxır.

Sistem qurmaq o deməkdir ki, məlumat necə saxlanılır, necə tapılır, necə
dəyişir, necə ötürülür və hansı qiymətə başa gəlir — bunları anlayırsan.

Məsələn, bir kolleksiyada lookup tezliyi yüksəkdirsə, sırf siyahı ilə işləmək
rahat görünə bilər, amma müəyyən həddən sonra set və ya hash-based struktur daha
doğru seçim olur. Sıralı data lazımdırsa, başqa trade-off yaranır. Bir
əməliyyatın zaman mürəkkəbliyi təkcə nəzəri rəqəm deyil; o, istifadəçi gözləmə
vaxtına, CPU istifadəsinə, [[memory footprint]]-ə, [[database round-trip]]
sayına çevrilir.

Ən maraqlısı budur ki, real sistemlərdə alqoritm problemi çox vaxt “çətin sual”
formasında gəlmir. O, bəzən çox adi görünən yerdə gəlir: yanlış filter
strategiyası, lazımsız [[tam scan]], səhv [[paging]] yanaşması, çox ağır
[[sort]], lazımsız [[serialization]], yanlış [[batch]] ölçüsü, qeyri-effektiv
background processing. Bunların hər biri kompüter elmləri təməlinin nə qədər
praktik olduğunu göstərir.

Yəni nəzəriyyə bu mərhələdə səndən textbook cavabı istəmir. O səndən cost model
hissi istəyir.

### **Sinxron, [[asinxron]] və thread məsələsi yalnız sintaksis mövzusu deyil**

Müasir proqramlaşdırmada ən çox səthi öyrənilən mövzulardan biri də budur. Çox
adam async/await sintaksisini öyrənir və düşünür ki, məsələ həll olundu. Halbuki
bu, yenə də yalnız səthdir.

Sistem qurmaq baxımından əsas suallar bunlardır: bu əməliyyat blocking-dir,
yoxsa [[non-blocking]]? Bu iş CPU-bound-dur, yoxsa I/O-bound? Thread nə vaxt
tutulur? Thread pool necə davranır? Eyni anda çox request gələndə sistem neçə
işi daşıya bilər? Gözləmə və hesablama işi necə ayrılır? [[Shared state]] varsa,
race condition ehtimalı nədir? Background work hansı zəmanətlə işləyir?
[[Cancellation]], timeout, retry kimi şeylər düşünülübmü?

Bir endpoint-i async etmək bəzən sadəcə düzgün sintaksis seçimidir. Amma sistem
səviyyəsində asinxronluq daha böyük məsələdir. Bu, execution model məsələsidir.

Məsələn, imtahan platformasında istifadəçi cavabı submit edir. Əgər submit
zamanı həm database write, həm score pre-processing, həm audit log, həm
notification, həm analytics event, həm də cache update sinxron ardıcıllıqla
işləyirsə, latency artır. Bu hissələrin hansı request daxilində qalmalıdır,
hansı background-a keçməlidir, hansının [[exactly-once]] zəmanəti lazımdır,
hansında eventual consistency kifayətdir — bax, bunlar artıq sistem
qərarlarıdır.

Deməli, async/sync mövzusu “hansı keyword yazım?” sualı deyil. Bu, sistemin
resurs davranışı və correctness sərhədləri ilə bağlıdır.

### **Arxitektura seçimi struktur yaratmaq deyil, sərhəd yaratmaqdır**

Sistem qurmaq haqqında danışarkən çox adamın ağlına dərhal arxitektura gəlir.
Layered architecture, [[MVC]], [[clean architecture]], [[hexagonal]],
[[microservices]], [[modular monolith]] və s. Amma burada da tez-tez bir
yanlışlıq olur: insanlar arxitekturanı görünən qovluq strukturu ilə səhv
salırlar.

Halbuki arxitektura ilk növbədə qovluq düzümü deyil. O, məsuliyyətlərin
sərhədidir.

MVC istifadə etmək sənə avtomatik yaxşı dizayn vermir. Service, repository,
controller qovluqları açmaq da elə. Əgər domain qərarları yenə də presentation
qatına sızırsa, data access qaydaları business logic ilə qarışırsa, validation
bir neçə sərhəddə təkrarlanırsa, naming semantik dəyər daşımırsa, o zaman
struktur var, amma memarlıq yoxdur.

Senior yanaşma burada daha sərtdir. O soruşur:

Bu sərhəd niyə mövcuddur?

Bu hissə hansı dəyişikliyi absorb etməlidir?

Bu dependency hansı istiqamətdə axmalıdır?

Bu komponent business qaydanı daşıyır, yoxsa sadəcə texniki vasitədir?

Bu modul öz daxilində cohesive-dirmi?

Bu service həqiqətən service-dir, yoxsa utility yığınıdır?

Bu API layer biznes qaydasını idarə edir, yoxsa sadəcə transport sərhədidir?

Yəni sistem qurmaqda arxitektura forma deyil, qərarların xəritəsidir.

### **Ən böyük fərq: yaxşı proqramçı kod yazır, yaxşı mühəndis sərhəd çəkir**

Bu hissənin mərkəzi fikri bəlkə də məhz budur.

Proqram yazmaq bacarığı səni məhsuldar edə bilər. Amma sistem qurmaq üçün daha
vacib bacarıq sərhəd çəkməkdir. Harada bir məsuliyyət bitir, harada digəri
başlayır; harada məlumatın sahibi budur, harada başqa komponent; harada sinxron
cavab lazımdır, harada eventual consistency kifayətdir; harada ORM rahatlıqdır,
harada birbaşa query daha doğrudur; harada caching dəyər yaradır, harada sadəcə
problemi gizlədir; harada pattern kömək edir, harada artıq səs-küyə çevrilir.

Bu sərhədləri görə bilməyən adam çox işləyə bilər, amma sistem qurmaqda tez
yorular. Çünki o, hər problemi eyni səviyyədə həll etməyə çalışacaq. Hər şey ya
“sadə funksiya” olacaq, ya da əksinə, lazımsız dərəcədə abstraktlaşdırılacaq.
Hər iki halın sonunda sistem ya dağınıq olur, ya da boğucu.

Real iş mühitində isə tələb olunan mühəndislik prinsipləri məhz bu orta xətti
tapmaqdır. Bu xətt nə teoriyanı şüar kimi istifadə edir, nə də praktikaya bəhanə
edib prinsipsiz işləyir. O, nəzəriyyəni qərar keyfiyyətinə çevirir.

Bu səbəbdən proqram yazmaqla sistem qurmaq arasındakı fərq təkcə miqyas fərqi
deyil. Bu, düşüncə fərqidir. Birində sən problemi birbaşa həll edirsən. O
birində isə problemin sistem daxilində necə yaşaya biləcəyini hesablayırsan.

Növbəti hissədə bu düşüncə fərqinin daha dərin qatına keçəcəyik: **abstraksiya,
model, [[invariant]] və trade-off** anlayışları əslində nədir və niyə
mühəndislik yetkinliyi bu anlayışları düzgün hiss etməkdən başlayır.

## **III hissə — Abstraksiya, model, invariant və trade-off: mühəndisliyin görünməyən təməli**

Real iş mühitində güclü mühəndisi digərlərindən fərqləndirən şey çox vaxt onun
neçə dil bilməsi, neçə framework istifadə etməsi, ya da neçə pattern adı
sadalaya bilməsi olmur. Əsas fərq daha dərin yerdə yaranır: o, sistemi hansı
düşüncə vahidləri ilə görür. Yəni onun beynində kod sadəcə sintaktik bloklardan
ibarət deyil. O, arxada abstraksiyalar görür, modellər qurur, dəyişməməli olan
qaydaları ayırd edir və hər texniki seçimin əslində bir trade-off olduğunu
anlayır.

Bu, nəzəri görünə bilər. Amma peşəkar mühəndisliyin ən praktik qatlarından biri
məhz budur. Çünki sistemlər əsasən elə burada qırılır. Kod çox vaxt sintaksis
səhvindən deyil, yanlış modeldən əziyyət çəkir. Komandalar çox vaxt texnologiya
çatışmazlığından deyil, sərhədləri düzgün qura bilmədikləri üçün yavaşlayır. Bir
çox arxitektura problemi də əslində səhv seçilmiş abstraksiyanın və ya
görünməyən trade-off-ların gec başa düşülmüş nəticəsidir.

Bu səbəbdən kompüter elmləri nəzəriyyəsindən real iş mühitinə keçid yalnız “daha
çox texnologiya bilmək” deyil. Bu, düşüncə aparatının güclənməsidir. O aparatın
əsas elementləri arasında da abstraksiya, model, invariant və trade-off xüsusi
yer tutur.

### **Abstraksiya sadələşdirmə deyil, doğru sərhəd seçməkdir**

Abstraksiya haqqında çox danışılır, amma az hallarda həqiqətən dəqiq anlaşılır.
Çox adam onu “detalları gizlətmək” kimi öyrənir. Bu, səhv deyil, amma kifayət də
deyil. Çünki real mühəndislikdə abstraksiya sadəcə detalları gizlətmək üçün
istifadə olunan texnika deyil; o, problemi hansı səviyyədə idarə edəcəyini
seçmək bacarığıdır.

Sistem böyüdükcə hər detalı eyni anda görmək mümkün olmur. Hətta bu, zərərlidir.
Güclü mühəndis sistemin bütün səviyyələrini bilir, amma hər problemi onun uyğun
səviyyəsində düşünür. Məsələn, ödəniş axını qurulanda hər şeyə eyni anda baxmaq
olar: HTTP request, validation, database write, transaction, provider
integration, retry, idempotency, audit log, notification. Ancaq bunların
hamısını bir funksiyanın içində saxlamaq sistemə nəzarət demək deyil. Bu, sadəcə
sərhədləri itirməkdir.

Abstraksiya burada vəziyyəti “gözəlləşdirmək” üçün yox, düşüncəni təmizləmək
üçün lazımdır. Ödənişin business qaydası ilə provider-in texniki inteqrasiyası
eyni məsuliyyət daşımır. İstifadəçi sorğusunun transport səviyyəsi ilə domain
qərarı eyni məkanın mövzusu deyil. Data-nın necə saxlanması ilə həmin data
üzərində hansı qaydanın işləməsi də eyni lay deyil. Bunları ayırmaq kodu bəzəmək
deyil, sistemi idarə oluna bilən hissələrə bölməkdir.

Yanlış abstraksiya isə bəzən abstraksiyanın olmamasından da pis nəticə verir.
Çünki o, mürəkkəbliyi azaltmır, sadəcə başqa yerə daşıyır. Məsələn, hər şeyi
generic etməyə çalışmaq çox “senior” görünə bilər. Amma business qaydası hələ
sabitləşməyibsə, vaxtından əvvəl qurulan universal qatlar sistemi elastik deyil,
əksinə sərt edir. Bu halda abstraksiya reallığı modelləşdirmir, reallığı məcburi
qəlibə salır.

Mühəndisliyin vacib dərslərindən biri də budur: abstraksiya həmişə artırılmalı
bir şey deyil. Bəzən ən düzgün qərar problemi konkret saxlamaqdır. Yəni yaxşı
mühəndis hər dəfə “bunu daha abstrakt yaza bilərəmmi?” deyə yox, “bu problem
hansı səviyyədə formalaşıbsa, onu orada saxlamaq daha doğrudurmu?” deyə düşünür.

### **Model sistemin içindən yox, problemin özündən çıxmalıdır**

Proqramçılar tez-tez kodu sistemin əsas reallığı kimi görməyə başlayırlar.
Halbuki kod reallığın özü deyil, onun modelidir. Bu fərq sadə görünə bilər, amma
çox şeyi dəyişir.

Model qurmaq o deməkdir ki, sən problemin təbiətini başa düşür və onu sistemdə
düzgün formaya salırsan. Bu, sadəcə [[entity]] adları seçmək deyil. Bu, real
dünyanın hansı qaydalarının sistemdə birinci dərəcəli rol oynadığını anlamaqdır.

Məsələn, “user”, “order”, “exam”, “attempt”, “payment”, “inventory item” kimi
sözlər yalnız data strukturu deyil. Bunların hər biri bir davranış və qayda
məkanı daşıyır. Əgər model yalnız field-lərdən ibarət görünürsə, çox vaxt domain
hələ tam görülməyib. Çünki real sistemdə obyektlər sadəcə məlumat daşımır; onlar
müəyyən vəziyyətlər, keçidlər, qadağalar və icazələr də daşıyır.

İmtahan sistemi buna yaxşı nümunədir. “Attempt” adlı bir anlayışı yalnız
database row kimi görmək kifayət etmir. Attempt-in nə vaxt başladığı, hansı
hallarda etibarsız sayıldığı, hansı status dəyişikliklərinin mümkün olduğu,
[[sessiya]] kəsiləndə nə baş verdiyi, vaxt cədvəli dəyişəndə hansı nəticənin
yaranacağı — bunlar attempt anlayışının öz modelinə daxildir. Əgər bütün bunlar
controller-lərə, helper-lərə, random service metodlarına səpələnirsə, problem
kod təşkilatı deyil, model zəifliyidir.

Eyni şey e-commerce, healthtech, fintech, education, logistics kimi bütün
sahələrdə keçərlidir. Sistem yalnız table-lər, endpoint-lər və response-lardan
ibarət deyil. O, bir reallığın riyazi olmayan, amma ciddi məntiqə sahib
modelidir.

Burada kompüter elmlərinin nəzəri hissəsi çox praktik kömək edir. Çünki nəzəri
düşüncə insanı “bu necə işləyir?” sualından əlavə, “bu əslində nəyi təmsil
edir?” nöqtəsinə gətirir. Güclü model də məhz buradan yaranır. O, texnologiyadan
çıxmır. O, problemin daxili məntiqindən çıxır.

### **İnvariant sistemin görünməyən skeletidir**

Bir sistemin uzunömürlü olub-olmaması çox vaxt onun invariant-larının nə qədər
aydın müəyyənləşdirilməsindən asılı olur. İnvariant anlayışı daha az
populyardır, amma mühəndislikdə son dərəcə mərkəzidir.

İnvariant — dəyişən axınların içində dəyişməməli olan qaydadır.

Bir çox biznes sistemində belə qaydalar var. Məsələn, mənfi balans müəyyən
hallarda qadağandır. Tamamlanmış sifariş geri “draft” vəziyyətinə düşməməlidir.
Bir attempt eyni anda həm “completed”, həm də “active” ola bilməz. Ödəniş
təsdiqlənməmişsə, resurs aktivləşməməlidir. Eyni source of truth-dan çıxan iki
status bir-biri ilə ziddiyyət təşkil etməməlidir.

Bu qaydalar bəzən cədvəldə constraint kimi görünür, bəzən domain service-də
qərar kimi, bəzən [[state transition]] qaydası kimi, bəzən transaction
sərhədində qorunur. Amma harada saxlanmasından asılı olmayaraq, invariant
sistemin sabitliyini qoruyur.

Zəif sistemlərdə invariant-lar açıq görünmür. Onlar ya insanın beynində qalır,
ya müxtəlif yerlərdə yarımçıq təkrarlanır, ya da yalnız UI qatında qorunmağa
çalışılır. Bir müddət sonra bu qaydalar parçalanır və sistem gözlənilməz
davranmağa başlayır. Məhz bu nöqtədə bug-lar “texniki nasazlıq” kimi görünür,
amma onların kökü çox vaxt invariant-ların sistemli şəkildə ifadə olunmamasına
gedib çıxır.

Senior mühəndislik burada özünü çox aydın göstərir. Güclü mühəndis yeni feature
əlavə etməzdən əvvəl hansı invariant-ların qorunmalı olduğunu hiss edir. O, bir
qaydanın sadəcə “validation” olmadığını anlayır. Bəzən bu, domain-in əsas
həqiqətidir. Həmin həqiqət harada yaşamalıdırsa, orada yaşamalıdır. Əks halda
sistem özünü itirir.

Bu səbəbdən yaxşı kod təkcə oxunaqlı kod deyil. Yaxşı kod həm də sistemin
dəyişməməli həqiqətlərini daşıyan koddur.

### **Trade-off görməyən mühəndis bir müddət sonra doqmatikləşir**

Peşəkar inkişafda ən vacib dönüşlərdən biri də budur: insan başa düşür ki,
texniki dünyada pulsuz qələbə çox azdır. Demək olar ki, hər düzgün seçim başqa
bir şeyin bahasına başa gəlir. Bu anlayış olmasa, mühəndislik tez-tez doqmatik
qərarlara çevrilir.

Bir nümunə ilə baxsaq, caching performansı yüksəldir, amma data freshness
riskini artırır. ORM development sürətini artırır, amma query davranışını
gizlədə bilər. Microservices deployment müstəqilliyi verə bilər, amma
[[distributed complexity]] yaradar. Async I/O resurs istifadəsini yaxşılaşdıra
bilər, amma flow observability-ni çətinləşdirə bilər. Güclü abstraction təkrar
istifadəni artırar, amma erkən qurulsa, sistemi ehtiyacdan artıq sərtləşdirər.
Tam normalization consistency-ni qoruyar, amma bəzi oxu ssenarilərində
performansı zəiflədə bilər. Denormalization oxunu sürətləndirər, amma update
kompleksliyini artıra bilər.

Yəni mühəndislik “ən yaxşı həll” tapmaqdan çox, kontekstə uyğun ən düzgün
kompromisi seçməkdir.

Bu çox fundamental dəyişiklikdir. Çünki başlanğıc səviyyədə insan adətən qayda
axtarır. O bilmək istəyir ki, “repository istifadə etmək doğrudurmu?”, “clean
architecture yaxşıdırmı?”, “[[inheritance]] pisdirmi?”, “SQL yazmaq daha
düzgündür, yoxsa ORM?”, “sync kod köhnə yanaşmadırmı?” və s. Bir müddət sonra
isə başa düşür ki, bu sualların çoxu təkcə “bəli” və “xeyr” ilə
cavablandırılmır. Cavab konteksdən asılıdır: sistemin ölçüsündən, komandanın
yetkinliyindən, məhsulun dəyişmə sürətindən, domain mürəkkəbliyindən, performans
profilindən, risk növündən, əməliyyat yükündən.

Trade-off düşüncəsi olmayan komanda bir müddət sonra şüarlarla işləməyə
başlayır. Biri deyir ki, “biz həmişə generic yazmalıyıq”, digəri deyir ki, “biz
həmişə clean architecture tətbiq etməliyik”, başqa biri deyir ki, “microservice
daha professional görünür”, bir başqası isə “raw SQL həmişə ORM-dən yaxşıdır”
qənaətinə gəlir. Bunların hamısı müəyyən şəraitdə doğru ola bilər, amma
universal həqiqət deyil.

Senior səviyyə burada özünü bir daha göstərir: yaxşı mühəndis texniki mövqeyi
ideoloji kimlik kimi daşımır. O, seçimin qiymətini və qazancını hesablayır.

### **Abstraksiya ilə sadəlik arasında incə bir xətt var**

Mühəndislikdə tez-tez paradoksal bir vəziyyət yaranır: insan sistemi daha təmiz
etmək istəyərkən onu daha mürəkkəb hala gətirir. Bunun səbəbi odur ki, sadəliklə
primitivlik, abstraksiya ilə dolaşıqlıq bir-birinə qarışdırılır.

Sadə sistem o demək deyil ki, az sinif var, az fayl var və hər şey bir yerdə
yazılıb. Bu, bəzən sadə görünən xaos olur. Amma bunun əksi də doğrudur: çox qat,
çox interface, çox generic container, çox wrapper istifadə etmək də avtomatik
yaxşı memarlıq demək deyil.

Əsl sadəlik anlaşılan sərhədlərdən gəlir.

Əgər bir modulun niyə mövcud olduğu aydındırsa, onun nəyi sahiblik etdiyi
görünürsə, dəyişiklik zamanı təsir radiusu proqnozlaşdırıla bilirsə, bu
sadəlikdir. Faylların sayı çox olsa da, sistem düşüncə baxımından yüngül qala
bilər. Amma əgər hər şey “çox təmiz görünmək” xatirinə formal qatlara bölünübsə,
məzmun sərhədlərlə uyğun gəlmirsə, o zaman sistem kağız üzərində səliqəli,
praktikada isə boğucu olur.

Burada yenə abstraksiya anlayışına qayıdırıq. Düzgün abstraksiya sadəliyi
artırır, yanlış abstraksiya isə sadəliyi imitasiya edir. Buna görə də güclü
mühəndislər forma ilə məzmunu ayırmağı bacarırlar. Onlar sadə görünən, amma
daxilən qarışıq sistemləri də tanıyırlar; strukturca böyük görünən, amma əslində
çox aydın olan sistemləri də.

### **Nəzəriyyənin real gücü burada hiss olunur**

Kompüter elmləri təməlini dərin mənimsəmiş mühəndisin üstünlüyü çox vaxt konkret
bir texnologiya anında deyil, məhz bu düşüncə qatlarında üzə çıxır. Çünki
nəzəriyyə ona alqoritm adı əzbərlətmək üçün yox, reallığı formal düşünmək üçün
lazımdır. Abstraksiya qurmaq, model seçmək, invariant qorumaq, trade-off
hesablamaq — bunların hamısı bir növ nəzəri düşüncə ilə praktik qərarın kəsişmə
nöqtəsidir.

Bu səbəbdən nəzəri baza ilə real iş mühiti arasında süni sərhəd çəkmək düzgün
deyil. Əksinə, güclü nəzəri baza praktikada daha ayıq qərar verməyə kömək edir.
O, insanı framework-ün içində itməkdən qoruyur. O, pattern-i dekorasiya kimi
tətbiq etməkdən saxlayır. O, optimizasiyanı yalnız sürət məsələsi kimi yox,
model və cost məsələsi kimi görməyə vadar edir. O, sinxron və asinxron yanaşmanı
keyword deyil, execution behavior kimi başa düşməyə imkan verir.

Mühəndislik prinsipləri də məhz burada canlılaşır. Onlar ayrıca mövzular
siyahısı kimi yox, qərarların keyfiyyətini artıran düşüncə alətləri kimi dəyər
qazanır.

Bu hissənin əsas nəticəsi budur: real iş mühitində güclü olmaq üçün yalnız
texniki alətlər toplamaq kifayət etmir. O alətləri daşıyan düşüncə sistemi
formalaşmalıdır. Abstraksiya problemi necə böləcəyini müəyyən edir. Model nəyin
əslində vacib olduğunu göstərir. İnvariant sistemin həqiqətlərini qoruyur.
Trade-off isə sənə hər seçimin bir qiyməti olduğunu xatırladır.

Bunlar görünməyən mövzulardır, amma peşəkar mühəndisliyin ən möhkəm
təməllərindən biridir.

## **IV hissə — [[obyekt-yönümlü proqramlaşdırma]], [[funksional proqramlaşdırma]] və [[procedural]] yanaşma: paradiqmaların savaşı yox, düşüncə alətlərinin düzgün seçimi**

Proqramlaşdırma dünyasında ən çox yanlış anlaşılan mövzulardan biri
paradiqmalardır. Bunun bir səbəbi texniki deyil, daha çox mədəniyyətlə bağlıdır.
İnsanlar çox tez-tez yanaşmaları alət kimi yox, mövqe kimi mənimsəyirlər. Biri
OOP tərəfdarı olur, digəri functional programming-i daha “təmiz” hesab edir,
başqası procedural yazmağı “sadə və real” sayır. Bir müddət sonra texniki seçim
mühəndislik qərarı olmaqdan çıxıb zövq, ideologiya və ya peşəkar imic məsələsinə
çevrilir.

Real iş mühitində isə bu cür yanaşma çox davamlı olmur. Çünki istehsal
səviyyəsində sistemlər paradiqma manifesti ilə yaşamır. Onlar düzgün sərhədlər,
aydın davranış, dəyişiklik xərcinin idarəsi və risklərin lokallaşdırılması ilə
yaşayır. Bu nöqtədə də əsas sual “ən yaxşı paradiqma hansıdır?” olmur. Əsas
məsələ budur: problem necə formalaşıb və onu hansı düşüncə modeli ilə daha
təmiz, daha dayanıqlı və daha izaholunan şəkildə həll etmək olar?

Kompüter elmləri nəzəriyyəsindən real iş mühitinə keçid burada özünü çox aydın
göstərir. Çünki təməlsiz yanaşmada insan paradiqmanı sintaksis səviyyəsində
öyrənir. Güclü mühəndislikdə isə paradiqma problemi necə modelləşdirdiyini,
state-i necə idarə etdiyini, asılılıqları necə azaltmağa çalışdığını və sistem
davranışını nə qədər proqnozlaşdırıla bilən etdiyini müəyyənləşdirir.

### **OOP nə üçün yarandı və niyə hələ də mərkəzi yer tutur?**

Object-Oriented Programming çox vaxt yalnız “class-lar, object-lər, inheritance”
kimi təqdim olunur. Bu, yenə də səthdir. OOP-nin real dəyəri sintaktik
strukturlarda deyil, model qurmaq imkanındadır. O, sistemdəki anlayışları təkcə
data konteyneri kimi yox, davranış daşıyıcısı kimi təşkil etməyə imkan verir.
Yəni obyekt yalnız field-lərin yığını deyil; o, eyni zamanda müəyyən qaydaların,
vəziyyətlərin və dəyişiklik mexanizmlərinin sahibidir.

Bu yanaşma xüsusilə biznes domeni daha zəngin olan sistemlərdə hələ də çox
güclüdür. Məsələn, payment, order, subscription, shipment, exam attempt,
booking, policy, claim kimi anlayışlar sadəcə məlumat saxlamır. Onların vəziyyət
keçidləri, qadağaları, icazələri, şərtləri və təsir radiusları olur. Bu cür
hallarda behavior ilə data-nı ayrı-ayrı yaşatmaq əvəzinə birlikdə modelləşdirmək
çox vaxt daha təbii olur. OOP-nin gücü də buradan gəlir: reallığı təkcə struktur
kimi yox, davranışla birlikdə təmsil edə bilir.

Amma OOP-nin gücü çox rahat şəkildə onun zəifliyinə də çevrilə bilir. Çünki
illər boyu bu yanaşma bir çox komandada sadəcə class istehsalı mədəniyyətinə
çevrilib. Hər şey üçün class, hər məsələ üçün interface, hər hərəkət üçün
service, hər service üçün base class, hər yerdə inheritance. Nəticədə sistem
obyekt yönlü olmur; sadəcə obyekt görüntülü olur. Domain model qurulmur,
əvəzində texniki qovluqlar və formal qatlar çoxalır.

Bu nöqtədə vacib fərqi görmək lazımdır: OOP class yazmaq deyil. OOP məsuliyyətin
və davranışın təbii sahibliyini müəyyənləşdirməkdir.

Əgər bir obyektin içinə aid olmayan məntiq dolursa, bu OOP deyil. Əgər obyekt
yalnız getter-setter daşıyır və bütün qərarlar başqa yerlərdə verilirsə, bu da
güclü model deyil. Əgər inheritance reuse adı ilə istifadə olunur, amma nəticədə
sistem daha sərt və daha qırılqan olur, burada artıq paradiqma kömək etmir,
əksinə sistemi ağırlaşdırır.

OOP ən yaxşı işlədiyi yerdə məsuliyyətləri məna baxımından bir araya gətirir. Ən
zəif işlədiyi yerdə isə sadəcə struktur görüntüsü yaradır.

### **Inheritance niyə tez-tez gücdən çox yükə çevrilir?**

Object-oriented dizaynda ən çox romantikləşdirilmiş vasitələrdən biri
inheritance olub. İlk baxışda çox cəlbedici görünür: ortaq davranışları yuxarıya
qaldırırsan, alt siniflər onu miras alır, kod təkrarı azalır. Kağız üzərində
səliqəli görünür. Praktikada isə inheritance çox vaxt sistemin dəyişiklik
qabiliyyətini aşağı salır.

Səbəb sadədir. Inheritance “is-a” münasibətini yalnız linqvistik səviyyədə yox,
davranış və gələcək dəyişiklik səviyyəsində də doğru tələb edir. Halbuki real
biznes sistemində bu münasibət çox vaxt sabit olmur. Bugünkü oxşarlıq sabah
fərqli istiqamətdə inkişaf edə bilər. O zaman yuxarı sinifdə toplanmış məntiq
alt siniflərin hamısı üçün eyni dərəcədə uyğun qalmır. Bir müddət sonra
override-lar artır, istisnalar toplanır, protected sahələr böyüyür, base class
əslində hamını daşıyan zəif bir kompromisə çevrilir.

Bu səbəbdən real iş mühitində [[composition]] çox vaxt inheritance-dən daha
sağlam seçim olur. Çünki composition davranışları sərt iyerarxiyada kilidləmir.
O, sistemi hissələrə bölür, birləşdirməyi asanlaşdırır və dəyişiklik zamanı
təsir radiusunu daha yaxşı idarə edir. Bu da mühəndisliyin əsas mövzularından
biri olan low coupling prinsipinə daha yaxındır.

Burada yenə eyni xətt qayıdır: məqsəd müəyyən texnikanı müqəddəsləşdirmək deyil.
Məqsəd gələcək dəyişikliklərə hansı strukturun daha dözümlü olduğunu görməkdir.

### **Functional Programming niyə bu qədər güclü təsir yaradıb?**

Functional Programming-in populyarlığı təkcə yeni dəb olduğu üçün yaranmadı.
Onun yüksəlişinin arxasında çox real səbəblər var. Müasir sistemlər getdikcə
daha çox concurrency, data transformation, asynchronous axınlar, paylanmış emal,
[[event-driven]] davranış və yan təsirlərin idarəsi kimi mövzularla işləyir. Bu
sahələrdə FP çox aydın üstünlüklər təqdim edir.

FP-nin əsas gücü state və [[side effect]]-lərlə daha intizamlı davranmasındadır.
Dəyişməz data, [[pure function]] yanaşması, input-output məntiqinin aydınlığı,
transformasiya zəncirlərinin sadəliyi və davranışın proqnozlaşdırıla bilməsi
sistemi həm test, həm reasoning, həm də concurrent icra baxımından daha sağlam
edə bilir.

Bu üstünlük xüsusilə data pipeline-larda, validation flow-larında, mapping
mərhələlərində, hesablama yönümlü modullarda, stream və event emalı
ssenarilərində çox aydın hiss olunur. Belə yerlərdə object-oriented model bəzən
lazımsız state və ceremony gətirir. Functional yanaşma isə problemi daha şəffaf
şəkildə açır: data gəlir, transformasiyadan keçir, nəticə çıxır.

FP həm də çox mühüm bir zehni intizam öyrədir: side effect haradadır, harada
deyil. Bu, real sistemdə çox qiymətlidir. Çünki sistem qırılmalarının böyük
hissəsi görünməyən təsirlərdən yaranır. Bir funksiya yalnız hesablamalı olduğu
yerdə həm də log yazırsa, cache dəyişirsə, network çağırışı edirsə və state
mutasiya edirsə, onu başa düşmək, test etmək və dəyişmək daha çətinləşir. FP bu
qarışıqlığı azaltmağa kömək edir.

Amma burada da eyni səhvə düşmək asandır. Functional Programming bəzən o qədər
estetik dillə təqdim olunur ki, insanlar onu hər şeyin universal həlli kimi
görməyə başlayırlar. Halbuki bu da yanlışdır. FP bütün problemləri “daha yaxşı”
həll etmir. O, müəyyən tip problemlərdə daha güclü düşüncə forması verir. Lakin
domain modelin davranış mərkəzli olduğu, vəziyyət keçidlərinin aydın obyekt
sərhədlərində saxlanmasının faydalı olduğu yerlərdə sırf functional yanaşma
bəzən sistemi süni şəkildə parçalayır.

Yəni FP-nin gücü onun hər yerə tətbiq olunmasında deyil. Onun gücü mühəndisə
state, mutation və side effect haqqında daha ciddi düşünməyi öyrətməsindədir.

### **Procedural yanaşma niyə hələ də yaşayır?**

Programming paradiqmaları haqqında danışarkən procedural üslub bəzən köhnəlmiş,
ibtidai, hətta “junior yanaşma” kimi təqdim olunur. Halbuki bu, çox səthi
baxışdır. Procedural thinking proqramlaşdırmanın ən təməl formalarından biridir
və bu gün də bir çox sahədə həm təbii, həm effektiv, həm də ən aydın yoldur.

Xüsusilə ardıcıl addımlardan ibarət proseslərdə procedural kod hələ də çox
dəyərlidir. Request handling flow-ları, pipeline-lar, script-lər, batch
processing, ETL işləri, deployment automation, orchestration ssenariləri, bəzi
API axınları procedural düşüncə ilə çox yaxşı qurulur. Çünki belə hallarda əsas
məsələ obyekt davranışından çox, əməliyyatın ardıcıllığını, mərhələlərini və
nəzarət axınını aydın saxlamaq olur.

Əslində object-oriented və functional yanaşmaların çoxu da tam procedural
düşüncəni ortadan qaldırmır. Sadəcə onu başqa qatlara daşıyır. Məsələn, domain
model daxilində OOP işləyə bilər, amma application service səviyyəsində yenə də
procedural orchestration lazım olur. Eyni şəkildə, data transformation-lar
functional ola bilər, amma sistemin ümumi flow-u procedural şəkildə idarə
olunar.

Bu çox vacib müşahidədir: real sistemlər çox vaxt tək bir paradiqma ilə yaşamır.
Onlar səviyyədən səviyyəyə fərqli düşüncə formaları istifadə edir.

Ona görə də procedural yanaşmanı “aşağı səviyyə”, OOP-ni “klassik”, FP-ni “daha
ağıllı” kimi təsnif etmək mühəndislik baxışına uyğun deyil. Əsas məsələ
problemin təbiətidir.

### **Real sistemlərdə paradiqmalar qarışır, amma nəzarətsiz yox**

Praktikada güclü sistemlər çox vaxt hibrid xarakter daşıyır. Məsələn, bir
e-commerce platformasında order və payment kimi anlayışlar domain model kimi OOP
yanaşması ilə formalaşa bilər. Validation, mapping və bəzi hesablamalar
functional tərzdə qurula bilər. Request-in ümumi axını isə procedural
orchestration kimi tətbiq oluna bilər. Eyni sistemdə background worker-lər daha
stream-oriented və event-driven düşünülə bilər, data access hissəsində isə ORM
və ya raw SQL-lə bağlı daha mexaniki qərarlar verilə bilər.

Bu qarışıq təbiidir. Problem qarışıq olması deyil. Problem nəzarətsiz qarışıq
olmasıdır.

Əgər komanda harada hansı paradiqmanın işlədiyini hiss etmirsə, sistem sürətlə
anlaşılmaz olur. Məsələn, domain modeli sırf data container-lərdən ibarətdir,
amma business logic random util metodlarda gəzir. Ya da functional görünmək üçün
hər şey function-a bölünür, amma state harada dəyişdiyi artıq aydın olmur. Ya da
service-lər procedural flow saxlayır, amma arada inheritance ilə qurulmuş zəif
abstraksiyalar qərarları gizlədir. Nəticədə sistem həm çox qatlı görünür, həm də
məna baxımından dağınıq olur.

Senior mühəndislik burada bir daha sərhəd hissi ilə fərqlənir. Yaxşı mühəndis
paradiqmaları qarışdırmaqdan qorxmur, amma onları kor-koranə də qarışdırmır. O
bilir ki, sistemin hansı hissəsi behavior-centered model istəyir, hansı hissəsi
saf transformasiya kimi düşünülə bilər, hansı hissəsi isə sadəcə aydın bir axın
kimi qalmalıdır.

### **OOP və FP arasındakı ən faydalı fərq: state-ə münasibət**

Bu iki yanaşmanı müqayisə edərkən ən məhsuldar baxışlardan biri onların state-ə
yanaşmasıdır. OOP state-i obyekt daxilində legitim və təbii hesab edir. Hətta
bir çox halda bu, doğrudan da düzgündür. Çünki bəzi anlayışlar məhz vəziyyət
keçidləri ilə mövcuddur. Məsələn, subscription aktivdən cancelled vəziyyətinə
keçir, payment pending-dən confirmed olur, exam attempt started-dən completed və
ya invalidated statusuna keçir. Bu cür davranışlar üçün encapsulated state çox
təbii modeldir.

FP isə əksinə, state-in mümkün qədər açıq, idarəolunan və dəyişməz formalarda
saxlanmasını üstün tutur. Bu da reasoning-i asanlaşdırır. Xüsusilə concurrent və
distributed mühitlərdə mutable shared state çox ciddi problemlər yarada bilir.
Race condition, synchronization xərci, gözlənilməz yan təsirlər və test
çətinliyi məhz burada artır.

Bu iki yanaşmanın heç biri özlüyündə “daha doğrudur” demək deyil. Sadəcə
sistemin hissələrinə fərqli lens-lərlə baxırlar. Mühəndislik yetkinliyi həmin
lens-ləri düzgün yerlərdə istifadə etməkdir. Əgər hər problemi mutable object
behavior kimi modelləşdirsən, transformasiya yönümlü hissələri ehtiyacdan artıq
ağırlaşdıra bilərsən. Əgər hər şeyi pure function-larla həll etməyə çalışsan,
stateful domain-in təbii formalarını süni şəkildə parçalaya bilərsən.

Burada yenə trade-off anlayışı qayıdır. Paradigms fight adətən nəzəri
mübahisədir. Paradigm fit isə mühəndislik qərarıdır.

### **API-lər, ORM-lər, caching və async flow-lar da paradiqma seçiminə təsir edir**

Bu məsələ sırf kod stili mövzusu deyil. Sistem daxilindəki texniki seçimlər də
hansı düşüncə modelinin uyğun olduğunu dəyişir. Məsələn, ORM ilə işləyən bir
business tətbiqində domain model OOP tərzində qurulanda daha təbii hiss oluna
bilər. Amma data-ya ağır transformasiya və agregasiya tətbiq olunan reporting
pipeline-larında functional yanaşma çox vaxt daha təmiz olur. API orchestration
qatında procedural axın aydınlıq yarada bilər. Cache ilə işləyən hissələrdə isə
immutability və explicit data flow yanaşmaları correctness riskini azaltmağa
kömək edə bilər.

Eyni şəkildə async proqramlaşdırma və thread davranışı da burada təsirsiz deyil.
Shared mutable state olan mühitdə concurrency idarəsi daha çətinləşir.
Functional üslubun bəzi üstünlükləri məhz burada ortaya çıxır. Digər tərəfdən,
bəzi domain prosesləri sırf [[state machine]] kimi modelləşdirildikdə
object-oriented yanaşma status keçidlərini daha aydın ifadə edə bilir.

Yəni paradiqma mövzusu ayrıca fəlsəfi debat kimi yox, sistemin başqa hissələri
ilə birlikdə düşünülməlidir. Əsl senior baxış da budur: alətlər bir-birindən
təcrid olunmuş qərarlar deyil, bir-birinə təsir edən sistem seçimləridir.

### **Güclü mühəndis paradiqma bilmir, paradiqma hiss edir**

Bu hissənin ən vacib nəticəsi bəlkə də budur. Zəif yanaşmada paradiqma məlumat
kimi toplanır. İnsan bilir ki, OOP-də encapsulation var, FP-də immutability var,
procedural üslubda ardıcıl flow var. Amma bu bilik real qərara çevrilmir. Güclü
yanaşmada isə mühəndis problemi görən kimi hansı səviyyədə hansı düşüncə
modelinin daha uyğun olduğunu hiss etməyə başlayır.

Bu hiss intuitiv sehr deyil. Bu, nəzəri təməlin, praktik müşahidənin və düzgün
[[refactoring]] vərdişinin nəticəsidir. İnsan zamanla görür ki, bəzi problemlər
obyekt davranışı kimi daha yaxşı oturur, bəziləri data transformasiyası kimi
daha təmizdir, bəziləri isə sadəcə mərhələli prosesdir və onları süni şəkildə
modelləşdirməyə ehtiyac yoxdur.

Məhz burada kompüter elmləri nəzəriyyəsi yenidən real iş mühitinə bağlanır.
Çünki paradiqmalar sintaksis mövzusu deyil, düşüncə strukturlarıdır. Onları
yalnız dil səviyyəsində yox, problem səviyyəsində anlamaq lazımdır. Bu da
mühəndislik prinsiplərinin mərkəzi mövzularından biridir.

---

_Məqalənin bu hissəsində mühəndislik düşüncəsinin nəzəri təməllərini,
abstraksiya və paradiqmaları incələdik. İkinci hissədə isə bu düşüncənin real
koda və arxitekturaya necə çevrildiyinə – Clean Code, SOLID prinsipləri, dizayn
pattern-ləri və performans optimizasiyası kimi praktik məsələlərə toxunacağıq._

# Mikroservis Mimarisi

## 1. Giriş: Yazılım Mimarilerinin Evrimi
<img width="579" height="360" alt="image" src="https://github.com/user-attachments/assets/68e5a3a1-fa8d-4ccc-b959-abc365e9908a" />

Yazılım mimarisi, bir yazılım sisteminin temel organizasyonunu ve bu organizasyonda yer alan bileşenlerin ilişkilerini tanımlar. Uzun yıllar boyunca **monolitik mimari** yaygın olarak kullanıldı. Bu mimaride, uygulamanın tüm işlevleri tek bir kod tabanında birleşir.

### Monolitik Mimarinin Zorlukları:
<img width="960" height="614" alt="image" src="https://github.com/user-attachments/assets/1d45f303-4ace-494c-a415-a5a009b83d1f" />

- Kod tabanı büyüdükçe bakım zorlaşır.
- Tüm uygulama tek seferde dağıtılır; küçük bir değişiklik için tüm sistemi yeniden dağıtmak gerekir.
- Farklı ekiplerin paralel çalışması zordur.
- Bir modüldeki hata tüm sistemi etkileyebilir.
- Yatay ölçeklendirme kısıtlıdır.
- Yeni teknolojilere veya araçlara geçmek zordur.
- Deploy süreçleri uzundur, geri alma (rollback) karmaşıktır.

## 2. Dağıtık Sistemler, SOA ve Mikroservise Geçiş
<img width="640" height="360" alt="image" src="https://github.com/user-attachments/assets/f3f06808-27e3-4e37-86e7-b2444111e4e5" />

### Dağıtık Sistemler & SOA
- 1990'larda dağıtık sistemler popülerleşti (CORBA, DCOM, EJB vs.).
- 2000'lerde **Service Oriented Architecture (SOA)** ile işlevler servisler halinde ayrıştırılmaya başlandı.
- SOA’da genellikle ağır protokoller (SOAP, WS-*) ve merkezi ESB (Enterprise Service Bus) kullanıldı.

### SOA'nın Sınırlamaları:
- Karmaşık ve maliyetli altyapı.
- Sıkı entegrasyon, bağımsız geliştirme ve dağıtımı zorlaştırdı.
- Veri paylaşımı ve ortak modeller nedeniyle servisler arasında sıkı bağlılık oluştu.
- Esneklik ve çeviklik kısıtlandı.

## 3. Mikroservislerin Doğuşu ve Temel İlkeleri
<img width="1248" height="439" alt="image" src="https://github.com/user-attachments/assets/15bad181-2527-4ec9-b916-fe0cce3bf68f" />

### Ortaya Çıkış (2010’lar başı)
- Büyük ölçekli web şirketlerinde (Amazon, Netflix, eBay) monolitik mimarinin sınırlarına ulaşıldı.
- 2011’de Martin Fowler & James Lewis, “Microservices” terimini ve temel prensiplerini tanımladı.

### Mikroservis Mimarisi Nedir?
<img width="1082" height="830" alt="image" src="https://github.com/user-attachments/assets/d13f119b-ec06-4455-88f7-385ebb8242e0" />

- Uygulamanın, bağımsız dağıtılabilen, küçük, işlevsel servislere bölünmesidir.
- Her servis kendi veritabanına, kod tabanına ve dağıtım döngüsüne sahip olabilir.
- Servisler birbirleriyle genellikle HTTP REST, gRPC veya mesajlaşma (RabbitMQ, Kafka) üzerinden haberleşir.
- Her bir servis, işlevsel olarak iş alanına (domain) göre şekillendirilir (domain-driven design).
- Servisler birbirlerinden bağımsız olarak geliştirilebilir, test edilebilir ve dağıtılabilir.

### Temel İlkeler:
<img width="720" height="540" alt="image" src="https://github.com/user-attachments/assets/a76e0b3f-56f9-4c62-b971-c603970ba77b" />

1. **Bağımsızlık:** Her servis bağımsız geliştirilir, test edilir ve dağıtılır.
2. **Tek Sorumluluk:** Her servis tek bir işlevden sorumludur.
3. **Teknoloji Çeşitliliği:** Farklı servislerde farklı teknolojiler, diller, veritabanları kullanılabilir.
4. **Otonom Takımlar:** Her servis ayrı bir ekip tarafından yönetilebilir.
5. **Otonom Veri:** Servisler birbirinin veritabanına doğrudan erişmez.
6. **Hafif İletişim:** REST, gRPC, mesaj kuyrukları gibi hafif protokoller tercih edilir.
7. **Hata İzolasyonu:** Bir servisteki hata tüm sistemi etkilemez.
8. **Sürekli Teslimat:** Her servis bağımsız olarak sürekli entegre edilir ve dağıtılır (CI/CD).

## 4. Mikroservislerin Yaygınlaşması ve Temel Teknolojiler

<img width="1200" height="406" alt="image" src="https://github.com/user-attachments/assets/a00e8644-b209-4394-a7c9-bfccb8a9271a" />

### Büyük Şirketlerde Mikroservis Dönüşümü:
- **Amazon:** Sipariş yönetim sistemini mikroservislere böldü. Her ekip, kendi servislerinin “you build it, you run it” mantığıyla uçtan uca sorumlusu oldu.
- **Netflix:** Binlerce servisten oluşan dağıtık bir yapı kurdu, kendi servis keşif ve dağıtım araçlarını geliştirdi (Eureka, Ribbon, Hystrix vs.).
- **Uber, Spotify, Google:** Farklı servislerde farklı teknolojiler kullanarak büyük ölçekli dağıtık sistemler kurdu.

### Mikroservis Ekosistemini Büyüten Temel Teknolojiler:
<img width="482" height="601" alt="image" src="https://github.com/user-attachments/assets/d8f748b4-5fdd-4057-85d3-389bdebd003d" />

- **Konteynerler:** Docker ile servislerin paketlenip taşınması ve izole şekilde çalıştırılması kolaylaştı.
- **Orkestrasyon:** Kubernetes, Docker Swarm gibi araçlar ile servislerin ölçeklenmesi, yönetimi ve otomatik onarımı sağlandı.
- **API Gateway:** Tüm servislerin dış dünyaya açıldığı tek bir giriş noktası (Kong, NGINX, Istio).
- **Servis Keşfi:** Servislerin birbirini bulmasını sağlayan sistemler (Consul, Eureka).
- **Merkezi Loglama & İzleme:** ELK, Prometheus, Grafana, Jaeger, Zipkin gibi araçlarla sistemin izlenmesi ve sorunların tespiti kolaylaştı.
- **CI/CD:** Jenkins, GitHub Actions, GitLab CI gibi araçlarla sürekli entegrasyon ve dağıtım akışları kuruldu.
- **Service Mesh:** Servisler arası iletişimin güvenli ve izlenebilir olmasını sağlayan Istio, Linkerd gibi çözümler yaygınlaştı.

## 5. Mikroservisin Avantajları
- **Hızlı Geliştirme ve Dağıtım:** Küçük servisler bağımsız olarak geliştirilip, hızlıca yayına alınabilir.
- **Küçük ve Yönetilebilir Kod Tabanı:** Her ekip sadece kendi servisini bilir ve yönetir.
- **Farklı Programlama Dilleri ve Teknolojiler:** Takımlar uygun gördükleri teknolojiyi özgürce seçebilir.
- **Bağımsız Ölçeklenebilirlik:** Sadece yoğun kullanılan servisler yatayda çoğaltılabilir.
- **Arıza İzolasyonu:** Bir servis çökse bile diğerleri çalışmaya devam edebilir.
- **Yenilik ve Deney:** Yeni teknolojiler, sadece bir serviste test edilip, tüm sistemi riske atmadan uygulanabilir.
- **Sürekli Teslimat:** Her servis bağımsız olarak deploy edilebilir, çeviklik sağlar.
- **Kurumsal Çeviklik:** Organizasyonlar, küçük ve bağımsız ekiplerle daha hızlı hareket edebilirler.

## 6. Mikroservisin Zorlukları ve Dezavantajları
<img width="800" height="527" alt="image" src="https://github.com/user-attachments/assets/b7498d59-2699-4d90-8414-46a92bf311fe" />

- **Dağıtık Sistem Karmaşıklığı:** Ağ üzerinden haberleşme, gecikme, veri tutarlılığı ve ağ hatası gibi yeni sorunlar ortaya çıkar.
- **Veri Tutarlılığı:** Farklı servislerin verileri tutarlı tutması zordur (eventual consistency).
- **Debug ve İzleme:** Bir hata olduğunda, hangi servisten kaynaklandığını bulmak zordur.
- **Otomasyon ve DevOps Gereksinimi:** Çok sayıda servisin otomatik test, dağıtım ve izleme sistemleri gerekir.
- **Ağ Güvenliği:** Servisler arası iletişimde güvenlik açıkları artar; servis-to-servis authentication (mTLS, OAuth) gerektirir.
- **Dağıtım Yönetimi:** Versiyonlama, backward compatibility ve bağımlılık yönetimi karmaşıklaşır.
- **Servis Bağımlılıkları:** Bir servisin güncellenmesi, diğer servisleri de etkileyebilir; doğru API versiyonlama ve backward compatibility önemlidir.
- **Aşırı Servisleşme:** Gereğinden fazla mikroservis oluşturulursa yönetim ve izleme zorlaşır.
- **Network Maliyetleri:** Servisler arası iletişimde ek gecikme ve bant genişliği maliyetleri oluşur.

## 7. Mikroservis Uygulama Desenleri
<img width="768" height="574" alt="image" src="https://github.com/user-attachments/assets/4bc45b8c-69a7-4f18-b9d1-f811bf3f57aa" />

- **API Gateway Pattern:** Mikroservislerin dışa açılan tek noktası.
- **Service Discovery Pattern:** Servislerin ağdaki adreslerini otomatik bulması.
- **Circuit Breaker Pattern:** Hatalı servislerin sistemi etkilememesi için devre kesici mekanizma.
- **Event-driven Architecture:** Servisler arası asenkron mesajlaşma ile loosely-coupled yapı.
- **Database per Service:** Her servisin kendi veri deposu.
- **Saga Pattern:** Dağıtık işlemler için uzun süren transaction yönetimi.
- **Sidecar Pattern:** Servise ek işlevsellik sağlayan yardımcı konteynerler (özellikle service mesh mimarisinde).

## 8. Gerçek Dünya Uygulamaları ve Deneyimler

### Netflix
- 1000+ mikroservis, günde milyarlarca isteğe cevap veriyor.
- Otomatik ölçeklendirme, self-healing ve merkezi izleme araçları ile sürdürülebilirlik sağlandı.
- Kaos mühendisliği (chaos engineering) ile sistemin dayanıklılığı sürekli test ediliyor.

### Amazon
- Her iş birimi kendi mikroservislerini yönetiyor.
- “You build it, you run it” prensibiyle ekipler ürünü uçtan uca sahipleniyor.
- API temelli iletişim ve bağımsız dağıtım akışları sayesinde sürekli inovasyon sağlanıyor.

### Uber
- Çok hızlı büyüme nedeniyle monolitten mikroservise geçişte “service sprawl” (aşırı servisleşme) ve yönetim zorlukları yaşandı.
- Dağıtık izleme (distributed tracing) ve merkezi loglama ile operasyonel zorluklar aşıldı.

### Spotify
- “Squad” adı verilen otonom ekipler, kendi mikroservislerini bağımsızca yönetiyor.
- Her ekip, ürünün belirli bir işlevinden tamamen sorumlu ve kendi geliştirme, test ve dağıtım süreçlerini yönetiyor.

## 9. Mikroservislerin Geleceği
<img width="1200" height="628" alt="image" src="https://github.com/user-attachments/assets/acd19c12-e4df-4cd9-a7d1-de40eb56eba2" />

- **Serverless ve Function as a Service (FaaS):** Mikroservislerin daha küçük birimi olan fonksiyon bazlı mimariler yaygınlaşıyor (AWS Lambda, Azure Functions).
- **Service Mesh:** Istio, Linkerd gibi çözümler, servisler arası ağ yönetimini, güvenliği ve gözlemlenebilirliği kolaylaştırıyor.
- **Yapay Zeka ile Otomasyon:** Otomatik hata tespiti, kapasite planlama vs. gibi alanlarda AI tabanlı araçlar öne çıkıyor.
- **NoOps (Operationless):** Tam otomasyon ile operasyonel iş yükünün minimuma indirildiği yaklaşımlar yaygınlaşıyor.
- **Platform Engineering:** Self-service platformlar sayesinde ekipler altyapı ve dağıtım konularında daha özerk hareket edebiliyor.

## 10. Sonuç

Mikroservis mimarisi, modern yazılım geliştirme dünyasında ölçeklenebilirlik, esneklik ve hızlı inovasyon için önemli bir paradigma değişimidir. Ancak, bu mimarinin getirdiği karmaşıklık ve zorluklar göz ardı edilmemelidir. Doğru araçlar, kültür ve süreçlerle desteklendiğinde, mikroservisler büyük ölçekli projelerde büyük avantajlar sunar. Her organizasyonun ihtiyaçları ve mevcut kaynakları göz önünde bulundurularak mikroservis mimarisine geçiş planlanmalıdır.

---

### Kaynaklar:
- Martin Fowler, James Lewis, “Microservices”
- Sam Newman, “Building Microservices”
- Netflix, Amazon, Uber, Spotify Engineering Blog’ları
- InfoQ, ThoughtWorks Technology Radar
- Cloud Native Computing Foundation (CNCF) dokümantasyonları
- Chris Richardson, "Microservices Patterns"
- Cindy Sridharan, "Distributed Systems Observability"

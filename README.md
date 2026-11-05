# 🌐 BSM 451 – Ağ Programlama Ders Konu Anlatımı ve Vize Rehberi

> **Sakarya Üniversitesi – Bilgisayar Mühendisliği Bölümü**  
> **Ders Sorumlusu:** Dr. Öğr. Üyesi Musa BALTA  
> **Kapsam:** Hafta 1–5 Ders Sunumları (Slayt Görselleri ve Sayfa/Slayt Referanslarıyla) & Katman 2–3 `libpcap` C Uygulama Kodları (`.c`)

---

## 📑 İçindekiler
1. [1. Ders: Hafta 1 – OSI Referans Modeli ve Katmansal Yapı](#1-ders-hafta-1--osi-referans-modeli-ve-katmansal-yapı)
   * [1.4. Hafta 1 Değerlendirme Soruları (20 Soru & Çözümleri)](#14-hafta-1-değerlendirme-soruları-20-soru--çözümleri)
2. [2. Ders: Hafta 2 (Bölüm 1) – PCAP ve Libpcap Kütüphanesi](#2-ders-hafta-2-bölüm-1--pcap-ve-libpcap-kütüphanesi)
3. [3. Ders: Hafta 2 (Bölüm 2) – Katman 2 Protokolleri (Ethernet & ARP) ve `1-arpgonder.c`](#3-ders-hafta-2-bölüm-2--katman-2-protokolleri-ethernet--arp-ve-1-arpgonderc)
   * [3.5. Hafta 2 Değerlendirme Soruları (20 Soru & Çözümleri)](#35-hafta-2-değerlendirme-soruları-20-soru--çözümleri)
4. [4. Ders (Bölüm 1): Hafta 3 – Katman 3: IPv4, Fragmantasyon, Opsiyonlar, Checksum ve IPv6](#4-ders-bölüm-1-hafta-3--katman-3-ipv4-fragmantasyon-opsiyonlar-checksum-ve-ipv6)
5. [5. Ders (Bölüm 2): Hafta 3 – Katman 3: ICMP Protokolü ve 3 C Kodu (`2-icmpgonder.c`, `ping_server.c`, `ping_client.c`)](#5-ders-bölüm-2-hafta-3--katman-3-icmp-protokolü-ve-3-c-kodu)
   * [5.5. Hafta 3 Değerlendirme Soruları (20 Soru & Çözümleri)](#55-hafta-3-değerlendirme-soruları-20-soru--çözümleri)
6. [6. Ders (Bölüm 1): Hafta 4 – Katman 4: TCP Segment Yapısı, 3-Way Handshake, Durum Şeması, Akış ve Hata Kontrolü](#6-ders-bölüm-1-hafta-4--katman-4-tcp-segment-yapısı-3-way-handshake-durum-şeması-akış-ve-hata-kontrolü)
   * [6.6. Hafta 4 Değerlendirme Soruları (20 Soru & Çözümleri)](#66-hafta-4-değerlendirme-soruları-20-soru--çözümleri)
7. [6. Ders (Bölüm 2): Hafta 4 – Katman 4: TCP Tıkanıklık Kontrolü, 4 Zamanlayıcı, RTT/RTO Hesabı ve UDP *(Sıradaki Konu)*](#6-ders-bölüm-2-hafta-4--katman-4-tcp-tıkanıklık-kontrolü-4-zamanlayıcı-rttrto-hesabı-ve-udp)
8. [7. Ders: Hafta 5 – Soket Programlama (C, Java ve Endianness) *(Sıradaki Konu)*](#7-ders-hafta-5--soket-programlama-c-java-ve-endianness)

---

# 1. Ders: Hafta 1 – OSI Referans Modeli ve Katmansal Yapı
**Kaynak Sunum:** `Hafta-1-OSI Referans Modeli ve Katmasal Yap .pdf` *(Toplam 4 PDF Sayfası / 8 Slayt)*

## 1.1. Bilgisayar Ağlarının Sınıflandırma Ağacı (PDF Sayfa 2, Slayt 3)
![Bilgisayar Ağlarının Sınıflandırma Ağacı](assets/slides/h1_s3_siniflandirma.png)

* **1) Coğrafi Yapılar:** `LAN` (Yerel Alan Ağı), `MAN` (Metropol Alan Ağı), `WAN` (Geniş Alan Ağı).
* **2) Standart Yapılar *(Sınavda De Jure / De Facto ayrımına dikkat!)*:**
  * **De Jure (Resmi / Yasal Standartlar):** `CCITT`, `IEEE`, `ISO`.
  * **De Facto (Fiili / Pratikte Kabul Gören Standartlar):** `IBM`, `UNIX`.
* **3) İletişim Tekniği:** `Senkron`, `Asenkron`, `İsenkron` (Sabit zaman aralıklı).
* **4) Topolojiler:** `Doğrusal` (Bus), `Yıldız` (Star), `Ağaç` (Tree), `Karmaşık` (Mesh), `Halka` (Ring).
* **5) İletim Ortamı ve İletim Metodları:**
  * *Ortamlar:* `Fiber Optik`, `Koaksiyel`, `Çift-Burgulu` (Twisted Pair).
  * *Metodlar:* `Geniş Band` (Broadband), `Taşıyıcı Band` (Carrierband), `Temel Band` (Baseband).
* **6) Kontrol Tipleri:** `Merkezi`, `Rastgele`, `Dağıtılmış`.
* **7) Ortam Erişim Kontrol Yöntemleri (MAC):** `DQDB`, `Token` (Jeton), `CSMA/CD`.
* **8) Haberleşme Tipleri:**
  * `Yayınlamalı Haberleşme` (Broadcast)
  * `Anahtarlamalı Haberleşme` (Switched) $\rightarrow$ **Devre Anahtarlamalı**, **Mesaj Anahtarlamalı**, **Paket Anahtarlamalı**.

---

## 1.2. Standart Organizasyonlar Hiyerarşisi (PDF Sayfa 2, Slayt 4)
![Standart Organizasyonlar](assets/slides/h1_s4_standartlar.png)

* **Şemadaki Hiyerarşi (Üstten Alta):**
  * **ISOC** (*Internet Society*) $\rightarrow$ **IAB** (*Internet Architecture Board*)
  * **IAB** iki ana kola ayrılır:
    1. **IETF** (*Internet Engineering Task Force*) $\rightarrow$ **IESG** (*Internet Engineering Steering Group*) $\rightarrow$ *Working Group #1, #2, #3...*
    2. **IRTF** (*Internet Research Task Force*) $\rightarrow$ **IRSG** (*Internet Research Steering Group*) $\rightarrow$ *Research Group #1, #2, #3...*
* **Diğer Kuruluşlar:** `IEEE`, `ISO`, `EIA`, `TIA`, `ITU-T`, `ICANN` (Alan adları ve sayılar), `IANA` (Port ve IP numara tahsisi).

---

## 1.3. OSI Referans Modeli, Kapsülleme ve Cihazlar (PDF Sayfa 3, Slayt 5–6 & PDF Sayfa 4, Slayt 7)
![OSI 7 Katman ve Ara Düğüm](assets/slides/h1_s5_osi_dugumler.png)
![OSI Modeli, TCP/IP ve Kapsülleme](assets/slides/h1_s6_osi_kapsulleme.png)

> [!IMPORTANT]
> **Sınav Detayı (Slayt 5 ve Slayt 6):**
> * **Intermediate Node (Ara Düğüm / Yönlendirici - Router):** Slayt 5'in sağındaki şemada görüldüğü üzere `Transmitting Node` ve `Receiving Node` 7 katmanın tamamını (`L1–L7`) çalıştırırken, aradaki yönlendiriciler (`Intermediate Node`) **yalnızca ilk 3 katmanı (`L1: Physical`, `L2: Data Link`, `L3: Network`)** çalıştırır!
> * **Kapsülleme (Encapsulation) Sırası (Slayt 6 Sağ Sütun):** Üst katmanlarda **`DATA`** (L7–L5) $\rightarrow$ Taşıma katmanında (L4) **`SEGMENT`** $\rightarrow$ Ağ katmanında (L3) **`PACKET or DATAGRAM`** $\rightarrow$ Veri Bağı katmanında (L2) **`FRAME`** $\rightarrow$ Fiziksel katmanda (L1) **`Bit or Data-Stream`**.

| Katman No | OSI Katmanı | Görevi ve Protokol Örnekleri (Slayt 5–7) | Cihaz / Bileşen (Slayt 6) | TCP/IP Modeli | Veri Birimi (PDU) |
| :---: | :--- | :--- | :--- | :--- | :--- |
| **7** | **Application** | Uygulama servisleri (`HTTP, DNS, DHCP, FTP, Telnet, SMTP`) | FTP services | Application | **DATA** |
| **6** | **Presentation**| Veri formatlama, sıkıştırma, şifreleme (`ANSI, HTML, JPEG, SSL/TLS`) | ANSI | Application | **DATA** |
| **5** | **Session** | Oturum kontrolü, diyalog yönetimi (`NetBIOS, RPC, SQL`) | — | Application | **DATA** |
| **4** | **Transport** | Uçtan uca bağlantı, güvenilirlik, akış/hata kontrolü, portlar (`TCP, UDP`) | Ports, Some Firewalls | **Host to Host** | **SEGMENT** |
| **3** | **Network** | Mantıksal adresleme (IP), yönlendirme, parçalama (`IP, ARP, ICMP, IGMP, OSPF`) | **Routers** | **Internetwork** | **PACKET / DATAGRAM** |
| **2** | **Data-Link (`LLC`+`MAC`)** | Fiziksel adresleme (MAC), hata tespiti (`FCS/CRC`), çerçeveleme (`Ethernet, PPP, ATM`) | **Bridges or Switches, NIC** | **Network Access** | **FRAME** |
| **1** | **Physical** | Kablo, sinyal gücü, ikili (binary) iletim (`RS-232, RJ45, 100BASE-TX`) | **Hubs, Network Cards** | **Network Access** | **Bit / Data-Stream** |

![Farklı Standartların Karşılaştırımı](assets/slides/h1_s7_karsilastirma.png)

---
## 1.4. Hafta 1 Değerlendirme Soruları (20 Soru & Çözümleri)

### Soru 1: Standart Yapılar ve Türleri
**Soru:** Bilgisayar ağlarında standartlar "De Jure" (resmi/yasal) ve "De Facto" (fiili/fiilen kabul gören) olarak ikiye ayrılır. Aşağıdaki eşleştirmelerden hangisi tamamen **De Jure** standart kuruluşlarını içerir?  
- A) IBM, UNIX, CCITT  
- B) IEEE, ISO, CCITT  
- C) UNIX, IEEE, ISO  
- D) IBM, IEEE, CCITT  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (PDF Sayfa 2, Slayt 3):** Slayt 3'teki sınıflandırma ağacına göre:
* **De Jure (Resmi/Hukuki):** `CCITT`, `IEEE`, `ISO` kurumlarıdır.
* **De Facto (Fiili/Piyasa Gerçeği):** `IBM` ve `UNIX` gibi endüstriyel kabul gören yapılardır.
</details>

---

### Soru 2: Ara Düğümlerin (Router) Katman Seviyesi
**Soru:** OSI referans modeline göre bir ağdaki kaynak ve hedef bilgisayarlar 7 katmanın tamamını çalıştırırken, aradaki yönlendiriciler (Router / Intermediate Node) en fazla hangi katmana kadar çalışır?  
- A) Sadece Katman 1 (Fiziksel)  
- B) Katman 1 ve Katman 2 (Veri Bağı)  
- C) Katman 1, Katman 2 ve Katman 3 (Ağ)  
- D) Katman 1'den Katman 4'e (Taşıma) kadar  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: C**  
**Açıklama (PDF Sayfa 3, Slayt 5):** Slayt 5'teki OSI şemasında açıkça görüldüğü üzere `Intermediate Node` (yönlendirici), paket yönlendirmesi yaptığı için yalnızca ilk 3 katmanı (**L1: Physical, L2: Data Link, L3: Network**) çalıştırır. Taşıma (L4) ve üst katmanlar uçtan uca (End-to-End) çalışır.
</details>

---

### Soru 3: Katman Veri Birimleri (PDU) Eşleştirmesi
**Soru:** OSI referans modelinde katmanlar arasında veri paketleme sürecinde kullanılan Protokol Veri Birimleri (PDU) adlandırmalarından hangisi **yanlıştır**?  
- A) Katman 4 (Taşıma) $\rightarrow$ Segment  
- B) Katman 3 (Ağ) $\rightarrow$ Packet veya Datagram  
- C) Katman 2 (Veri Bağı) $\rightarrow$ Frame (Çerçeve)  
- D) Katman 1 (Fiziksel) $\rightarrow$ Datagram  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: D**  
**Açıklama (PDF Sayfa 3, Slayt 6):** Katman 1'deki (Fiziksel) veri birimi **Bit** veya **Data-Stream**'dir. Datagram ise Katman 3 (Ağ) veri birimidir.
</details>

---

### Soru 4: Standart Kuruluşları Hiyerarşisi
**Soru:** İnternet standartlarını belirleyen organizasyon şemasına göre en üstte ISOC (Internet Society) yer alır. ISOC'a bağlı olan IAB (Internet Architecture Board) doğrudan hangi iki alt kurula ayrılır?  
- A) IEEE ve ISO  
- B) IETF ve IRTF  
- C) IESG ve IRSG  
- D) ICANN ve IANA  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (PDF Sayfa 2, Slayt 4):** Slayt 4'teki hiyerarşik şemaya göre: `ISOC` $\rightarrow$ `IAB`. IAB ise iki ana kola ayrılır: **IETF** (*Internet Engineering Task Force*) ve **IRTF** (*Internet Research Task Force*). IESG ve IRSG ise bunların yönlendirme gruplarıdır.
</details>

---

### Soru 5: İletim Metotları: Baseband ve Broadband
**Soru:** Sayısal (dijital) sinyallerin herhangi bir modülasyona tabi tutulmadan doğrudan kablo frekans bandının tamamını kullanarak iletildiği yöntem aşağıdakilerden hangisidir?  
- A) Geniş Band (Broadband)  
- B) Taşıyıcı Band (Carrierband)  
- C) Temel Band (Baseband)  
- D) Asenkron Band  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: C**  
**Açıklama (PDF Sayfa 2, Slayt 3):** Temel Band (Baseband), iletim ortamının tüm bant genişliğini tek bir dijital sinyale ayırır (örneğin standart Ethernet). Geniş Band (Broadband) ise frekans bölmeli çoğullama ile birden fazla analog taşıyıcı dalga kullanır.
</details>

---

### Soru 6: Ortam Erişim Yöntemleri (MAC)
**Soru:** Klasik kablolu Ethernet ağlarında (IEEE 802.3) kullanılan ortam erişim kontrol yöntemi aşağıdakilerden hangisidir?  
- A) Token (Jeton)  
- B) DQDB  
- C) CSMA/CD  
- D) TDMA  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: C**  
**Açıklama (PDF Sayfa 2, Slayt 3 & Hafta 2 Slayt 4):** Ethernet, paylaşımlı ortamda çakışmaları sezmek için **CSMA/CD** (*Carrier Sense Multiple Access with Collision Detection*) protokolünü kullanır.
</details>

---

### Soru 7: Sunum (Presentation) Katmanı Görevleri
**Soru:** Aşağıdakilerden hangisi OSI 6. Katman olan Sunum (Presentation) katmanının temel görevlerinden biri **değildir**?  
- A) Karakter kodlama ve veri formatı dönüştürme (ASCII/ANSI çevirisi)  
- B) Veri sıkıştırma (Compression)  
- C) Veri şifreleme ve güvenlik (Encryption/Decryption)  
- D) Süreçler arası diyalog kontrolü ve oturum yönetimi  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: D**  
**Açıklama (PDF Sayfa 3, Slayt 5 & 6):** Süreçler arası diyalog kontrolü ve oturum yönetimi **Katman 5 (Oturum / Session)** katmanının görevidir. Sunum katmanı verinin nasıl temsil edildiğiyle (çeviri, sıkıştırma, şifreleme) ilgilenir.
</details>

---

### Soru 8: Oturum (Session) Katmanı ve Diyalog Yönetimi
**Soru:** İki uygulama arasındaki haberleşmede tek yönlü (simplex), sırayla iki yönlü (half-duplex) veya eşzamanlı iki yönlü (full-duplex) iletişim kurallarını belirleyen ve senkronizasyon kontrol noktaları koyan OSI katmanı hangisidir?  
- A) Katman 4 (Taşıma)  
- B) Katman 5 (Oturum)  
- C) Katman 6 (Sunum)  
- D) Katman 7 (Uygulama)  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (PDF Sayfa 3, Slayt 5):** İletişim diyaloglarının yönetimi, senkronizasyon noktalarının eklenmesi ve oturumun açılıp kapatılması **Oturum (Session)** katmanının sorumluluğundadır.
</details>

---

### Soru 9: TCP/IP Modeli ile OSI Katman Karşılaştırması
**Soru:** TCP/IP modelinde yer alan "Host to Host" (veya Taşıma) katmanı, OSI modelinde hangi katmana birebir karşılık gelir?  
- A) Katman 2 (Veri Bağı)  
- B) Katman 3 (Ağ)  
- C) Katman 4 (Taşıma)  
- D) Katman 5 (Oturum)  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: C**  
**Açıklama (PDF Sayfa 3, Slayt 6):** TCP/IP modelinde Host-to-Host katmanı doğrudan OSI Katman 4 (Transport / Taşıma) katmanına karşılık gelir ve `TCP` ile `UDP` protokollerini barındırır.
</details>

---

### Soru 10: Ağ Cihazları ve Çalışma Katmanları
**Soru:** Hub, Anahtar (Switch) ve Yönlendirici (Router) cihazlarının OSI referans modelinde çalıştığı en üst katmanlar sırasıyla aşağıdakilerden hangisinde doğru verilmiştir?  
- A) L1 (Fiziksel), L2 (Veri Bağı), L3 (Ağ)  
- B) L2 (Veri Bağı), L2 (Veri Bağı), L3 (Ağ)  
- C) L1 (Fiziksel), L3 (Ağ), L4 (Taşıma)  
- D) L1 (Fiziksel), L2 (Veri Bağı), L4 (Taşıma)  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: A**  
**Açıklama (PDF Sayfa 3, Slayt 6):**
* **Hub / Repeater:** Yalnızca elektrik sinyalini çoğaltır $\rightarrow$ **L1 (Fiziksel)**
* **Switch / Bridge:** MAC adreslerini okur ve süzer $\rightarrow$ **L2 (Veri Bağı)**
* **Router:** IP adreslerini okur ve yönlendirir $\rightarrow$ **L3 (Ağ)**
</details>

---

### Soru 11: Anahtarlama Türleri
**Soru:** İletişim başlamadan önce kaynak ile hedef arasında fiziksel ve kesintisiz bir yol kuran, iletim süresince bant genişliğini bu yola rezerve eden anahtarlama türü hangisidir?  
- A) Paket Anahtarlamalı (Packet Switched)  
- B) Mesaj Anahtarlamalı (Message Switched)  
- C) Devre Anahtarlamalı (Circuit Switched)  
- D) Hücre Anahtarlamalı (Cell Switched)  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: C**  
**Açıklama (PDF Sayfa 2, Slayt 3):** Geleneksel telefon şebekelerinde kullanılan **Devre Anahtarlamalı (Circuit Switched)** iletimde bağlantı öncesinde hat rezerve edilir. İnternet ise **Paket Anahtarlamalı** yapıdadır.
</details>

---

### Soru 12: İletişim Teknikleri: İsenkron İletişim
**Soru:** Slayt 3'te listelenen "İletişim Teknikleri" sınıflandırmasında yer alan **İsenkron (Isochronous)** haberleşmenin en belirgin özelliği nedir?  
- A) Verilerin rastgele zamanlarda gönderilmesi  
- B) Veri baytlarının kesin ve sabit zaman aralıklarıyla, sıfıra yakın gecikme dalgalanmasıyla iletilmesi  
- C) Her karakterin başına start, sonuna stop biti konması  
- D) Veri aktarımı sırasında alıcıdan onay beklenmesi  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (PDF Sayfa 2, Slayt 3):** İsenkron iletişim, gecikmeye duyarlı gerçek zamanlı ses ve video akışlarında verilerin sabit zaman aralıklarıyla ve eşzamanlı olarak iletilmesini ifade eder.
</details>

---

### Soru 13: IP ve Port Numaraları Tahsis Kuruluşu
**Soru:** İnternette kullanılan port numaralarının (örneğin port 80 HTTP, port 53 DNS) ve IP adresi bloklarının küresel tahsisinden sorumlu organizasyon hangisidir?  
- A) IEEE  
- B) ISO  
- C) IANA  
- D) ITU-T  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: C**  
**Açıklama (PDF Sayfa 2, Slayt 4):** **IANA** (*Internet Assigned Numbers Authority*), IP adresleri ve port numaralarının tescil ve dağıtımını denetleyen yetkili kurumdur.
</details>

---

### Soru 14: Kapsülleme (Encapsulation) Sırası
**Soru:** Gönderici bir bilgisayarda uygulama katmanında üretilen bir verinin kabloya çıkana kadar katmanlardan geçiş sırası (Kapsülleme) aşağıdakilerden hangisidir?  
- A) Uygulama $\rightarrow$ Veri Bağı $\rightarrow$ Ağ $\rightarrow$ Taşıma $\rightarrow$ Fiziksel  
- B) Uygulama $\rightarrow$ Taşıma $\rightarrow$ Ağ $\rightarrow$ Veri Bağı $\rightarrow$ Fiziksel  
- C) Fiziksel $\rightarrow$ Veri Bağı $\rightarrow$ Ağ $\rightarrow$ Taşıma $\rightarrow$ Uygulama  
- D) Ağ $\rightarrow$ Taşıma $\rightarrow$ Uygulama $\rightarrow$ Veri Bağı $\rightarrow$ Fiziksel  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (PDF Sayfa 3, Slayt 6):** Gönderici tarafta veri üstten alta doğru akar: **Uygulama (L7-L5) $\rightarrow$ Taşıma (L4) $\rightarrow$ Ağ (L3) $\rightarrow$ Veri Bağı (L2) $\rightarrow$ Fiziksel (L1)**. Alıcıda ise tam tersi sırada (Ters Kapsülleme / Decapsulation) yukarı çıkar.
</details>

---

### Soru 15: Veri Bağı Katmanı Alt Katmanları
**Soru:** IEEE 802 standartlarına göre OSI 2. Katman olan Veri Bağı (Data Link) katmanı hangi iki alt katmana ayrılmıştır?  
- A) IP ve ICMP  
- B) TCP ve UDP  
- C) LLC (Logical Link Control) ve MAC (Media Access Control)  
- D) CSMA ve CD  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: C**  
**Açıklama (PDF Sayfa 3, Slayt 6 & Sayfa 4 Slayt 7):** Veri bağı katmanı:
1. **LLC (802.2):** Üst katman protokollerini ayırt etme ve akış denetimi sağlar.
2. **MAC (802.3/802.11):** Donanım adresleme ve ortama erişim kontrolünü sağlar.
</details>

---

### Soru 16: Ağ Topolojileri ve Tek Nokta Arızası
**Soru:** Merkezi bir düğümün (örneğin bir Switch) arızalanması durumunda tüm ağın iletişiminin kesildiği ancak kablo kopmalarının sadece ilgili bilgisayarı etkilediği topoloji hangisidir?  
- A) Doğrusal (Bus)  
- B) Yıldız (Star)  
- C) Halka (Ring)  
- D) Karmaşık (Mesh)  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (PDF Sayfa 2, Slayt 3):** Yıldız (Star) topolojisinde tüm istasyonlar merkezi cihaza bağlıdır. Merkezi cihaz bozulursa tüm ağ çöker; bir uç kablosu koparsa sadece o istasyon devre dışı kalır.
</details>

---

### Soru 17: Fiziksel İletim Ortamları Karşılaştırması
**Soru:** Elektromanyetik parazitlerden (EMI) hiç etkilenmeyen, en yüksek bant genişliğini sunan ve ışık sinyaliyle iletim yapan fiziksel kablo türü hangisidir?  
- A) Çift-Burgulu Kablo (UTP/STP)  
- B) Koaksiyel Kablo (Coaxial)  
- C) Fiber Optik Kablo  
- D) RS-232 Seri Kablo  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: C**  
**Açıklama (PDF Sayfa 2, Slayt 3):** Fiber optik kablolar elektrik yerine ışık darbeleri ilettiği için elektriksel gürültüden (EMI) etkilenmez ve çok yüksek mesafelerde kayıpsız çalışır.
</details>

---

### Soru 18: Coğrafi Ağ Kapsamları
**Soru:** Bir üniversite kampüsü veya şehir ölçeğindeki binalar arası ağı ifade eden coğrafi sınıflandırma kısaltması nedir?  
- A) LAN (Local Area Network)  
- B) MAN (Metropolitan Area Network)  
- C) WAN (Wide Area Network)  
- D) PAN (Personal Area Network)  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (PDF Sayfa 2, Slayt 3):** Bir oda veya bina içi **LAN**, şehir veya büyük kampüs ölçeği **MAN**, ülkeler ve kıtalar arası ağlar ise **WAN** olarak tanımlanır.
</details>

---

### Soru 19: Kontrol Tipleri: Merkezi, Dağıtılmış ve Rastgele
**Soru:** Slayt 3'teki sınıflandırmaya göre bir ağda iletim haklarının merkezi bir yönetici düğüm olmadan, her düğümün rastgele rekabet ederek hatta veri gönderdiği kontrol tipi hangisidir?  
- A) Merkezi (Centralized) Kontrol  
- B) Rastgele (Random / Contention-based) Kontrol  
- C) Dağıtılmış (Distributed) Kontrol  
- D) Hiyerarşik Kontrol  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (PDF Sayfa 2, Slayt 3):** Ethernet'te CSMA/CD mantığı rastgele (random) erişim kontrolü sınıfındadır; düğümler hattı dinleyip rastgele yarışarak gönderir.
</details>

---

### Soru 20: Paket Anahtarlamanın Devre Anahtarlamaya Üstünlüğü
**Soru:** İnternetin temelini oluşturan Paket Anahtarlamalı (Packet Switched) ağların Devre Anahtarlamalı ağlara göre en büyük avantajı nedir?  
- A) İletişim boyunca hattın sadece iki kullanıcıya tahsis edilmesi  
- B) Ağ hatlarının ve bant genişliğinin dinamik paylaşılarak çok daha verimli kullanılması  
- C) Gecikmenin her zaman sıfır olması  
- D) Hiçbir paketin kaybolmaması  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (PDF Sayfa 2, Slayt 3):** Paket anahtarlamada hatlar rezerve edilmez; paketler paylaşımlı hatlar üzerinden dinamik olarak iletilir, böylece hat boş kalmaz ve bant genişliği maksimum verimle kullanılır.
</details>

---

# 2. Ders: Hafta 2 (Bölüm 1) – PCAP ve Libpcap Kütüphanesi
**Kaynak Sunum:** `Hafta-2 Pcap.pdf` *(Toplam 9 PDF Sayfası / 17 Slayt)*

## 2.1. PCAP Kavramı ve Paket Yakalama Yöntemleri (PDF Sayfa 2, Slayt 3–4)
* **Slayt 3 (`PCAP == Packet Capture`):** Ağ aktivitelerinin **Katman 2'den Katman 7'ye kadar** tüm kaydıdır. En yaygın açık kaynak C kütüphanesi **`libpcap`**'tir (*nix ve Windows uyumlu; Windows karşılığı **WinPcap**).
* **Kullanım Alanları (Slayt 3):** Ağ trafiğini dinlemek, bant genişliği kontrolü, pasif DNS çözümlemesi, saldırı girişimlerini görüntüleme, araştırma testleri.
* **Slayt 4 (PCAP Dosyalarını Yakalamak):** Ağdan paket yakalamanın 3 topolojik yolu:
  1. **Switch üzerinde Monitoring Ports (Port Mirroring / SPAN)**
  2. **Tap (Network TAP):** Kablo üzerine fiziksel olarak takılan pasif kopyalayıcı
  3. **Inline Device:** Trafiğin doğrudan içinden geçtiği ara cihaz

![PCAP Dosyalarını Yakalamak](assets/slides/h2p_s4_yakalama.png)

---

## 2.2. Ham PCAP Depolama, Dosya Formatı ve Overhead Hesapları (PDF Sayfa 3–4, Slayt 5–7)
![Ham PCAP Depolama](assets/slides/h2p_s5_depolama.png)
![libpcap Format](assets/slides/h2p_s6_format.png)
![libpcap Overhead Tablosu](assets/slides/h2p_s7_overhead.png)

> [!TIP]
> **Sayısal Sınav Sorusu Rehberi (Slayt 5, 6 ve 7 Hesaplamaları):**
> 1. **1 Gbps Hattın 1 Günlük (24 Saat) Toplam Ham Veri Boyutu (Slayt 5):**
>    $$1\text{ Gbps} \times 3600\text{ sn} \times 24\text{ saat} = 86,400\text{ gigabits} \xrightarrow{\div 8} 10,800\text{ gigabytes (GB/gün)}$$
> 2. **Saniyedeki Paket Sayısı (`pps` - Packets Per Second) Hesabı (Slayt 5):**
>    * Ortalama paket boyutu **64 byte** ise bit cinsinden boyutu: $64\text{ bytes} \times 8\text{ bits} = 512\text{ bits}$.
>    $$\text{pps} = \frac{1\text{ Gbps}}{512\text{ bits}} = \frac{10^9\text{ bits/s}}{512\text{ bits}} = 1,953,125\text{ pps}$$
> 3. **libpcap Dosya Formatı ve Başlık Ek Yükü (Overhead) Hesabı (Slayt 6 & 7):**
>    * Slayt 6'da görüldüğü gibi `.pcap` dosyasının en başında **1 adet `File Header` (`24 bytes`)**, ardından yakalanan **her paket için `Packet Header` (Slaytta `4 bytes`)** + `Packet Data (x bytes)` yer alır.
>    * Saniyedeki başlık ek yükü: $N\text{ pps} \times H_{\text{PCAP}} = N \cdot H\text{ Bps}$.
>    * *Slayt 7 Doğrulaması (64 Byte için):* $1,953,125\text{ pps} \times 4\text{ byte} = 7,812,500\text{ Byte/s} \div 1024^2 \approx \mathbf{7.45\text{ MB/s}}$ (Günde $628.64\text{ GB}$). Paket boyutu büyüdükçe (1500B, 9000B) saniyedeki paket sayısı (`pps`) düştüğü için overhead de `0.32 MB/s` ve `0.05 MB/s` seviyesine iner.

---

## 2.3. Ağ Dinleme Araçları (Sniffer) ve Wireshark Mimarisi (PDF Sayfa 4–7, Slayt 8–13)
* **Slayt 8–9 (Sniffer):** Ağ trafiğini **pasif izleme (sezme)** veya **aktif (atak yapma)** amacıyla kullanılan araçlardır. Saldırganlar şifresiz protokollerden (`FTP, POP3, IMAP, SMTP, rlogin, HTTP, VoIP`) pasif veri toplamak için kullanır.
* **Slayt 10 (Wireshark Hakkında Kesin Bilinmesi Gerekenler):**
  * **Gerald Combs** tarafından **1998** yılında **Ethereal** adıyla başlatılmış, **Haziran 2006**'da **Wireshark** adını almıştır.
  * 750'nin üzerinde protokol destekler ve kapsüllemeli görünüm sunar.
  * **Çok Kritik 2 Sınav Maddesi:**
    1. *"Paket sniffer uygulamasıdır, dolayısıyla **bir ağın haritasını çıkartmak için kullanılamaz**."*
    2. *"**Pasif bir izleme aracıdır, dolayısıyla ağ verisi üretmez**."*

![Wireshark ve WinPcap/libpcap Mimarisi](assets/slides/h2p_s11_mimari.png)
![Sniffer ve Topolojideki Yeri](assets/slides/h2p_s12_topoloji.png)

---

## 2.4. Libpcap C Fonksiyonları ve Syntax Yapısı (PDF Sayfa 7–8, Slayt 14–16)
![Libpcap Cihaz Koklaması](assets/slides/h2p_s15_openlive.png)
![Libpcap Paket Filtreleme](assets/slides/h2p_s16_filtre.png)

| Libpcap Fonksiyonu | Slayt Yeri | C Kodlarındaki Satır Yeri | Parametreleri, Dönüş Değeri ve Görevi |
| :--- | :--- | :--- | :--- |
| `pcap_lookupdev(errbuf)` | Slayt 14 (Sayfa 7) | [`1-arpgonder.c` Satır 14](./0-Katman2-3%20Kodlar/1-arpgonder.c#L14)<br>[`ping_server.c` Satır 37](./0-Katman2-3%20Kodlar/Ping%20Uygulaması/ping_server.c#L37) | Sistemdeki varsayılan aktif ağ kartı adını döndürür. Bulamazsa `NULL` döner ve hatayı `errbuf` (`PCAP_ERRBUF_SIZE`) içine yazar. |
| `pcap_lookupnet(dev, &net, &mask, errbuf)` | Slayt 16 (Sayfa 8) | [`ping_client.c` Satır 59](./0-Katman2-3%20Kodlar/Ping%20Uygulaması/ping_client.c#L59)<br>[`ping_server.c` Satır 47](./0-Katman2-3%20Kodlar/Ping%20Uygulaması/ping_server.c#L47) | Cihazın IP ağ adresini (`net`) ve alt ağ maskesini (`mask`) `bpf_u_int32` tipinde alır. Başarısızsa `-1` döner. |
| `pcap_open_live(dev, snaplen, promisc, to_ms, errbuf)` | Slayt 15 (Sayfa 8) | [`1-arpgonder.c` Satır 22](./0-Katman2-3%20Kodlar/1-arpgonder.c#L22)<br>[`ping_server.c` Satır 54](./0-Katman2-3%20Kodlar/Ping%20Uygulaması/ping_server.c#L54) | Cihazı yakalama/gönderme için açar, `pcap_t*` döner (Hata: `NULL`). `snaplen`: max byte (`BUFSIZ` veya `100`), `promisc`: `1` ise promiscuous mod (tüm paketleri yakala), `to_ms`: okuma zaman aşımı (`1000` ms). |
| `pcap_compile(handle, &fp, filter_exp, 0, net)` | Slayt 16 (Sayfa 8) | [`ping_client.c` Satır 80](./0-Katman2-3%20Kodlar/Ping%20Uygulaması/ping_client.c#L80)<br>[`ping_server.c` Satır 67](./0-Katman2-3%20Kodlar/Ping%20Uygulaması/ping_server.c#L67) | Filtre stringini (Slayt 16'da `"port 23"`, ping kodlarında `"icmp && dst <IP>"`) derleyip `struct bpf_program fp` yapısına yazar (Hata: `-1`). |
| `pcap_setfilter(handle, &fp)` | Slayt 16 (Sayfa 8) | [`ping_client.c` Satır 85](./0-Katman2-3%20Kodlar/Ping%20Uygulaması/ping_client.c#L85)<br>[`ping_server.c` Satır 72](./0-Katman2-3%20Kodlar/Ping%20Uygulaması/ping_server.c#L72) | Derlenmiş olan `fp` filtresini açık oturuma uygular (Hata: `-1`). |

---

# 3. Ders: Hafta 2 (Bölüm 2) – Katman 2 Protokolleri (Ethernet & ARP) ve `1-arpgonder.c`
**Kaynak Sunum ve Kod:** `Hafta-2 Katman 2 Protokolleri.pdf` *(8 PDF Sayfası / 15 Slayt)* & [`1-arpgonder.c`](./0-Katman2-3%20Kodlar/1-arpgonder.c) *(Satır 1–108)*

## 3.1. Ethernet Protokolü (IEEE 802.3) ve CSMA/CD Backoff Algoritması (PDF Sayfa 2–3, Slayt 3–5)
* **Slayt 3 (Ethernet):** En yaygın LAN veri bağı protokolü **IEEE 802.3 Ethernet**'tir (1960'lardaki radyo tabanlı **Alohanet**'in uzantısıdır). Tercih sebepleri: Kurulum kolaylığı, güvenilirlik, ölçeklenebilirlik, çoklu kullanım uyumu.
* **Slayt 4 (CSMA/CD):**
  * **Carrier Sense (Taşıyıcı Sezme):** Kabloda aktarım olup olmadığını kontrol eder.
  * **Multiple Access (Çoklu Erişim):** İletim hattındaki tüm düğümlerin aynı hakka sahip olduğunu belirtir.
  * **Collision Detection (Çarpışmayı Sezme):** İki düğümün aynı anda veri göndermesiyle oluşan çarpışmayı algılar.
* **Slayt 5 (Ethernet'te Veri Gönderme / Backoff Akış Şeması):**
  1. `Start` $\rightarrow$ `Set k to zero` (Deneme sayacı $k = 0$ yapılır).
  2. `Sense carrier` (Hattı dinle — *1-persistent strategy*: hat meşgulse boşalana kadar sürekli dinle).
  3. Hat boşsa (`Busy? No`) $\rightarrow$ `Wait IFG time` (*Interframe Gap* süresi kadar bekle) $\rightarrow$ `Send the frame` (Çerçeveyi gönder).
  4. `Collision?` (Çarpışma oldu mu?): Hayır ise `Success`. Evet ise `Send jam signal` (diğer düğümleri uyarmak için bozucu sinyal gönder) $\rightarrow$ `Increment k` ($k = k + 1$).
  5. Deneme sayısı kontrolü (Slayttaki şemada `k < 10`): Limit aşılmadıysa `Wait backoff time` kadar rastgele bekle ve başa dön; limit aşıldıysa `Abort` (iptal et).

![Ethernet'te Veri Gönderme ve Backoff Şeması](assets/slides/h2k_s5_backoff.png)

---

## 3.2. Ethernet II Başlık Yapısı (14 Byte) ve İletişim Şekilleri (PDF Sayfa 3–4, Slayt 6–7)
![Ethernet II Başlık Yapısı](assets/slides/h2k_s6_eth_header.png)

* **Slayt 6 (Ethernet II Başlığı = `14 Byte`):**
  * `Destination Address (Hedef MAC)`: **6 Byte** (`packet[0..5]`)
  * `Source Address (Kaynak MAC)`: **6 Byte** (`packet[6..11]`)
  * `Packet Type (Üst katman protokol tipi)`: **2 Byte** (`packet[12..13]` $\rightarrow$ ARP için `0x0806`, IPv4 için `0x0800`)
  * **Toplam Ethernet Başlığı:** $6 + 6 + 2 = \mathbf{14\text{ Byte}}$! *(Baştaki 8 Byte `Preamble` ve sondaki 4 Byte `CRC` ağ kartı donanımı tarafından kabloda eklenir; yazılımdaki 14 byte başlığa dahil değildir).*
  * `Data Bölümü (Payload)`: **46 – 1500 Byte** arasındadır.
* **Slayt 7 (Ethernet İletişim Şekilleri):**
  1. **Unicast:** Tek bir MAC adresine (`00-07-E9-42-AC-28`).
  2. **Multicast:** Bir gruba; hedef MAC **`01-00-5E`** ile başlar (`01-00-5E-00-00-01`).
  3. **Broadcast:** Ağdaki tüm cihazlara; hedef MAC **`FF-FF-FF-FF-FF-FF`**.

![Ethernet İletişim Şekilleri](assets/slides/h2k_s7_unicast_multicast.png)

---

## 3.3. ARP (Address Resolution Protocol) Yapısı ve Senaryoları (PDF Sayfa 4–7, Slayt 8–14)
* **Slayt 8–10 (ARP Görevi):** Paketin teslimi için **Mantıksal (IP)** ve **Fiziksel (MAC)** olmak üzere iki düzey adresleme gerekir. ARP, IP protokolünden mantıksal (IP) adresi alır, fiziksel (MAC) adresle eşler ve veri bağı katmanına iletir.
* **Slayt 9 (ARP İşleyişi):** **ARP Request** tüm yerel ağa yayınlanır (**Broadcast**: Ethernet hedef MAC `FF:FF:FF:FF:FF:FF`), **ARP Reply** ise sadece soran düğüme gönderilir (**Unicast**).

![ARP OSI Karşılığı ve Kapsülleme](assets/slides/h2k_s11_arp_osi_kapsulleme.png)
![ARP 28 Byte Paket Yapısı](assets/slides/h2k_s12_arp_paket.png)

> [!IMPORTANT]
> **Kapsülleme Mantığı: "14 Byte Ethernet + 28 Byte ARP = 42 Byte" Nereden Gelir?**
> * **Slayt 11 ve Slayt 12:** Şablonun genel adı **ARP Paketi**dir ve boyutu **28 Byte**'tır (`2B Hardware Type + 2B Protocol Type + 1B HW Len + 1B Proto Len + 2B Operation + 6B Sender MAC + 4B Sender IP + 6B Target MAC + 4B Target IP = 28 Byte`).
> * Bu 28 byte'lık ARP şablonunun `Operation` (`packet[20..21]`) alanına `1` (`0x0001`) yazılırsa adı **ARP Request Paketi**, `2` (`0x0002`) yazılırsa adı **ARP Reply Paketi** olur.
> * Slayt 11'de pembe oklarla gösterildiği gibi, bu **28 byte'lık ARP (Request veya Reply) paketi** doğrudan Ethernet çerçevesinin **`Data`** kısmına (`packet[14..41]`) yerleştirilir! *(ARP paketinde IP başlığı yoktur).*
> * Başına **14 Byte Ethernet Başlığı** (`packet[0..13]`) eklendiğinde kabloya gönderilen toplam çerçeve **`14 + 28 = 42 Byte`** (`u_char packet[42]`) olur.

![ARP 4 Kullanım Durumu](assets/slides/h2k_s13_arp_4durum.png)

* **Slayt 13 (ARP 4 Kullanım Durumu — Sınav Senaryosu!):**
  * **Case 1 (Host $\rightarrow$ Aynı ağdaki Host):** ARP `Target IP` = IP datagramındaki `Destination IP`.
  * **Case 2 (Host $\rightarrow$ Başka ağdaki Host):** Paket önce yerel ağ geçidine (Router) gitmelidir; bu yüzden ARP `Target IP` = **Router'ın IP adresi** olur!
  * **Case 3 (Router $\rightarrow$ Başka ağdaki Router):** ARP `Target IP` = **Bir sonraki Router'ın IP adresi**.
  * **Case 4 (Router $\rightarrow$ Aynı ağdaki Hedef Host):** ARP `Target IP` = IP datagramındaki `Destination IP`.
* **Slayt 14 (ARP Cache Table Durum Harfleri):** `R` = *Resolved* (Çözümlenmiş, MAC biliniyor), `P` = *Pending* (Beklemede, istek atıldı), `F` = *Free* (Boş satır).

![ARP Örnek ve 28 Byte Hex Yapısı](assets/slides/h2k_s14_arp_ornek_hex.png)

---

## 3.4. Kod Analizi: [`1-arpgonder.c`](./0-Katman2-3%20Kodlar/1-arpgonder.c) (Satır 1–108)

| Dizi İndeksi | Boyut | Katman ve Alan Adı | Kodda Atanan Değer | `1-arpgonder.c` Satır No ve Açıklama |
| :--- | :---: | :--- | :--- | :--- |
| `packet[0..5]` | 6 Byte | Ethernet: Destination MAC | `0xff, 0xff, 0xff, 0xff, 0xff, 0xff` | **[Satır 28–34](./0-Katman2-3%20Kodlar/1-arpgonder.c#L28-L34):** Broadcast MAC adresi (Tüm LAN'a gider). |
| `packet[6..11]` | 6 Byte | Ethernet: Source MAC | `0x54, 0x42, 0x49, 0x02, 0x31, 0x8c` | **[Satır 38–44](./0-Katman2-3%20Kodlar/1-arpgonder.c#L38-L44):** Gönderen cihazın MAC adresi. |
| `packet[12..13]` | 2 Byte | Ethernet: Type (EtherType) | `0x08, 0x06` (`0x0806`) | **[Satır 46–48](./0-Katman2-3%20Kodlar/1-arpgonder.c#L46-L48):** Ethernet Data kısmında **ARP** olduğunu belirtir. |
| `packet[14..15]` | 2 Byte | ARP: Hardware Type | `0x00, 0x01` | **[Satır 53–55](./0-Katman2-3%20Kodlar/1-arpgonder.c#L53-L55):** Donanım tipi `1` = Ethernet. *(Satır 53 yorumundaki `=Request` dizgi hatasıdır)*. |
| `packet[16..17]` | 2 Byte | ARP: Protocol Type | `0x08, 0x00` (`0x0800`) | **[Satır 57–59](./0-Katman2-3%20Kodlar/1-arpgonder.c#L57-L59):** Çözümlenen protokol tipi = IPv4. |
| `packet[18]` | 1 Byte | ARP: Hardware Size | `0x06` | **[Satır 61–62](./0-Katman2-3%20Kodlar/1-arpgonder.c#L61-L62):** MAC adres uzunluğu = 6 byte. |
| `packet[19]` | 1 Byte | ARP: Protocol Size | `0x04` | **[Satır 64–65](./0-Katman2-3%20Kodlar/1-arpgonder.c#L64-L65):** IPv4 adres uzunluğu = 4 byte. |
| `packet[20..21]` | 2 Byte | ARP: Opcode (Operation) | `0x00, 0x01` | **[Satır 67–69](./0-Katman2-3%20Kodlar/1-arpgonder.c#L67-L69):** `1` = **ARP Request** (`2` olsaydı ARP Reply olurdu). |
| `packet[22..27]` | 6 Byte | ARP: Sender MAC | `0x54, 0x42, 0x49, 0x02, 0x31, 0x8c` | **[Satır 71–77](./0-Katman2-3%20Kodlar/1-arpgonder.c#L71-L77):** Gönderen MAC (`packet[6..11]` ile aynı). |
| `packet[28..31]` | 4 Byte | ARP: Sender IP | `0x0a, 0x09, 0x1b, 0xe1` | **[Satır 79–83](./0-Katman2-3%20Kodlar/1-arpgonder.c#L79-L83):** Gönderen IP: `10.9.27.225`. |
| `packet[32..37]` | 6 Byte | ARP: Target MAC | `0x00, 0x00, 0x00, 0x00, 0x00, 0x00` | **[Satır 85–91](./0-Katman2-3%20Kodlar/1-arpgonder.c#L85-L91):** Hedef MAC henüz bilinmediği için `0` doldurulur (Slayt 12). |
| `packet[38..41]` | 4 Byte | ARP: Target IP | `0x0a, 0x09, 0x1b, 0x64` | **[Satır 93–97](./0-Katman2-3%20Kodlar/1-arpgonder.c#L93-L97):** MAC adresi sorulan hedef IP: `10.9.27.100`. |

---
## 3.5. Hafta 2 Değerlendirme Soruları (20 Soru & Çözümleri)

### Soru 1: PCAP Kapsamı ve Yakalama Seviyesi
**Soru:** libpcap / WinPcap mimarisine göre ağ kartından paket yakalama işlemi (PCAP), OSI modelinin hangi katman aralığındaki tüm verileri kaydeder?  
- A) Yalnızca Katman 7 (Uygulama)  
- B) Katman 3 ve Katman 4  
- C) Katman 2'den Katman 7'ye kadar tüm katmanlar  
- D) Yalnızca Katman 1 (Fiziksel bitler)  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: C**  
**Açıklama (Hafta 2 Pcap PDF Sayfa 2, Slayt 3):** PCAP, Ethernet çerçevesinden (Katman 2) başlayarak IP (Katman 3), TCP/UDP (Katman 4) ve Uygulama (Katman 7) dahil tüm PDU içeriğini yakalar.
</details>

---

### Soru 2: Ağdan Paket Yakalama Topolojileri
**Soru:** Ağ trafiğini izlemek amacıyla bir ağ kablosunun arasına fiziksel olarak takılan ve iletilen sinyallerin bir kopyasını donanımsal olarak izleme portuna aktaran cihaz nedir?  
- A) Switch Monitoring Port (SPAN)  
- B) Network TAP  
- C) Inline Proxy  
- D) Loopback Adaptör  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (Hafta 2 Pcap PDF Sayfa 2, Slayt 4):** Slayt 4'e göre paket yakalamanın 3 yöntemi vardır: 1) Switch SPAN portu, 2) Network TAP (pasif donanımsal kopyalayıcı), 3) Inline cihaz.
</details>

---

### Soru 3: 1 Gbps Hat Ham Veri Depolama Hesabı
**Soru:** 1 Gbps (Gigabit per second) hızındaki bir omurga hattından geçen tüm ham veri 24 saat boyunca PCAP formatında diske kaydedilirse toplam kaç Gigabayt (GB) disk alanına ihtiyaç duyulur?  
- A) 1,080 GB  
- B) 8,640 GB  
- C) 10,800 GB  
- D) 86,400 GB  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: C**  
**Açıklama (Hafta 2 Pcap PDF Sayfa 3, Slayt 5):**
$$1\text{ Gbps} \times 3600\text{ saniye} \times 24\text{ saat} = 86,400\text{ gigabit}$$
Gigabayt'a dönüştürmek için 8'e böleriz:
$$\frac{86,400}{8} = \mathbf{10,800\text{ Gigabyte (GB)}}$$
</details>

---

### Soru 4: Saniyedeki Paket Sayısı (pps) Hesabı
**Soru:** 1 Gbps hızındaki bir hatta ortalama paket büyüklüğü **64 bayt** olduğuna göre hatta saniyede teorik olarak kaç paket (pps - packets per second) iletilir?  
- A) 1,953,125 pps  
- B) 15,625,000 pps  
- C) 81,274 pps  
- D) 512,000 pps  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: A**  
**Açıklama (Hafta 2 Pcap PDF Sayfa 3, Slayt 5):**
Bir paketin bit cinsinden boyutu: $64\text{ bayt} \times 8\text{ bit} = 512\text{ bit}$.
$$\text{pps} = \frac{1\text{ Gbps}}{512\text{ bit}} = \frac{10^9\text{ bit/sn}}{512\text{ bit}} = \mathbf{1,953,125\text{ pps}}$$
</details>

---

### Soru 5: libpcap Başlık Ek Yükü (Overhead) Hesabı
**Soru:** Standart bir libpcap dosyasında dosyanın en başında kaç baytlık global `File Header`, yakalanan her paketin başında ise kaç baytlık `Packet Header` bulunur?  
- A) 14 Byte File Header, 20 Byte Packet Header  
- B) 24 Byte File Header, 4 Byte Packet Header (Slayt 6-7 tablosu)  
- C) 20 Byte File Header, 8 Byte Packet Header  
- D) 42 Byte File Header, 14 Byte Packet Header  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (Hafta 2 Pcap PDF Sayfa 3-4, Slayt 6 & 7):** Slayt 6 şemasına göre libpcap dosya yapısı başında **24 Bayt File Header**, ardından her paket için **4 Bayt Packet Header** ve `Packet Data` gelir. Slayt 7 tablosunda 64B için $1,953,125 \times 4\text{ bayt} \approx 7.45\text{ MB/sn}$ ek yük bu sayede hesaplanır.
</details>

---

### Soru 6: Wireshark Hakkındaki Kesin Sınav Maddeleri
**Soru:** Slayt 10'da Wireshark için vurgulanan ve sınavda soru olarak gelebilecek aşağıdaki ifadelerden hangisi **doğrudur**?  
- A) Wireshark aktif bir tarayıcıdır, ağdaki cihazlara ping atarak harita çıkarır.  
- B) Wireshark pasif bir izleme aracıdır; ağ verisi üretmez ve ağın haritasını çıkartmak için kullanılamaz.  
- C) Wireshark 1980 yılında AT&T tarafından geliştirilmiştir.  
- D) Wireshark yalnızca TCP paketlerini çözümler, ARP ve ICMP'yi desteklemez.  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (Hafta 2 Pcap PDF Sayfa 5, Slayt 10):** Slayt 10'da kırmızıyla belirtilen iki altın kural:
1. *"Paket sniffer uygulamasıdır, dolayısıyla bir ağın haritasını çıkartmak için kullanılamaz."*
2. *"Pasif bir izleme aracıdır, dolayısıyla ağ verisi üretmez."*
*(Wireshark 1998'de Gerald Combs tarafından Ethereal adıyla başlatılmış, 2006'da Wireshark olmuştur).*
</details>

---

### Soru 7: `pcap_lookupdev` Fonksiyonu
**Soru:** Bir C libpcap programında sistemdeki varsayılan aktif ağ cihazının adını (`eth0`, `wlan0` vb.) öğrenmek için çağrılan fonksiyon hangisidir? Cihaz bulunamazsa ne döner?  
- A) `pcap_open_live`, hata durumunda `-1` döner  
- B) `pcap_lookupdev`, hata durumunda `NULL` döner ve hatayı `errbuf` dizisine yazar  
- C) `pcap_findalldevs`, hata durumunda `0` döner  
- D) `pcap_compile`, hata durumunda `PCAP_ERROR` döner  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (Hafta 2 Pcap Slayt 14 & `1-arpgonder.c` Satır 14):** `char *dev = pcap_lookupdev(errbuf);` fonksiyonu başarı durumunda cihaz adresi işaretçisi, başarısızlıkta `NULL` döner ve `errbuf` içine açıklama yazar.
</details>

---

### Soru 8: `pcap_open_live` ve Promiscuous Mod
**Soru:** `pcap_open_live(dev, BUFSIZ, 1, 1000, errbuf)` fonksiyon çağrısındaki `1` (üçüncü parametre) neyi ifade eder?  
- A) Paket yakalama işleminin arka planda çalışacağını  
- B) Promiscuous (Karmaşık / Ayrım gözetmeyen) modun açıldığını; hedef MAC adresi kendisine ait olmayan paketlerin de yakalanacağını  
- C) Yalnızca 1 adet paket yakalanıp programın sonlanacağını  
- D) Filtrelemenin aktif olduğunu  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (Hafta 2 Pcap Slayt 15 & `1-arpgonder.c` Satır 22):** `promisc = 1` verildiğinde ağ kartı promiscuous moda geçer ve switch hub gibi davranarak hatta geçen hedefi kim olursa olsun tüm çerçeveleri işletim sistemine iletir.
</details>

---

### Soru 9: BPF Filtreleme Fonksiyonları Sırası
**Soru:** Libpcap kullanarak yalnızca belirli paketleri (örneğin `"port 23"` veya `"icmp"`) filtrelemek için hangi iki fonksiyon hangi sırayla çağrılmalıdır?  
- A) Önce `pcap_setfilter`, sonra `pcap_compile`  
- B) Önce `pcap_compile`, sonra `pcap_setfilter`  
- C) Önce `pcap_open_live`, sonra `pcap_lookupnet`  
- D) Sadece `pcap_filter` fonksiyonu yeterlidir  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (Hafta 2 Pcap Slayt 16 & `ping_server.c` Satır 67-72):**
1. `pcap_compile(handle, &fp, filter_exp, 0, net)` ile metin filtresi BPF bytecode'una derlenir.
2. `pcap_setfilter(handle, &fp)` ile derlenmiş filtre dinleme oturumuna uygulanır.
</details>

---

### Soru 10: CSMA/CD Backoff Algoritması ve 1-Persistent
**Soru:** IEEE 802.3 Ethernet'te CSMA/CD iletiminde hat meşgulse istasyonun hattı sürekli dinlemesi ve hat boşaldığı anda iletime geçmesi prensibine ne ad verilir?  
- A) Non-persistent  
- B) p-persistent  
- C) 1-persistent  
- D) Aloha  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: C**  
**Açıklama (Hafta 2 Katman 2 PDF Sayfa 3, Slayt 5):** Slayt 5'teki akış şemasında görüldüğü üzere istasyon hat boşalana kadar sürekli dinler (`Sense carrier, Busy? Yes -> Sense carrier`), boşaldığı anda IFG süresi bekleyip gönderir. Bu `1-persistent` stratejisidir.
</details>

---

### Soru 11: CSMA/CD Çarpışma ve Jam Sinyali
**Soru:** CSMA/CD çalıştıran bir Ethernet kartı, çerçeveyi gönderirken aynı anda hatta gerilim seviyesinin yükseldiğini görüp çarpışma (collision) sezdiğinde derhal ne yapar?  
- A) Gönderimi iptal edip hemen aynı çerçeveyi baştan gönderir  
- B) İletimi durdurur ve diğer tüm istasyonları uyarmak için hatta bozucu bir "Jam Signal" gönderir  
- C) Bilgisayarı yeniden başlatır  
- D) Paketi doğrudan router'a yönlendirir  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (Hafta 2 Katman 2 Slayt 5):** Çarpışma tespit edildiğinde istasyon derhal çerçeveyi keser, diğer düğümler de çarpışmayı fark etsin diye hatta **Jam Signal** basar ve deneme sayacını ($k$) 1 artırarak rastgele bekleme süresine (backoff) geçer.
</details>

---

### Soru 12: Ethernet II Başlık Boyutu ve Alanları
**Soru:** Ethernet II çerçeve başlığı yazılım katmanında (C programlamada) kaç bayttır ve hangi 3 temel alandan oluşur?  
- A) 20 Bayt (Kaynak IP, Hedef IP, Tip)  
- B) 14 Bayt (Hedef MAC [6B], Kaynak MAC [6B], Tip [2B])  
- C) 28 Bayt (Donanım Tipi, Protokol Tipi, MAC'ler)  
- D) 18 Bayt (Preamble [8B], MAC'ler [6B], CRC [4B])  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (Hafta 2 Katman 2 Slayt 6):**
* Hedef MAC: 6 Bayt (`packet[0..5]`)
* Kaynak MAC: 6 Bayt (`packet[6..11]`)
* Tip (EtherType): 2 Bayt (`packet[12..13]`)
* Toplam = $6 + 6 + 2 = \mathbf{14\text{ Bayt}}$.
</details>

---

### Soru 13: Preamble ve CRC'nin C Kodunda Bulunmama Sebebi
**Soru:** Ethernet çerçevesinin donanım seviyesinde başında 8 bayt Preamble ve sonunda 4 bayt CRC (FCS) bulunmasına rağmen `1-arpgonder.c` veya `2-icmpgonder.c` kodlarında Ethernet başlığı neden 14 bayt olarak dizide tanımlanır?  
- A) Kod yazarı CRC eklemeyi unutmuştur  
- B) Preamble ve CRC hesaplaması ağ arayüz kartı (NIC) donanımı tarafından fiziksel iletim anında yapılıp eklendiği için  
- C) Linux çekirdeği CRC kullanımını yasakladığı için  
- D) Libpcap kütüphanesi sadece 14 baytlık paketleri desteklediği için  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (Hafta 2 Katman 2 Slayt 6):** Preamble (alıcının saatini senkronize etmek için) ve FCS/CRC (fiziksel iletim hatası tespiti için) donanım (PHY/MAC çipi) tarafından otomatik eklenir ve paket yakalanırken donanım tarafından soyulur; bu yüzden yazılım katmanında 14 baytlık başlık kullanılır.
</details>

---

### Soru 14: Multicast Ethernet MAC Kalıbı
**Soru:** Bir Ethernet çerçevesinin hedef MAC adresi hangi özel 3 baytlık önek ile başlıyorsa bu çerçevenin bir **Multicast** grubu hedeflediği anlaşılır?  
- A) `FF:FF:FF`  
- B) `00:00:00`  
- C) `01:00:5E`  
- D) `192:168:1`  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: C**  
**Açıklama (Hafta 2 Katman 2 Slayt 7):** Slayt 7'deki şemaya göre Multicast MAC adresleri her zaman **`01-00-5E`** hex öneki ile başlar (Örnek: `01-00-5E-00-00-01`).
</details>

---

### Soru 15: Broadcast MAC Adresi
**Soru:** Yerel ağdaki (LAN) tüm cihazların ağ kartlarının kabul etmesi amacıyla gönderilen bir Ethernet çerçevesinde hedef MAC adresi ne olarak atanır?  
- A) `00:00:00:00:00:00`  
- B) `FF:FF:FF:FF:FF:FF`  
- C) `255.255.255.255`  
- D) `01:00:5E:FF:FF:FF`  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (Hafta 2 Katman 2 Slayt 7 & `1-arpgonder.c` Satır 28-34):** Broadcast MAC adresi 6 baytın tamamının 1 (`0xFF`) yapıldığı **`FF-FF-FF-FF-FF-FF`** adresidir.
</details>

---

### Soru 16: ARP Paket Boyutu ve Kapsülleme
**Soru:** Standart bir ARP Request veya Reply paketinin kendi gövde boyutu kaç bayttır? Ethernet çerçevesine kapsüllendiğinde toplam paket boyutu kaç bayt olur?  
- A) 20B ARP + 14B Ethernet = 34 Byte  
- B) 28B ARP + 14B Ethernet = 42 Byte  
- C) 28B ARP + 20B IP + 14B Ethernet = 62 Byte  
- D) 32B ARP + 14B Ethernet = 46 Byte  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (Hafta 2 Katman 2 Slayt 11 & 12):** ARP paketinde IP başlığı yoktur! 28 Baytlık ARP şablonu doğrudan Ethernet'in Veri (Data) kısmına yazılır:
$$\mathbf{14\text{ Byte Ethernet Başlığı}} + \mathbf{28\text{ Byte ARP Şablonu}} = \mathbf{42\text{ Byte}}$$
(`1-arpgonder.c` dosyasında `u_char packet[42]` tanımlanmasının sebebi budur).
</details>

---

### Soru 17: ARP Request Alan Değerleri
**Soru:** Bir ARP Request paketi oluşturulurken ARP başlığındaki `Opcode` alanına ve henüz bilinmeyen `Target MAC` alanına sırasıyla hangi değerler atanmalıdır?  
- A) `Opcode = 2`, `Target MAC = FF:FF:FF:FF:FF:FF`  
- B) `Opcode = 1`, `Target MAC = 00:00:00:00:00:00`  
- C) `Opcode = 1`, `Target MAC = FF:FF:FF:FF:FF:FF`  
- D) `Opcode = 2`, `Target MAC = 00:00:00:00:00:00`  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (Hafta 2 Katman 2 Slayt 12 & `1-arpgonder.c` Satır 67-69 & 85-91):**
* `Opcode = 1` $\rightarrow$ ARP Request (`2` olsaydı Reply olurdu).
* `Target MAC` henüz bilinmediği için sıfırlanır (`00:00:00:00:00:00`).
* *(Not: Ethernet başlığındaki Hedef MAC ise tüm ağ duysun diye `FF:FF:FF:FF:FF:FF` yapılır).*
</details>

---

### Soru 18: ARP Farklı Ağa Gönderim Senaryosu (Case 2)
**Soru:** A bilgisayarı (`10.0.1.5`), farklı bir alt ağda bulunan B bilgisayarına (`10.0.2.80`) bir IP paketi göndermek istiyor. A bilgisayarı yerel ağda ARP Request yayınlarken ARP paketindeki `Target IP` alanına hangi adresi yazar?  
- A) B bilgisayarının IP adresini (`10.0.2.80`)  
- B) Kendi IP adresini (`10.0.1.5`)  
- C) Kendi yerel ağ geçidinin (Varsayılan Router) IP adresini  
- D) `255.255.255.255`  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: C**  
**Açıklama (Hafta 2 Katman 2 Slayt 13 - Case 2):** Farklı ağdaki bir cihaza doğrudan ulaşılamaz; paket router üzerinden çıkmalıdır. Bu yüzden kaynak bilgisayar paketi router'a teslim edebilmek için **Router'ın IP adresini** `Target IP` olarak sorgulayıp Router'ın MAC adresini öğrenir.
</details>

---

### Soru 19: ARP Tablosu Durum Harfleri
**Soru:** Slayt 14'te verilen ARP Önbellek Tablosunda yer alan bir satırda `State` (Durum) sütununda **`P`** harfi görülüyorsa bu ne anlama gelir?  
- A) Resolved (Çözümlenmiş, MAC adresi biliniyor)  
- B) Pending (Beklemede, ARP isteği yollandı henüz cevap gelmedi)  
- C) Permanent (Kalıcı statik kayıt)  
- D) Free (Boş satır)  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (Hafta 2 Katman 2 Slayt 14):**
* `R` = *Resolved* (Çözümlendi)
* `P` = *Pending* (Beklemede - istek çıktı yanıt bekleniyor)
* `F` = *Free* (Kullanılabilir boş satır)
</details>

---

### Soru 20: `1-arpgonder.c` Kodundaki Yorum Hatası
**Soru:** `1-arpgonder.c` dosyasının 53. satırında `packet[14]=0x00; packet[15]=0x01;` kodunun yanına `//0x0001=Request` şeklinde bir açıklama yazılmıştır. Bu satırın gerçek protokol görevi nedir ve asıl `Opcode = Request` hangi satırda atanmaktadır?  
- A) Gerçekte donanım tipidir (Ethernet = 1); asıl Opcode Satır 67-69'da (`packet[20..21]`) atanmıştır.  
- B) Gerçekte IP protokol tipidir; asıl Opcode Satır 46'da atanmıştır.  
- C) Kod doğrudur, ARP'de iki kez Request bayrağı yazılır.  
- D) Gerçekte hedef MAC adresidir.  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: A**  
**Açıklama (`1-arpgonder.c` Satır 53 vs 67-69 & Hafta 2 Katman 2 Slayt 12):**
* `packet[14..15]` ARP şablonunun ilk 2 baytı olan **Donanım Tipi (Hardware Type)** alanıdır (`1 = Ethernet`). Yorumdaki `=Request` ifadesi dizgi/yorum hatasıdır.
* Asıl **İşlem Kodu (Opcode)** Satır 67-69'daki `packet[20] = 0x00; packet[21] = 0x01;` atamasıdır.
</details>

---

# 4. Ders (Bölüm 1): Hafta 3 – Katman 3: IPv4, Fragmantasyon, Opsiyonlar, Checksum ve IPv6
**Kaynak Sunum:** `Hafta-3 Katman 3 Protokolleri.pdf` *(PDF Sayfa 1–10, Slayt 1–20)*

## 4.1. IPv4 Temel Özellikleri ve Başlık Yapısı (PDF Sayfa 2–3, Slayt 3–5)
* **Slayt 4 (IPv4 Özellikleri):** Ağ katmanı paketlerine **datagram** denir. **Bağlantısız**, **en iyi teslim (best-effort)** ve **ortam bağımsız** bir protokoldür.
* **Boyut Kuralları (Slayt 4):** IP Başlığı **20–60 bayt** aralığındadır (Sabit kısım **20 bayt**, Opsiyonlar **0–40 bayt**). Toplam datagram boyutu **20–65,535 bayt** aralığındadır.
* **Slayt 5 (`Protocol` Alanı Değerleri Tablosu — `packet[23]`):** **`1` = ICMP**, **`2` = IGMP**, **`6` = TCP**, **`17` = UDP**, **`89` = OSPF**.

![IPv4 Başlık Yapısı](assets/slides/h3_s4_ip_baslik.png)
![IP Datagramı Payload ve Protocol Alanı](assets/slides/h3_s5_ip_payload_proto.png)

---

## 4.2. IPv4 Fragmantasyon (Parçalama) ve Sayısal Hesaplama (PDF Sayfa 3–4, Slayt 6–7)
![IP Datagramı Detaylı Fragmantasyon](assets/slides/h3_s7_fragmantasyon.png)

> [!TIP]
> **Fragmantasyon Sayısal Çözüm Formülleri (Slayt 7):**
> * **Bayraklar (3 Bit):** `D (Do not fragment) = 1` ise parçalanamaz. `M (More fragments) = 1` ise arkadan başka parçalar gelecek, `M = 0` ise bu son parçadır.
> * **Total Length (Toplam Uzunluk):** Her parçaya 20 Byte IP başlığı eklendiği için $\text{Total Length} = \text{Parça Veri Boyutu} + 20$.
> * **Fragmentation Offset:** Son parça hariç her parçadaki veri boyutu **8'in katı** olmalıdır: $\text{Offset} = \text{İlk Veri Baytının Sıra Numarası} \div 8$.
> * **Slayt 7 Örneğinin Adım Adım Çözümü (Orijinal Veri: 4000 Byte [`0000–3999`], Total Length: `4020`, ID: `14,567`):**
>   * **Fragment 1 (`0000–1399`, 1400B veri):** `Total Length` = $1400 + 20 = \mathbf{1420}$ | `M = 1` | `Offset` = $0 \div 8 = \mathbf{000}$.
>   * **Fragment 2 (`1400–2799`, 1400B veri):** `Total Length` = $1400 + 20 = \mathbf{1420}$ | `M = 1` | `Offset` = $1400 \div 8 = \mathbf{175}$.
>     * *Fragment 2.1 (`1400–2199`, 800B veri):* `Total Length` = $800 + 20 = \mathbf{820}$ | `M = 1` | `Offset` = $1400 \div 8 = \mathbf{175}$.
>     * *Fragment 2.2 (`2200–2799`, 600B veri):* `Total Length` = $600 + 20 = \mathbf{620}$ | **`M = 1`** *(arkada hala Fragment 3 var!)* | `Offset` = $2200 \div 8 = \mathbf{275}$.
>   * **Fragment 3 (`2800–3999`, 1200B veri):** `Total Length` = $1200 + 20 = \mathbf{1220}$ | **`M = 0`** *(Son parça!)* | `Offset` = $2800 \div 8 = \mathbf{350}$.

---

## 4.3. IPv4 Başlık Opsiyonları (Seçenekler) (PDF Sayfa 4–9, Slayt 8–17)
![Opsiyon Type Alanı](assets/slides/h3_s9_opsiyon_type.png)
![Opsiyon Ağacı](assets/slides/h3_s10_opsiyon_agaci.png)

| Kategori (Slayt 10) | Opsiyon Adı | Type / Code Değeri | Slayt No | Görevi ve Çalışma Mantığı |
| :--- | :--- | :---: | :---: | :--- |
| **Single-byte** | **No operation (`NO-OP`)** | `Type: 1` (`00000001`) | Slayt 11 | Seçenekleri 16/32-bit sınırına **hizalamak (align)** için kullanılır. |
| **Single-byte** | **End of option (`END-OP`)**| `Type: 0` (`00000000`) | Slayt 11 | Seçeneklerin sonunu **doldurmak (padding)** için kullanılır. |
| **Multiple-byte**| **Record route** | `Type: 7` (`00000111`) | Slayt 11–12| Başlangıçta boş olan (maks. **9 adreslik**) listeye, paketin geçtiği her router kendi çıkış IP adresini kaydeder (`Pointer` 4 artar). |
| **Multiple-byte**| **Strict source route** | `Type: 137` (`10001001`)| Slayt 13–14| **Kesin Kaynak Yönlendirme:** Gönderen, geçilecek **tüm** router IP'lerini baştan belirler; paket liste dışındaki hiçbir router'dan geçemez! |
| **Multiple-byte**| **Loose source route** | `Type: 131` (`10000011`)| Slayt 15 | **Esnek Kaynak Yönlendirme:** Paket listedeki router'lara uğramak zorundadır ama aralarında başka router'lardan da geçebilir. |
| **Multiple-byte**| **Timestamp** | `Code: 68` (`01000100`) | Slayt 16–17| Geçilen her router'ın IP adresini ve paketin işlendiği **zaman damgasını** kaydeder. |

---

## 4.4. IPv4 Kontrol Toplamı (Checksum), İşletim Modülleri ve IPv6 (PDF Sayfa 9–10, Slayt 18–20)
![IP Başlık Kontrol Toplamı](assets/slides/h3_s18_checksum.png)
![IP Datagramının İşletimi Modülleri](assets/slides/h3_s19_ip_moduller.png)
![IPv6 ve Başlık Karşılaştırması](assets/slides/h3_s20_ipv6.png)

* **Slayt 18 (Kontrol Toplamı / Checksum):** Başlık 16-bitlik satırlara bölünür. Gönderende Checksum alanı `0` yapılarak toplanır (`Sum`) ve **1'e tümleyeni (bitlerin tersi)** alınarak Checksum alanına (`35761`) yazılır. Alıcıda tüm başlık (Checksum dahil) toplandığında `Sum = 11111111 11111111` ve tersi alındığında **`Checksum = 0000 0000 0000 0000`** çıkmalıdır.
* **Slayt 19 (4 İşletim Modülü):** `Adding Module`, `Processing Module` (Router ise `TTL` azaltır, `TTL <= 0` ise atıp ICMP hata döner), `Fragmantasyon Module` (`Boyut > MTU` ve `D=1` ise atıp ICMP hata döner), `Reassembly Module` (Süre aşımı olursa tüm fragmentleri düşürüp ICMP hata döner).
* **Slayt 20 (IPv6):** **128 bit adresleme** (340 undesilyon adres), **NAT ihtiyacını ortadan kaldırır**, entegre güvenlik. IPv6 başlığında `IHL`, `Identification`, `Flags`, `Fragment Offset` ve `Header Checksum` kaldırılmış; `TTL` $\rightarrow$ `Hop Limit`, `Protocol` $\rightarrow$ `Next Header`, `Type of Service` $\rightarrow$ `Traffic Class` olmuş ve **`Flow Label`** eklenmiştir.

---

# 5. Ders (Bölüm 2): Hafta 3 – Katman 3: ICMP Protokolü ve 3 C Kodu
**Kaynak Sunum ve Kodlar:** `Hafta-3 Katman 3 Protokolleri.pdf` *(PDF Sayfa 11–16, Slayt 21–32)* & [`2-icmpgonder.c`](./0-Katman2-3%20Kodlar/2-icmpgonder.c), [`ping_server.c`](./0-Katman2-3%20Kodlar/Ping%20Uygulaması/ping_server.c), [`ping_client.c`](./0-Katman2-3%20Kodlar/Ping%20Uygulaması/ping_client.c)

## 5.1. ICMP Kapsüllemesi, 8 Byte Başlık ve Mesaj Kategorileri (PDF Sayfa 11–12, Slayt 21–23)
![ICMP Kapsülleme](assets/slides/h3_s21_icmp_kapsulleme.png)
![ICMP Başlık ve Mesaj Kategorileri](assets/slides/h3_s22_icmp_tablo.png)

## 5.2. ICMP Hata Raporlama ve Sorgu Mesajları Kuralları (PDF Sayfa 12–16, Slayt 24–31)
![ICMP Hedef Ulaşılamaz Type 3](assets/slides/h3_s24_icmp_type3.png)
![ICMP Yeniden Yönlendirme Type 5](assets/slides/h3_s28_icmp_type5_redirect.png)
![ICMP Echo Request ve Reply Type 8 ve 0](assets/slides/h3_s29_icmp_echo.png)

> [!IMPORTANT]
> **Sınavda Kesin Sorulabilecek ICMP Hata Kuralları (Slayt 24–30):**
> * **Ortak Kural (Slayt 24–28):** Tüm ICMP hata mesajları, hataya sebep olan paketin **IP başlığını + orijinal verinin ilk 8 baytını** (`IP header plus the first 8 bytes of datagram data`) içerir.
> * **1) Hedef Ulaşılamaz (`Type: 3, Code: 0..15` — Slayt 24):**
>   * **`Code 2` (Protokol ulaşılamaz) ve `Code 3` (Port ulaşılamaz)** mesajları **YALNIZCA hedef ana bilgisayar (Host)** tarafından oluşturulabilir!
>   * Diğer tüm `Type 3` iletileri **YALNIZCA yönlendiriciler (Router)** tarafından oluşturulabilir!
> * **2) Kaynak Söndürme (`Type: 4, Code: 0` — Slayt 25):** Yönlendirici veya hedefteki tıkanıklık nedeniyle **atılan her datagram için** gönderilir; kaynağın gönderimi yavaşlatmasını ister.
> * **3) Zaman Aşımı (`Type: 11, Code: 0 veya 1` — Slayt 26):**
>   * **`Code 0`:** Yalnızca **yönlendiriciler (Router)** tarafından `TTL = 0` olduğunda gönderilir.
>   * **`Code 1`:** Yalnızca **hedef ana bilgisayar (Host)** tarafından, parçalanmış datagramın tüm parçaları süresi içinde gelmediğinde gönderilir.
> * **4) Parametre Problemi (`Type: 12, Code: 0 veya 1` — Slayt 27):** Yönlendirici veya hedef host tarafından oluşturulabilir; `Pointer` alanı hatanın olduğu baytı gösterir.
> * **5) Yeniden Yönlendirme / Redirection (`Type: 5, Code: 0..3` — Slayt 28):** Yönlendiriciden (`R1`), **aynı yerel ağdaki (LAN)** bir ana bilgisayara (`Host A`) gönderilerek yönlendirme tablosunu hedef yönlendirici (`R2`) ile güncellemesini sağlar.
> * **6) Sorgu Mesajları (Slayt 29–30):** `Type 8 / 0` (Echo Request / Reply — `ping, traceroute`) ve `Type 13 / 14` (Timestamp Request / Reply — **saatler senkronize olmasa bile** gidiş-dönüş süresi RTT hesabı ve saat eşitleme yapar).

---

## 5.3. Kod Analizi 1: [`2-icmpgonder.c`](./0-Katman2-3%20Kodlar/2-icmpgonder.c) (Satır 1–118) — 50 Byte ICMP Echo Request

**Toplam Boyut:** `14 Byte` (Ethernet Başlığı) + `20 Byte` (IPv4 Başlığı) + `16 Byte` (8B ICMP Başlığı + 8B Veri) = **`50 Byte`** (`u_char packet[50]`)

| Dizi İndeksi | Boyut | Katman ve Alan Adı | Kodda Atanan Değer | `2-icmpgonder.c` Satır No ve Açıklama |
| :--- | :---: | :--- | :--- | :--- |
| `packet[0..5]` | 6 Byte | L2 Ethernet: Hedef MAC | `00:50:56:fc:18:27` | **[Satır 24–29](./0-Katman2-3%20Kodlar/2-icmpgonder.c#L24-L29):** Alıcı MAC adresi. |
| `packet[6..11]` | 6 Byte | L2 Ethernet: Kaynak MAC | `00:0c:29:cd:27:50` | **[Satır 32–37](./0-Katman2-3%20Kodlar/2-icmpgonder.c#L32-L37):** Gönderen MAC adresi. |
| `packet[12..13]` | 2 Byte | L2 Ethernet: Tip (EtherType) | `0x08, 0x00` (`0x0800`) | **[Satır 40–41](./0-Katman2-3%20Kodlar/2-icmpgonder.c#L40-L41):** Üst katmanın **IPv4** olduğunu belirtir. |
| `packet[14]` | 1 Byte | L3 IPv4: Version + HLEN | `0x45` | **[Satır 45](./0-Katman2-3%20Kodlar/2-icmpgonder.c#L45):** `4` = IPv4, `5` = $5 \times 4 = 20\text{ Byte}$ IP başlığı. |
| `packet[15]` | 1 Byte | L3 IPv4: Service Type | `0x00` | **[Satır 48](./0-Katman2-3%20Kodlar/2-icmpgonder.c#L48):** Servis alanı (TOS). |
| `packet[16..17]` | 2 Byte | L3 IPv4: Total Length | `0x00, 0x24` (`36 Byte`) | **[Satır 51–52](./0-Katman2-3%20Kodlar/2-icmpgonder.c#L51-L52):** $20\text{B IP} + 16\text{B ICMP} = 36\text{ Byte}$ (Hex `0x24`). |
| `packet[18..19]` | 2 Byte | L3 IPv4: Identification | `0x10, 0xfd` | **[Satır 55–56](./0-Katman2-3%20Kodlar/2-icmpgonder.c#L55-L56):** Paket kimlik numarası. |
| `packet[20..21]` | 2 Byte | L3 IPv4: Flags + Offset | `0x00, 0x00` | **[Satır 59–60](./0-Katman2-3%20Kodlar/2-icmpgonder.c#L59-L60):** Parçalanma yok. |
| `packet[22]` | 1 Byte | L3 IPv4: TTL | `0x40` (`64`) | **[Satır 63](./0-Katman2-3%20Kodlar/2-icmpgonder.c#L63):** Yaşam süresi = 64 (`ping_client.c` Satır 182'de okunur!). |
| `packet[23]` | 1 Byte | L3 IPv4: Protocol | `0x01` (`1 = ICMP`) | **[Satır 66](./0-Katman2-3%20Kodlar/2-icmpgonder.c#L66):** IP'nin içinde **ICMP** taşındığını belirtir (Slayt 5). |
| `packet[24..25]` | 2 Byte | L3 IPv4: Header Checksum | `0x00, 0x00` | **[Satır 69–70](./0-Katman2-3%20Kodlar/2-icmpgonder.c#L69-L70):** IP başlık kontrol toplamı. |
| `packet[26..29]` | 4 Byte | L3 IPv4: Kaynak IP | `0xc0, 0xa8, 0x0b, 0x80` | **[Satır 73–76](./0-Katman2-3%20Kodlar/2-icmpgonder.c#L73-L76):** `192.168.11.128`. |
| `packet[30..33]` | 4 Byte | L3 IPv4: Hedef IP | `0xd8, 0x3a, 0xce, 0xc4` | **[Satır 79–82](./0-Katman2-3%20Kodlar/2-icmpgonder.c#L79-L82):** `216.58.206.196`. |
| `packet[34]` | 1 Byte | ICMP: Tip Alanı (Type) | `0x08` | **[Satır 86](./0-Katman2-3%20Kodlar/2-icmpgonder.c#L86):** `8` = **ICMP Echo Request** (Cevapta `0x00` yapılır). |
| `packet[35]` | 1 Byte | ICMP: Kod Alanı (Code) | `0x00` | **[Satır 89](./0-Katman2-3%20Kodlar/2-icmpgonder.c#L89):** `0` *(Not: `ping_client.c` Satır 295'te özel olarak `0x08` verilmiştir)*. |
| `packet[36..37]` | 2 Byte | ICMP: Checksum | `0x00, 0x00` | **[Satır 92–93](./0-Katman2-3%20Kodlar/2-icmpgonder.c#L92-L93):** ICMP kontrol toplamı. |
| `packet[38..41]` | 4 Byte | ICMP: Rest of Header | `0x11, 0x8d, 0x00, 0x1b` | **[Satır 96–99](./0-Katman2-3%20Kodlar/2-icmpgonder.c#L96-L99):** Identifier (2B) + Sequence Number (2B) (Slayt 29). |
| `packet[42..49]` | 8 Byte | ICMP: Zaman Damgası (Data) | `0xa6, 0x5d, 0x4d, 0x5e...` | **[Satır 102–109](./0-Katman2-3%20Kodlar/2-icmpgonder.c#L102-L109):** 8 byte isteğe bağlı veri / zaman damgası. |

---

## 5.4. Kod Analizi 2: [`ping_server.c`](./0-Katman2-3%20Kodlar/Ping%20Uygulaması/ping_server.c) ve [`ping_client.c`](./0-Katman2-3%20Kodlar/Ping%20Uygulaması/ping_client.c)

* **1) Dinamik BPF Filtresi Oluşturma (`filter_ip_address` — [`ping_server.c` Satır 148–176](./0-Katman2-3%20Kodlar/Ping%20Uygulaması/ping_server.c#L148-L176) & [`ping_client.c` Satır 186–212](./0-Katman2-3%20Kodlar/Ping%20Uygulaması/ping_client.c#L186-L212)):**
  * `pcap_findalldevs(&alldevs, error_buffer)` ile tüm ağ arayüzlerini bağlı liste olarak alır.
  * `strcmp(d->name, device) == 0` ile aktif cihazı bulur; `a->addr->sa_family == AF_INET` kontrolüyle IPv4 adresini `inet_ntoa(((struct sockaddr_in *)a->addr)->sin_addr)` ile stringe çevirir ve `" icmp && dst <kendi_IP_adresi>"` filtresini oluşturur.
* **2) Sunucuda Echo Request Yakalayıp Echo Reply Gönderme ([`ping_server.c` Satır 82–137](./0-Katman2-3%20Kodlar/Ping%20Uygulaması/ping_server.c#L82-L137)):**

```c
// ping_server.c Satır 107-118: Kaynak/Hedef MAC ve IP Adreslerini Takas Edip Echo Reply Gönderme
for (int i = 0; i < 4; i++) {
    swap(&my_packet[i + 0], &my_packet[i + 6]);   // MAC adresi ilk 4 byte takası (packet[0..3] <-> packet[6..9])
    swap(&my_packet[i + 26], &my_packet[i + 30]); // IP adresi 4 byte takası (packet[26..29] <-> packet[30..33])
}
swap(&my_packet[4], &my_packet[10]); // MAC 5. byte takası
swap(&my_packet[5], &my_packet[11]); // MAC 6. byte takası (Çünkü MAC 6 byte, IP ise 4 byte'tır!)

my_packet[34] = 0x00; // ICMP Type: Echo Request (0x08) -> Echo Reply (0x00) yapılır!
pcap_sendpacket(handle, my_packet, 50);
```

---
## 5.5. Hafta 3 Değerlendirme Soruları (20 Soru & Çözümleri)

### Soru 1: IPv4 Başlık Boyutu ve HLEN Alanı
**Soru:** Bir IPv4 datagram başlığının sabit boyutu kaç bayttır ve opsiyonlarla en fazla kaç bayt olabilir? 4 bitlik HLEN (Header Length) alanı bu boyutu nasıl gösterir?  
- A) Sabit 14B, maks 42B; bayt sayısı doğrudan yazılır  
- B) Sabit 20B, maks 60B; 4 baytlık kelime sayısını tutar ($5 \times 4 = 20$, $15 \times 4 = 60$)  
- C) Sabit 32B, maks 64B; 2 baytlık kelime sayısını tutar  
- D) Sabit 20B, maks 65,535B; bit sayısı yazılır  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (Hafta 3 PDF Sayfa 2, Slayt 4):** IPv4 başlığı sabit 20 bayt, opsiyonlarla (0–40 bayt) en fazla 60 bayttır. HLEN alanı 4 bitlik olduğundan ($0\text{--}15$) başlık uzunluğunu 4 baytlık bloklar cinsinden saklar. Bu nedenle HLEN değeri $5 \le \text{HLEN} \le 15$ aralığındadır.
</details>

---

### Soru 2: IPv4 Protokol Alanı Eşleştirmesi
**Soru:** Bir IPv4 paketinin başlığındaki `Protocol` (Slayt 5) alanında ICMP, TCP ve UDP protokolleri için sırasıyla hangi ondalık değerler yer alır?  
- A) 1, 6, 17  
- B) 2, 6, 89  
- C) 1, 17, 6  
- D) 6, 1, 17  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: A**  
**Açıklama (Hafta 3 Slayt 5 & `2-icmpgonder.c` Satır 66):**
* `1` = ICMP (`packet[23] = 0x01`)
* `2` = IGMP
* `6` = TCP
* `17` = UDP
* `89` = OSPF
</details>

---

### Soru 3: Fragmantasyon Bayrakları (Flags)
**Soru:** IPv4 başlığındaki 3 bitlik Bayraklar (Flags) alanında yer alan `D` (Do not fragment) ve `M` (More fragments) bitlerinin `D = 0, M = 1` olması ne anlama gelir?  
- A) Paket parçalanamaz ve bu son parçadır  
- B) Paket parçalanabilir ve arkasından gelen başka parçalar vardır  
- C) Paket parçalanamaz ve bu ilk parçadır  
- D) Paket bozuktur, atılmalıdır  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (Hafta 3 Slayt 6 & 7):**
* `D = 0`: Parçalanmaya izin verilmiştir.
* `M = 1`: Arkadan daha fazla parça gelecektir (More fragments).
* `M = 0`: Bu parça son parçadır.
</details>

---

### Soru 4: Parçalama Ofseti (Fragmentation Offset) Kuralı
**Soru:** IP fragmantasyonunda her parçadaki veri boyutunun (son parça hariç) mutlaka **8'in katı** olmasının matematiksel sebebi nedir?  
- A) Ağ kartlarının sadece 8 bitlik veri işleyebilmesi  
- B) Fragmentation Offset alanının 13 bit olması ve bayt numarasını 8'e bölerek ($8\text{ baytlık birimler}$) saklaması  
- C) IPv4 adreslerinin 4 bayt (32 bit) olması  
- D) Checksum alanının 8 bitlik olması  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (Hafta 3 Slayt 7):** Toplam veri boyutu 65,535 bayta kadar çıkabilirken offset alanı 13 bittir ($2^{13} = 8192$). 65,535 sayısını 8192 içine sığdırmak için her offset değeri 8 baytlık bloğu temsil eder ($\text{Offset} = \text{Bayt No} \div 8$). Bu yüzden veri boyutu 8'e tam bölünmelidir.
</details>

---

### Soru 5: Sayısal Fragmantasyon Problemi
**Soru (Slayt 7 Örneği):** 4000 baytlık veri taşıyan bir IP datagramı (Toplam Uzunluk = 4020, ID = 14567) MTU = 1420 olan bir hattan geçerken 3 parçaya ayrılıyor:
* 1. Parça: 0 – 1399 baytlar (1400B)
* 2. Parça: 1400 – 2799 baytlar (1400B)
* 3. Parça: 2800 – 3999 baytlar (1200B)  
Buna göre **2. parçanın** Total Length, M biti ve Offset değeri sırasıyla nedir?  
- A) Total Length = 1400, M = 0, Offset = 175  
- B) Total Length = 1420, M = 1, Offset = 175  
- C) Total Length = 1420, M = 1, Offset = 1400  
- D) Total Length = 1400, M = 1, Offset = 0  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (Hafta 3 Slayt 7):**
1. $\text{Total Length} = 1400\text{ (veri)} + 20\text{ (IP başlığı)} = \mathbf{1420}$
2. Arkadan 3. parça geleceği için $\mathbf{M = 1}$
3. $\text{Offset} = \frac{\text{İlk Bayt Numarası}}{8} = \frac{1400}{8} = \mathbf{175}$
*(3. parça için Total Length = 1220, M = 0, Offset = 2800 / 8 = 350 olurdu).*
</details>

---

### Soru 6: Tek Baytlık Opsiyonlar: NO-OP ve END-OP
**Soru:** IPv4 başlık opsiyonlarında tek baytlık (Single-byte) seçeneklerden `NO-OP (Type: 1)` ve `END-OP (Type: 0)` hangi amaçla kullanılır?  
- A) NO-OP hatalı paketleri düşürür, END-OP paketi sonlandırır  
- B) NO-OP seçenekleri 32-bit (4 bayt) sınırına hizalamak (alignment), END-OP ise kalan boşluğu doldurmak (padding) için kullanılır  
- C) NO-OP şifreleme yapar, END-OP rotayı kaydeder  
- D) İkisi de yönlendirme amacıyla kullanılır  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (Hafta 3 Slayt 10 & 11):** Başlık uzunluğunun 4 baytın katı olması zorunludur. Araya gelen seçenekleri hizalamak için aralara `NO-OP (1)`, seçenekler listesinin bittiğini belirtip kalan alanı sıfırlamak için `END-OP (0)` eklenir.
</details>

---

### Soru 7: Record Route Opsiyonu Maksimum Adres Sayısı
**Soru:** IPv4 başlığında `Record Route (Type: 7)` seçeneği kullanıldığında bir paketin başlığına en fazla kaç adet yönlendirici (Router) IP adresi kaydedilebilir?  
- A) 5  
- B) 9  
- C) 10  
- D) 15  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (Hafta 3 Slayt 11 & 12):** IP başlığında opsiyonlar için maksimum alan 40 bayttır. Record Route seçeneğinin 3 baytlık kendi başlığı vardır (`Type=1B, Length=1B, Pointer=1B`). Geriye $40 - 3 = 37\text{ bayt}$ kalır. Her IPv4 adresi 4 bayt olduğundan: $\lfloor 37 \div 4 \rfloor = \mathbf{9\text{ adres}}$ kaydedilebilir.
</details>

---

### Soru 8: Strict vs Loose Source Route Farkı
**Soru:** Kaynak Yönlendirme seçeneklerinden `Strict Source Route (Type: 137)` ile `Loose Source Route (Type: 131)` arasındaki temel fark nedir?  
- A) Strict şifrelidir, Loose şifresizdir  
- B) Strict'te paket YALNIZCA belirtilen router'lardan geçebilir, araya başka router giremez; Loose'ta ise listelenen router'lara uğramak şartıyla aradaki diğer router'lardan da geçebilir  
- C) Loose'ta router sınırı yoktur, Strict'te 3 router sınırı vardır  
- D) Strict yerel ağda, Loose geniş ağda kullanılır  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (Hafta 3 Slayt 13, 14, 15):**
* **Strict (Kesin):** Gönderici tüm yolu baştan belirler. Paket listede olmayan tek bir router'a dahi uğrarsa paket atılır ve ICMP hatası üretilir.
* **Loose (Esnek):** Paket listedeki duraklara mutlaka uğramak zorundadır ancak duraklar arasında istediği router'lar üzerinden geçebilir.
</details>

---

### Soru 9: IPv4 Kontrol Toplamı (Checksum) Hesabı
**Soru:** Gönderici bilgisayar IPv4 başlık kontrol toplamını (Header Checksum) hesaplarken Checksum alanına önce ne yazar ve toplama işleminin ardından hangi matematiksel işlemi uygular?  
- A) Rastgele bir sayı yazar ve 2'ye böler  
- B) Checksum alanını 0x0000 yapar, tüm 16-bitlik kelimeleri toplar ve toplamın 1'e tümleyenini (bit tersini) alarak bu alana yazar  
- C) Checksum alanına 0xFFFF yazar ve CRC-32 hesaplar  
- D) IP adreslerinin XOR işlemini alır  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (Hafta 3 Slayt 18):** Checksum alanına önce sıfır yazılır. Başlık 16-bitlik bloklar halinde toplanır (elde bitleri en alta eklenir). Elde edilen sonucun **1'e tümleyeni (bitlerin tersi: 1 $\rightarrow$ 0, 0 $\rightarrow$ 1)** alınarak Checksum alanına yerleştirilir.
</details>

---

### Soru 10: Checksum Alıcı Sağlaması
**Soru:** Alıcı cihaz bir IPv4 paketi aldığında Checksum alanı dahil tüm başlığı 16-bitlik bloklar halinde toplar ve sonucun 1'e tümleyenini alır. Paketin hatasız kabul edilmesi için sonucun ne çıkması gerekir?  
- A) `0xFFFF` (1111 1111 1111 1111)  
- B) `0x0000` (0000 0000 0000 0000)  
- C) Göndericinin IP adresi  
- D) Paketin toplam uzunluğu  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (Hafta 3 Slayt 18):** Başlığın kendisi ile kendi tersi (checksum) toplandığında tüm bitler 1 (`1111...`) olur. Bunun 1'e tümleyeni (tersi) alındığında sonucun kesinlikle **`0000 0000 0000 0000`** çıkması gerekir; aksi halde paket bozulmuştur ve atılır.
</details>

---

### Soru 11: IP İşletim Modüllerinde TTL ve ICMP
**Soru:** Slayt 19'daki IP İşletim Modüllerinden `Processing Module`, bir yönlendiriciden geçen paket için TTL değerini 1 azalttığında `TTL <= 0` olursa ne yapar?  
- A) Paketi hedefe ulaştırıp geri dönmesini ister  
- B) Paketi düşürür (discard) ve kaynağa `ICMP Time Exceeded (Type 11)` hata mesajı gönderir  
- C) TTL değerini tekrar 64 yapar  
- D) Paketi doğrudan bir sonraki router'a devreder  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (Hafta 3 Slayt 19 & Slayt 26):** Paketlerin döngüye girip ağı tıkamasını engellemek için TTL sıfır olduğunda router paketi atar ve kaynak düğüme `ICMP Type 11 Code 0` (Zaman Aşımı) hata bildirimi döner (`traceroute` bu mantıkla çalışır).
</details>

---

### Soru 12: IPv6 Başlığında Yapılan Temel Değişiklikler
**Soru:** IPv6 protokolünde IPv4 başlığına kıyasla aşağıdaki değişikliklerden hangisi **yapılmamıştır**?  
- A) Adres uzunluğu 32 bitten 128 bite çıkarılmıştır  
- B) Başlık Checksum alanı kaldırılarak yönlendiricilerin işlem yükü azaltılmıştır  
- C) Gerçek zamanlı akışlar için `Flow Label` (Akış Etiketi) alanı eklenmiştir  
- D) Başlık boyutu değişken yapılarak 20 ile 120 bayt arasına çıkarılmıştır  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: D**  
**Açıklama (Hafta 3 Slayt 20):** IPv6 temel başlığı değişken değil, **sabit 40 bayt** boyutundadır! Opsiyonlar başlık içine değil, uzantı başlıkları (Extension Headers) olarak araya eklenir. Checksum, IHL, Fragmantasyon alanları temel başlıktan tamamen kaldırılmıştır.
</details>

---

### Soru 13: ICMP Başlık Formatı ve Kapsülleme
**Soru:** ICMP protokol başlığı kaç bayttır ve ilk 4 baytı hangi alanlardan oluşur?  
- A) 20 Bayt: Type (4B), Code (4B), Checksum (4B), Rest (8B)  
- B) 8 Bayt: Type (1B), Code (1B), Checksum (2B), Rest of Header (4B)  
- C) 14 Bayt: Source (6B), Destination (6B), Type (2B)  
- D) 4 Bayt: Type (1B), Code (1B), Checksum (2B)  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (Hafta 3 Slayt 22 & `2-icmpgonder.c` Satır 86-99):** ICMP başlığı sabit 8 bayttır:
* `Type`: 1 Bayt (`packet[34]`)
* `Code`: 1 Bayt (`packet[35]`)
* `Checksum`: 2 Bayt (`packet[36..37]`)
* `Rest of Header`: 4 Bayt (`packet[38..41]` - ID ve Sequence No)
</details>

---

### Soru 14: ICMP Hata Mesajlarının Ortak Gövde Kuralı
**Soru:** Ağdaki bir hata nedeniyle oluşturulan tüm ICMP hata mesajlarının veri (payload) kısmında hataya yol açan orijinal pakete ait hangi bilgiler yer alır?  
- A) Yalnızca kaynak MAC adresi  
- B) Orijinal paketin IP başlığı + datagram verisinin ilk 8 baytı  
- C) Orijinal paketin tüm verisi  
- D) Yalnızca ICMP başlığı  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (Hafta 3 Slayt 24, 25, 26, 27, 28):** Tüm ICMP hata mesajları standart olarak `IP header plus the first 8 bytes of original datagram data` içerir. Böylece hatayı alan kaynak, hangi protokole ve hangi porta ait segmentin hata verdiğini ilk 8 bayttaki TCP/UDP port numaralarına bakarak anlar.
</details>

---

### Soru 15: ICMP Type 3 (Destination Unreachable) Kritik Kuralı
**Soru:** ICMP Hedef Ulaşılamaz (Type 3) mesajlarında yer alan `Code 2` (Protokol ulaşılamaz) ve `Code 3` (Port ulaşılamaz) iletileri kim tarafından oluşturulabilir?  
- A) Yalnızca ağdaki yönlendiriciler (Router)  
- B) YALNIZCA hedef ana bilgisayar (Destination Host)  
- C) Kaynak ana bilgisayar  
- D) Güvenlik duvarı (Firewall)  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (Hafta 3 Slayt 24):** Slayt 24'teki nota göre:
* **`Code 2` (Protokol ulaşılamaz) ve `Code 3` (Port ulaşılamaz)** YALNIZCA hedef ana bilgisayar (Host) tarafından oluşturulabilir.
* Diğer tüm Type 3 iletileri (Ağ ulaşılamaz, Host ulaşılamaz vb.) ise YALNIZCA yönlendiriciler (Router) tarafından oluşturulabilir.
</details>

---

### Soru 16: ICMP Zaman Aşımı (Type 11) Code 0 vs Code 1
**Soru:** ICMP Time Exceeded (Type 11) mesajında `Code 0` ile `Code 1` ayrımı aşağıdakilerden hangisinde doğru açıklanmıştır?  
- A) Code 0 router tarafından TTL=0 olduğunda; Code 1 hedef host tarafından tüm parçalar süre aşımında tamamlanamadığında üretilir  
- B) Code 0 bağlantı kurulurken; Code 1 bağlantı koparken üretilir  
- C) Code 0 host tarafından; Code 1 router tarafından TTL bittiğinde üretilir  
- D) İkisi de aynı durum için kullanılır  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: A**  
**Açıklama (Hafta 3 Slayt 26):**
* **`Code 0`:** Yönlendirici (Router) paketin TTL sayacı sıfırlandığında paketi atar ve bu mesajı döner.
* **`Code 1`:** Hedef ana bilgisayar (Host) parçalanmış bir paketin ilk parçası geldikten sonra süre aşımı (Reassembly timer) dolmasına rağmen diğer parçalar gelmediğinde tüm parçaları atıp bu mesajı döner.
</details>

---

### Soru 17: ICMP Yeniden Yönlendirme (Type 5 - Redirection)
**Soru:** ICMP Redirection (Type 5) mesajının temel amacı nedir?  
- A) Web sitelerini başka bir URL'ye yönlendirmek  
- B) Bir yerel ağdaki yönlendiricinin (R1), ana bilgisayara (Host A) belirli bir hedefe giderken kendisi yerine aynı yerel ağdaki daha uygun başka bir yönlendiriciyi (R2) kullanması gerektiğini bildirerek yönlendirme tablosunu güncellemesini sağlamak  
- C) Paketleri döngüye sokarak ağ trafiğini test etmek  
- D) DNS sunucu adresini değiştirmek  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (Hafta 3 Slayt 28):** Slayt 28'deki topolojiye göre R1, aynı LAN'daki Host A'ya paketi R2 üzerinden göndermesinin daha kısa yol olduğunu söyler ve Host A yönlendirme tablosundaki ilgili satırı R2 ile günceller.
</details>

---

### Soru 18: `2-icmpgonder.c` Paket Boyutu Analizi
**Soru:** `2-icmpgonder.c` kodunda kabloya gönderilen `packet` dizisi `u_char packet[50]` olarak tanımlanmıştır. Bu 50 baytın katmanlara göre dağılımı aşağıdakilerden hangisidir?  
- A) 14B Ethernet + 20B IPv4 + 16B ICMP (8B Başlık + 8B Veri)  
- B) 14B Ethernet + 28B ARP + 8B ICMP  
- C) 20B Ethernet + 20B IPv4 + 10B ICMP  
- D) 14B Ethernet + 24B IPv4 + 12B ICMP  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: A**  
**Açıklama (`2-icmpgonder.c` Satır 24-109):**
* `packet[0..13]`: 14 Byte Ethernet Başlığı
* `packet[14..33]`: 20 Byte IPv4 Başlığı
* `packet[34..41]`: 8 Byte ICMP Başlığı (Type 0x08 Echo Request)
* `packet[42..49]`: 8 Byte ICMP Veri / Zaman Damgası
* Toplam = $14 + 20 + 8 + 8 = \mathbf{50\text{ Bayt}}$.
</details>

---

### Soru 19: `ping_server.c` Takas (Swap) Algoritması
**Soru:** `ping_server.c` programında yakalanan bir ICMP Echo Request paketine Echo Reply cevabı oluşturulurken MAC ve IP adresleri için neden iki ayrı `swap` döngüsü kurulmuştur?  
- A) MAC adresleri 6 bayt, IPv4 adresleri ise 4 bayt olduğu için  
- B) MAC adresleri şifreli olduğu için  
- C) IPv4 adresleri ters sırada saklandığı için  
- D) Kod yazarı döngü sınırını yanlış hesapladığı için  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: A**  
**Açıklama (`ping_server.c` Satır 107-118):** Kodda `for(int i=0; i<4; i++)` döngüsüyle ilk 4 byte'lık MAC (`packet[0..3]` $\leftrightarrow$ `packet[6..9]`) ve 4 byte'lık IP (`packet[26..29]` $\leftrightarrow$ `packet[30..33]`) takas edilir. MAC 6 bayt olduğundan kalan 2 bayt (`packet[4..5]` $\leftrightarrow$ `packet[10..11]`) döngü dışında ayrıca takas edilir.
</details>

---

### Soru 20: `ping_server.c` ICMP Type Dönüşümü
**Soru:** `ping_server.c` kodunda gelen Echo Request paketi Echo Reply'a dönüştürülürken `packet[34]` baytına hangi değer atanır?  
- A) `0x08`  
- B) `0x00`  
- C) `0x01`  
- D) `0xFF`  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (`ping_server.c` Satır 120 & Hafta 3 Slayt 29):**
* `Type: 8` (`0x08`) = ICMP Echo Request (İstek)
* `Type: 0` (`0x00`) = ICMP Echo Reply (Cevap)
Sunucu isteği cevaplamak için `my_packet[34] = 0x00;` ataması yapar.
</details>

---

# 6. Ders (Bölüm 1): Hafta 4 – Katman 4: TCP Segment Yapısı, 3-Way Handshake, Durum Şeması, Akış ve Hata Kontrolü
**Kaynak Sunum:** `Hafta-4 Katman 4 Protokolleri.pdf` *(PDF Sayfa 1–12, Slayt 1–24)*

## 6.1. TCP Temel Özellikleri, Portlar, Segment Yapısı ve Akış Gönderimi (PDF Sayfa 2–4, Slayt 3–7)
![TCP Port Numaraları](assets/slides/h4_s4_tcp_portlar.png)
![TCP Segment Yapısı](assets/slides/h4_s5_tcp_segment.png)
![TCP Akış Gönderimi ve Tamponlar](assets/slides/h4_s6_akis_gonderimi.png)
![TCP Kapsülleme İşlemi](assets/slides/h4_s7_tcp_kapsulleme.png)

* **Slayt 3 (TCP Genel Bilgiler):**
  * **TCP (Transmission Control Protocol):** **Bağlantı yönelimlidir (Connection-oriented)** ve **güvenilirdir (Reliable)**.
  * Kaynak ve hedef arasında **sanal bir yol** oluşturur; bir mesaja ait tüm segmentler bu sanal yol üzerinden gönderilir.
  * **Hata kontrolü**, **akış kontrolü** ve **tıkanıklık kontrolü** mekanizmalarını barındırır.
  * Her bağlantıda aktarılan veri baytları **rastgele oluşturulmuş bir numara (ISN)** ile başlayarak TCP tarafından numaralandırılır:
    * **Sıra Numarası (`Sequence Number`):** O segmentte bulunan **ilk veri baytına** atanan sayıyı tanımlar.
    * **Onay Numarası (`Acknowledgment Number`):** Bir tarafın karşıdan **almayı beklediği bir sonraki bayt** sayısını tanımlar ve **kümülatif (birikimli)** bir değerdir.
* **Slayt 4 (İyi Bilinen TCP Port Numaraları Tablosu):**
  * `7`: Echo | `9`: Discard | `11`: Users | `13`: Daytime | `17`: Quote | `19`: Chargen
  * **`20 and 21`: FTP (Data and Control)** | **`23`: TELNET** | **`25`: SMTP** | **`53`: DNS** | **`67`: BOOTP** | `79`: Finger | **`80`: HTTP**
* **Slayt 5 (TCP Segment Başlığı = `20–60 Byte`):**
  * Sabit başlık **20 Byte**, opsiyonlarla (**0–40 Byte**) en fazla **60 Byte** olur.
  * **`HLEN` (4 bit):** Başlık uzunluğunu 4 baytlık kelimeler cinsinden tutar ($\text{HLEN} \in [5, 15] \Rightarrow 20\text{–}60\text{ Byte}$).
  * **6 Kontrol Bayrağı (6 bit):** `URG` (Acil işaretçi geçerli), `ACK` (Onay numarası geçerli), `PSH` (Tamponda bekletmeden aktar), `RST` (Bağlantıyı sıfırla), `SYN` (Sıra numaralarını senkronize et / bağlantı kur), `FIN` (Bağlantıyı sonlandır).
* **Slayt 6–7 (Akış Gönderimi ve Kapsülleme):** Gönderici ve alıcıda dairesel tamponlar (`Buffer`) bulunur. Uygulama verisi + `TCP header` = `TCP payload` $\rightarrow$ `IP header` eklendiğinde `IP payload` $\rightarrow$ `Frame header` eklendiğinde `Data-link layer payload` olur.

---

## 6.2. 3 Yollu El Sıkışma (3-Way Handshake): Kurulum, Veri Transferi ve Sonlandırma (PDF Sayfa 4–5, Slayt 8–10)
![TCP 3 Yollu El Sıkışma Bağlantı Kurulumu](assets/slides/h4_s8_3way_handshake.png)
![TCP Veri Transferi](assets/slides/h4_s9_veri_transferi.png)
![TCP Bağlantı Sonlandırma](assets/slides/h4_s10_baglanti_sonlandirma.png)

> [!IMPORTANT]
> **Sınavda `Seq` ve `Ack` Numarası Takibi Kuralları (Slayt 8, 9, 10):**
> * **1) Bağlantı Kurulumu (Slayt 8):**
>   * **Adım 1 (Client $\rightarrow$ Server):** `seq: 8000`, Bayrak: `SYN`. *(SYN segmenti veri taşımaz ama **1 sıra numarası tüketir!**)*
>   * **Adım 2 (Server $\rightarrow$ Client):** `seq: 15000`, `ack: 8001` ($8000 + 1$), Bayrak: `SYN + ACK`, `rwnd: 5000`.
>   * **Adım 3 (Client $\rightarrow$ Server):** `seq: 8000` *(Slayttaki not: `Means "no data"! seq: 8001 if piggybacking` — veri taşımayan saf ACK sıra numarası tüketmez!)*, `ack: 15001` ($15000 + 1$), Bayrak: `ACK`, `rwnd: 10000`.
> * **2) Veri Transferi (Slayt 9):**
>   * İstemci `seq: 8001, ack: 15001` ile `8001..9000` (1000B) ve `seq: 9001, ack: 15001` ile `9001..10000` (1000B) gönderir (`ACK + PSH`).
>   * Sunucu `seq: 15001, ack: 10001` ile hem 10000'e kadar olan baytları onaylar hem de kendi `15001..17000` (2000B) verisini gönderir.
>   * İstemci `seq: 10000, ack: 17001, rwnd: 10000` ile onaylar.
> * **3) Bağlantı Sonlandırma (Slayt 10):**
>   * İstemci `seq: x, ack: y` ile `FIN + ACK` gönderir $\rightarrow$ Sunucu `seq: y, ack: x + 1` ile `FIN + ACK` döner (*`FIN` bayrağı 1 sıra numarası tüketir*) $\rightarrow$ İstemci `seq: x, ack: y + 1` ile son `ACK` gönderir.

---

## 6.3. Zaman Çizelgesi, Durum Geçiş Şeması ve Bağlantı Red/İptal (`RST`) (PDF Sayfa 6–7, Slayt 11–13)
![TCP Zaman Çizelgesi](assets/slides/h4_s11_zaman_cizelgesi.png)
![TCP Durum Geçiş Şeması](assets/slides/h4_s12_durum_gecis.png)
![TCP Bağlantı Red ve İptal Etme](assets/slides/h4_s13_rst_iptal.png)

* **Slayt 11–12 (11 TCP Durumu ve Durum Geçiş Tablosu):**
  * `CLOSED`: Bağlantı yok.
  * `LISTEN`: Pasif açılış alındı; `SYN` bekleniyor.
  * `SYN-SENT`: `SYN` gönderildi; `ACK` bekleniyor.
  * `SYN-RCVD`: `SYN + ACK` gönderildi; `ACK` bekleniyor.
  * `ESTABLISHED`: Bağlantı kuruldu; veri aktarımı devam ediyor.
  * `FIN-WAIT-1`: İlk `FIN` gönderildi; `ACK` bekleniyor.
  * `FIN-WAIT-2`: İlk `FIN`'in `ACK` onayı alındı; karşıdan ikinci `FIN` bekleniyor.
  * `CLOSE-WAIT`: İlk `FIN` alındı, `ACK` gönderildi; uygulamanın bağlantıyı kapatması bekleniyor.
  * `TIME-WAIT`: İkinci `FIN` alındı, `ACK` gönderildi; **`2MSL` (Maksimum Segment Ömrünün 2 katı)** zaman aşımı bekleniyor.
  * `LAST-ACK`: İkinci `FIN` gönderildi; son `ACK` bekleniyor.
  * `CLOSING`: Her iki taraf aynı anda kapatmaya karar verdi (*Simultaneous close*).
* **Slayt 13 (Bağlantıları Red / İptal Etme — `RST`):**
  * **Bağlantı Red Etme (Sol Şema):** İstemci `SYN` gönderdiğinde sunucu portu kapalıysa sunucu **`RST`** göndererek bağlantıyı reddeder.
  * **Bağlantı İptal Etme (Sağ Şema):** `ESTABLISHED` durumundayken bir taraf normal `FIN` beklemek yerine **`RST + ACK`** göndererek bağlantıyı derhal sonlandırır (`Abort` $\rightarrow$ `CLOSED`).

---

## 6.4. Pencere Kavramı (`Send/Receive Window`) ve Akış Kontrolü (`rwnd`) (PDF Sayfa 7–8, Slayt 14–16)
![TCP Pencere Kavramı](assets/slides/h4_s14_pencere_kavrami.png)
![TCP Akış Kontrolü](assets/slides/h4_s15_akis_kontrolu.png)
![TCP Akış Kontrolü Örnek Uygulama](assets/slides/h4_s16_akis_ornek.png)

> [!TIP]
> **Pencere Duvarları ve Akış Kontrolü Sayısal Takibi (Slayt 14–16):**
> * **Slayt 14:** TCP çift yönlü iletişimde her yön için 2 (gönderme ve alma) olmak üzere **toplam 4 pencere** kullanır.
>   * **Pencere Kapanması (`Closing`):** Sol duvarın sağa hareket etmesi (gönderilen verilerin onaylanması / alınması).
>   * **Pencere Açılması (`Opening`):** Sağ duvarın sağa hareket etmesi (alıcı uygulamanın tampondan veri çekip boş yer açması).
>   * **Pencere Küçülmesi (`Shrinking`):** Sağ duvarın sola hareket etmesi (alıcı penceresinde izin verilmez).
> * **Slayt 16 (Örnek Uygulama Adım Adım `rwnd` Hesabı — Alıcı Tamponu = `800 Byte`):**
>   1. Bağlantı kurulurken sunucu `rwnd: 800` bildirir $\rightarrow$ İstemci penceresi `101..900` (`Size = 800`).
>   2. İstemci **`200 byte`** (`101..300`) gönderir $\rightarrow$ Sunucu tamponuna 200B girer, boş yer: $\text{rwnd} = 800 - 200 = \mathbf{600}$, `ackNo: 301` döner.
>   3. İstemci **`300 byte`** (`301..600`) gönderir $\rightarrow$ Sunucu 300B alır ve uygulama tampondan **100B okur (tüketir)** $\rightarrow$ Boş yer: $\text{rwnd} = 600 - 300 + 100 = \mathbf{400}$, `ackNo: 601` döner (`401..600` tamponda bekliyor).
>   4. Sunucu uygulaması kalan **200B'yi de okur** $\rightarrow$ Tampon tamamen boşalır, sunucu `ackNo: 601, rwnd: 800` göndererek pencereyi tekrar 800 bayta (`601..1400`) açar!

---

## 6.5. TCP Hata Kontrolü: ARQ Yöntemleri ve 4 Kayıp Senaryosu (PDF Sayfa 9–12, Slayt 17–24)
![ARQ Hata Kontrolü Yöntemleri](assets/slides/h4_s18_arq_yontemleri.png)
![Segment Kaybı Go-Back-N ARQ](assets/slides/h4_s20_gobackn.png)
![Segment Kaybı Selective Repeat](assets/slides/h4_s21_selective_repeat.png)
![Hızlı Yeniden İletim Fast Retransmit](assets/slides/h4_s22_fast_retransmit.png)
![Kayıp Onay Bildirimi](assets/slides/h4_s23_kayip_onay.png)
![Kayıp Segmentin Yeniden Gönderimi](assets/slides/h4_s24_kayip_segment.png)

* **Slayt 17–18 (Hata Denetimi ve ARQ):**
  * TCP'de hata denetimi **3 araç** ile sağlanır: **1) Checksum**, **2) Onay (`ACK`)**, **3) Zaman aşımı (`Timeout`)**.
  * Kaybolan veya bozulan paketlerin sezimi ve yeniden iletimi **ARQ (*Automatic Repeat Request*)** olarak adlandırılır: **Stop-and-Wait ARQ**, **Go-Back-N ARQ**, **Selective Repeat ARQ**.
* **Slayt 19–24 (4 Temel Hata Senaryosu):**
  1. **Segment Kaybı (`Go-Back-N` vs `Selective Repeat` — Slayt 20–21):**
     * **Go-Back-N (Slayt 20):** `Packet 2` kaybolduğunda, arkadan gelen `Packet 3, 4, 5` alıcı tarafından atılır ve alıcı sürekli `ACK 2` döner. `Packet 2` için zaman aşımı (`Timeout`) oluştuğunda gönderici **`Packets 2, 3, 4, 5`'in tamamını** baştan gönderir.
     * **Selective Repeat (Slayt 21):** `Seq: 701–800` kaybolduğunda, arkadan gelen `Seq: 801–900` atılmaz; alıcı tamponda **sırasız (*Out of order*)** olarak saklanır ve `Ack: 701` gönderilir. `RTO` süresi dolunca **yalnızca kaybolan `Seq: 701–800`** yeniden gönderilir; alıcı iki parçayı birleştirip kümülatif **`Ack: 901`** döner.
  2. **Hızlı Yeniden İletim (`Fast Retransmit` — Slayt 22):**
     * `Seq: 301–400` kaybolduğunda, arkadan gelen `401–500`, `501–600`, `601–700` segmentlerinin her biri için alıcı `Ack: 301` gönderir.
     * Gönderici `RTO` zamanlayıcısının dolmasını beklemeden **3 adet yinelenen onay (`First, Second, Third duplicate ACK = 301`)** alır almaz `Seq: 301–400` segmentini anında yeniden gönderir (`Fast retransmit`)!
  3. **Kayıp Onay Bildirimi (`Lost ACK` — Slayt 23):**
     * `Ack: 701` yolda kaybolsa bile, bir sonraki segmentin onayı olan **`Ack: 901`** kümülatif olduğu için gönderici `501–700` aralığının da ulaştığını anlar ve yeniden iletim yapmaz!
  4. **Kayıp Onay Sonrası Yeniden Gönderim (Slayt 24):**
     * `Ack: 701` kaybolur ve arkadan başka onay gelmeden `RTO` süresi dolarsa, gönderici `Seq: 501–600`'ü tekrar gönderir; alıcı bu baytları zaten aldığı için segmenti atar (**Rule 6**) ve tekrar `Ack: 701` gönderir.

---
## 6.6. Hafta 4 Değerlendirme Soruları (20 Soru & Çözümleri)

### Soru 1: TCP Süreçten Sürece İletişim ve Port Kavramı
**Soru:** Taşıma katmanında TCP protokolünün aynı bilgisayar üzerinde çalışan farklı uygulama süreçlerini (process) birbirinden ayırt etmek için kullandığı adresleme bilgisi nedir?  
- A) MAC Adresi (48 bit)  
- B) IP Adresi (32 bit)  
- C) Port Numarası (16 bit)  
- D) Sekans Numarası (32 bit)  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: C**  
**Açıklama (Hafta 4 PDF Sayfa 2, Slayt 3):** IP adresi bilgisayarı (host), Port numarası ise o bilgisayar içinde çalışan spesifik uygulama sürecini (process-to-process) tanımlar.
</details>

---

### Soru 2: İyi Bilinen TCP Port Eşleştirmesi
**Soru:** Slayt 4'te verilen iyi bilinen TCP port numaralarından FTP Data, FTP Control, TELNET ve HTTP için port numaraları sırasıyla hangileridir?  
- A) 20, 21, 23, 80  
- B) 21, 20, 25, 80  
- C) 20, 21, 53, 443  
- D) 23, 25, 80, 110  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: A**  
**Açıklama (Hafta 4 Slayt 4):**
* `20`: FTP Data
* `21`: FTP Control
* `23`: TELNET
* `25`: SMTP
* `53`: DNS
* `80`: HTTP
</details>

---

### Soru 3: Soket Adresi ve TCP 4-Tuple
**Soru:** Bir TCP bağlantısını küresel internet üzerinde benzersiz (unique) olarak tanımlayan 4'lü demet (4-tuple) hangi bileşenlerden oluşur?  
- A) Kaynak MAC, Hedef MAC, Tip, CRC  
- B) Kaynak IP, Kaynak Port, Hedef IP, Hedef Port  
- C) Sekans No, Ack No, Window Size, Checksum  
- D) İstemci IP, Sunucu IP, URL, Protokol  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (Hafta 4 Slayt 5):** $\text{Soket Adresi} = \text{IP Adresi} + \text{Port Numarası}$'dır. Çift yönlü bir TCP oturumu **Kaynak IP, Kaynak Port, Hedef IP, Hedef Port** kombinasyonu ile tekilleştirilir.
</details>

---

### Soru 4: Sıra Numarası ve Kümülatif Onay Mantığı
**Soru:** TCP segment başlığındaki Sıra Numarası (Sequence Number) ile Onay Numarası (Acknowledgment Number) alanları neyi ifade eder?  
- A) Seq: Paket sırasını (1, 2, 3); Ack: Toplam paket sayısını  
- B) Seq: O segmentteki ilk veri baytının numarasını; Ack: Karşı taraftan alınması beklenen bir sonraki baytın numarasını (kümülatif)  
- C) Seq: Port numarasını; Ack: Pencere boyutunu  
- D) Seq: Gönderilen bayt sayısını; Ack: Alınan son baytın numarasını  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (Hafta 4 Slayt 3 & 5):** TCP bayt akışı tabanlıdır. `Seq` segmentteki ilk baytın numarasıdır. `Ack` ise karşı tarafa "bu numaraya kadar olan tüm baytları eksiksiz aldım, şimdi senden bu numaralı baytı bekliyorum" mesajını iletir (**kümülatif onay**).
</details>

---

### Soru 5: TCP Başlık Boyutu ve HLEN Alanı
**Soru:** Bir TCP segment başlığında HLEN (Header Length) alanı `1000` (ikili) yani ondalık `8` değerini taşımaktadır. Bu TCP başlığının toplam boyutu kaç bayttır ve kaç bayt opsiyon içermektedir?  
- A) Toplam 32 bayt başlık, 12 bayt opsiyon  
- B) Toplam 20 bayt başlık, opsiyon yok  
- C) Toplam 8 bayt başlık, opsiyon yok  
- D) Toplam 40 bayt başlık, 20 bayt opsiyon  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: A**  
**Açıklama (Hafta 4 Slayt 5 & 7):** HLEN alanı 4 baytlık kelimeleri sayar. $\text{Başlık Boyutu} = 8 \times 4 = \mathbf{32\text{ Bayt}}$. Sabit başlık 20 bayt olduğuna göre opsiyon boyutu: $32 - 20 = \mathbf{12\text{ Bayt}}$ olur.
</details>

---

### Soru 6: TCP Kontrol Bayrakları (Flags)
**Soru:** Bir TCP segmentinde `RST` bayrağının `1` olması ile `PSH` bayrağının `1` olması sırasıyla ne anlama gelir?  
- A) Bağlantı kuruluyor; acil veri taşınıyor  
- B) Bağlantı derhal sıfırlanıyor/kapatılıyor; veri tamponda bekletilmeden doğrudan uygulama katmanına iletiliyor  
- C) Bağlantı sonlandırılıyor; pencere boyutu sıfırlanıyor  
- D) Sıra numaraları eşitleniyor; paket düşürülüyor  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (Hafta 4 Slayt 8):**
* `RST (Reset)`: Bağlantıyı anormal şekilde derhal sonlandırır veya reddeder.
* `PSH (Push)`: Alıcı TCP'ye tamponun dolmasını beklemeden gelen baytları anında tüketici uygulamaya iletmesini söyler.
</details>

---

### Soru 7: TCP Checksum ve Sözde Başlık (Pseudoheader)
**Soru:** TCP başlığındaki Checksum hesaplanırken segment verilerine ek olarak neden IP katmanından 12 baytlık "Sözde Başlık" (Pseudoheader) eklenir?  
- A) IP başlığı şifreli olduğu için  
- B) Paketin yanlış bir IP adresine veya yanlış bir protokole teslim edilmediğini garanti altına almak için  
- C) TCP başlığını 64 bayta tamamlamak için  
- D) Yönlendiricilerin TCP paketlerini okumasını hızlandırmak için  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (Hafta 4 Slayt 9):** Sözde başlık Kaynak IP, Hedef IP, Protokol (6) ve TCP Uzunluk bilgilerini içerir. Böylece IP katmanında hedef IP veya protokol alanı bozulmuş bir paket alıcı TCP tarafından tespit edilip düşürülür.
</details>

---

### Soru 8: 3 Yollu El Sıkışmada Sıra Numarası Tüketimi
**Soru:** İstemci sunucuya bağlantı açmak için `seq: 8000, SYN` segmenti gönderdiğinde; bu SYN segmenti herhangi bir veri taşımadığı halde sunucunun döneceği `ack` numarası neden `8001` olur?  
- A) TCP'de tüm baytlar 1'den başladığı için  
- B) `SYN` kontrol bayrağı, bağlantı kurulumunu garanti etmek ve sahte paketleri önlemek için mantıksal olarak **1 sıra numarası tüketir**  
- C) Sunucu istemcinin sekans numarasını beğenmediği için  
- D) Hata kontrolü için 1 eklenir  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (Hafta 4 Slayt 8 & 10):** Kural: Veri taşımayan `SYN` ve `FIN` segmentleri mantıksal olarak **1 sıra numarası tüketir**. Bu yüzden sunucu $8000 + 1 = \mathbf{8001}$ numaralı baytı onaylar.
</details>

---

### Soru 9: Saf ACK Segmentinin Sıra Numarası Tüketimi
**Soru:** 3 Yollu El Sıkışmanın 3. adımında istemcinin sunucuya gönderdiği veri içermeyen saf `ACK` segmenti sıra numarası tüketir mi?  
- A) Evet, 1 sıra numarası tüketir  
- B) Hayır; veri taşımayan saf ACK segmentleri sıra numarası **tüketmez**  
- C) Evet, pencere boyutu kadar tüketir  
- D) Yalnızca bağlantı kapanırken tüketir  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (Hafta 4 Slayt 8):** Slayt 8'deki alt notta açıkça belirtilmiştir: `Means "no data"! seq: 8001 if piggybacking`. Veri taşımayan saf ACK segmentleri sıra numarası tüketmez; bir sonraki veri paketi yine aynı sıra numarasıyla başlar.
</details>

---

### Soru 10: Piggybacking (Sırtlama) Tekniği
**Soru:** TCP veri transferinde "Piggybacking" (Sırtlama) kavramı neyi ifade eder?  
- A) Bir paketin arkasına birden fazla IP başlığı eklenmesi  
- B) Alınan verilere ait onay numarasının (ACK), karşı tarafa gönderilecek veri segmentinin içine yerleştirilerek tek bir segment halinde iletilmesi  
- C) Verilerin sıkıştırılarak gönderilmesi  
- D) Ağ kartının çift yönlü çalışması  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (Hafta 4 Slayt 9):** Sunucu istemciden veri aldığında ayrı bir boş ACK segmenti göndermek yerine, istemciye göndereceği kendi veri segmentinin `Acknowledgment Number` alanına bu onayı iliştirir. Buna sırtlama (piggybacking) denir ve ağ trafiğini azaltır.
</details>

---

### Soru 11: TCP Yarım Kapanma (Half-Close)
**Soru:** TCP bağlantı sonlandırma sürecinde "Yarım Kapanma" (Half-Close) durumu oluştuğunda ne gerçekleşir?  
- A) Bağlantı her iki taraf için de anında kopar  
- B) İstemci `FIN` göndererek kendi gönderme yönünü kapatır ancak sunucu elindeki verileri istemciye göndermeye devam edebilir; istemci bu verileri almaya devam eder  
- C) Sadece sunucu veri gönderebilir, istemci çöker  
- D) Paketler UDP üzerinden iletilir  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (Hafta 4 Slayt 10 & 14):** TCP çift yönlüdür. Bir tarafın veri gönderimi bitince `FIN` yollar (`FIN-WAIT-1`). Karşı taraf `ACK` döner (`CLOSE-WAIT`). Bu durumda istemci artık veri gönderemez ama karşı tarafın göndereceği verileri `FIN` gelene kadar kabul etmeye devam eder.
</details>

---

### Soru 12: Durum Geçiş Şeması: LISTEN $\rightarrow$ SYN-RCVD
**Soru:** Sunucu tarafında `LISTEN` durumunda bekleyen bir TCP soketi istemciden bir `SYN` paketi aldığında `SYN + ACK` göndererek hangi bağlantı durumuna geçer?  
- A) `ESTABLISHED`  
- B) `SYN-SENT`  
- C) `SYN-RCVD`  
- D) `CLOSE-WAIT`  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: C**  
**Açıklama (Hafta 4 Slayt 11 & 12):** Sunucu pasif dinlemedeyken (`LISTEN`) gelen `SYN` isteğini kabul edip `SYN+ACK` yolladığında **`SYN-RCVD`** durumuna geçer. İstemciden son `ACK` geldiğinde ise **`ESTABLISHED`** olur.
</details>

---

### Soru 13: `TIME-WAIT` Durumu ve `2MSL` Bekleme Süresi
**Soru:** Aktif kapatma yapan taraf (Client) son `ACK` paketini gönderdikten sonra neden hemen `CLOSED` durumuna geçmez ve `TIME-WAIT` durumunda `2MSL` (Maximum Segment Lifetime'ın 2 katı) kadar bekler?  
- A) İşletim sistemi belleğini temizlemek için  
- B) Gönderdiği son ACK kaybolursa sunucunun yeniden ileteceği FIN paketini alıp tekrar ACK dönebilmek ve ağda geciken eski paketlerin yeni açılacak bağlantıya karışmasını önlemek için  
- C) Sunucunun onay vermesini beklemek için  
- D) DNS önbelleğini boşaltmak için  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (Hafta 4 Slayt 11, 12, 16):** Eğer son ACK yolda kaybolursa sunucu `LAST-ACK` durumunda takılı kalır ve FIN'i tekrar yollar. İstemci `2MSL` (genelde 1-2 dakika) boyunca `TIME-WAIT`'te bekleyerek bu FIN'i yakalar ve yeniden ACK göndererek sunucunun temiz kapanmasını sağlar.
</details>

---

### Soru 14: Kapalı Porta Bağlantı İsteği ve `RST`
**Soru:** Bir istemci, üzerinde herhangi bir sunucu uygulamasının dinleme yapmadığı kapalı bir porta `SYN` paketi gönderdiğinde hedef işletim sistemi nasıl yanıt verir?  
- A) Paketi sessizce düşürür  
- B) `RST` (Reset) bayraklı bir segment göndererek bağlantı isteğini derhal reddeder  
- C) `FIN` paketi gönderir  
- D) Portu otomatik olarak açar  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (Hafta 4 Slayt 13):** Slayt 13'teki "Bağlantı Red Etme" şemasına göre port kapalıysa sunucu TCP katmanı istemciye **`RST`** paketi döndürerek portun kapalı olduğunu ve bağlantının reddedildiğini bildirir.
</details>

---

### Soru 15: TCP'de Çift Yönlü İletişim ve Pencere Sayısı
**Soru:** Çift yönlü (full-duplex) çalışan bir TCP bağlantısında her iki tarafın veri alışverişini yönetmek için toplam kaç adet pencere (window) yapısı kullanılır?  
- A) 1  
- B) 2  
- C) 4 (Her iki taraf için 1 Gönderme ve 1 Alma penceresi)  
- D) 8  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: C**  
**Açıklama (Hafta 4 Slayt 14):** Slayt 14: *"TCP, veri aktarımının her yönü için iki pencere (gönderme penceresi ve alma penceresi) kullanır; bu, çift yönlü iletişim için dört pencere anlamına gelir."*
</details>

---

### Soru 16: Alıcı Penceresi (`rwnd`) Hesaplama Formülü
**Soru:** TCP akış kontrolünde alıcının göndericiye bildirdiği Alıcı Penceresi boyutu (`rwnd`) hangi formülle hesaplanır?  
- A) $\text{rwnd} = \text{MSS} \times 2$  
- B) $\text{rwnd} = \text{Toplam Tampon Boyutu} - \text{Tamponda Tüketilmeyi Bekleyen (Okunmamış) Veri Miktarı}$  
- C) $\text{rwnd} = \text{Sekans No} + \text{Ack No}$  
- D) $\text{rwnd} = \text{Bant Genişliği} \times \text{RTT}$  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (Hafta 4 Slayt 14, 15, 16):** Alıcı tamponundaki boş alan göndericiye bildirilir. Boş alan kalmadığında $\text{rwnd} = 0$ olur ve gönderici veri göndermeyi durdurur (kilitlenme engellenir).
</details>

---

### Soru 17: Sayısal Akış Kontrolü Örneği
**Soru (Slayt 16 Örneği):** Alıcı tamponu 800 bayt olarak belirlenmiştir. İstemci 200 bayt veri gönderir. Alıcı bu 200 baytı tamponuna alır fakat alıcı uygulama tampondan **hiçbir veri okumamıştır**. Alıcının göndereceği onay segmentindeki yeni `rwnd` değeri kaç bayttır?  
- A) 800 Bayt  
- B) 600 Bayt  
- C) 400 Bayt  
- D) 0 Bayt  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (Hafta 4 Slayt 16):**
$$\text{Yeni rwnd} = \text{Toplam Tampon (800)} - \text{Bekleyen Veri (200)} = \mathbf{600\text{ Bayt}}$$
Alıcı `ackNo: 201, rwnd: 600` döner.
</details>

---

### Soru 18: Go-Back-N ile Selective Repeat ARQ Ayrımı
**Soru:** Hata kontrolünde `Go-Back-N ARQ` ile `Selective Repeat ARQ` yöntemleri arasındaki en belirgin fark nedir?  
- A) Go-Back-N TCP'de hiç kullanılmaz  
- B) Go-Back-N'de kaybolan paketten sonra gelen sağlam paketler de atılır ve hepsi baştan gönderilir; Selective Repeat'te ise gelen sağlam paketler alıcı tamponda tutulur ve yalnızca kaybolan paket yeniden iletilir  
- C) Selective Repeat onay numarası kullanmaz  
- D) Go-Back-N daha hızlıdır  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (Hafta 4 Slayt 20 & 21):**
* **Go-Back-N (Slayt 20):** Paket 2 kaybolunca sonraki 3, 4, 5 paketleri atılır; zaman aşımında 2, 3, 4, 5 hepsi tekrar yollanır.
* **Selective Repeat (Slayt 21):** Paket kaybolunca sonrakiler sırasız (out of order) tamponlanır; zaman aşımında yalnızca kaybolan paket yeniden yollanır.
</details>

---

### Soru 19: Hızlı Yeniden İletim (Fast Retransmit) Kuralı
**Soru:** TCP'de "Hızlı Yeniden İletim" (Fast Retransmit) mekanizması, RTO zamanlayıcısının süresinin dolmasını beklemeden kayıp segmenti yeniden göndermek için hangi olayın gerçekleşmesini şart koşar?  
- A) Sunucudan RST paketi gelmesi  
- B) Göndericinin arka arkaya **3 adet yinelenen onay (3 Duplicate ACKs)** alması  
- C) Alıcı penceresinin sıfırlanması  
- D) RTT süresinin 1 saniyeyi aşması  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (Hafta 4 Slayt 22):** Alıcı aradaki bir paket kaybolduğunda, sonraki gelen her segment için eksik olan ilk baytı isteyen mükerrer ACK yollar. Gönderici **3 adet yinelenen ACK** aldığında paketin yolda kaybolduğunu kesinleştirir ve zamanlayıcıyı beklemeden paketi anında yeniden basar (**Fast Retransmit**).
</details>

---

### Soru 20: Kayıp Onay (Lost ACK) Durumu
**Soru:** Gönderici 501–700 aralığını göndermiş ve alıcı `Ack: 701` üretmiştir ancak bu onay paketi yolda kaybolmuştur. Hemen ardından alıcı 701–900 segmentini de alıp `Ack: 901` gönderdiğinde gönderici tarafında neden yeniden iletim (retransmit) yapılmaz?  
- A) Alıcı bağlantıyı kapattığı için  
- B) TCP onay numaraları **kümülatif (birikimli)** olduğu için; `Ack: 901` onayı 900'e kadar olan tüm önceki baytların da eksiksiz alındığını garanti eder  
- C) Gönderici kaybolan onayı önemsemediği için  
- D) Çekirdek seviyesinde bayrak silindiği için  

<details>
<summary><b>💡 Çözümü ve Açıklamayı Gör</b></summary>

**Doğru Cevap: B**  
**Açıklama (Hafta 4 Slayt 23):** Kümülatif onay özelliği sayesinde aradaki münferit bir ACK paketi düşse dahi, arkasından gelen daha büyük numaralı bir ACK paketi önceki tüm baytların başarıyla ulaştığını doğrulamış olur.
</details>

---

# 6. Ders (Bölüm 2): Hafta 4 – Katman 4: TCP Tıkanıklık Kontrolü, 4 Zamanlayıcı, RTT/RTO Hesabı ve UDP
*(Bu bölüm bir sonraki çalışma adımımızda buraya eklenecektir)*

---

# 7. Ders: Hafta 5 – Soket Programlama (C, Java ve Endianness)
*(Bu bölüm bir sonraki çalışma adımımızda buraya eklenecektir)*

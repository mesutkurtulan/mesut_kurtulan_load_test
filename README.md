# JMeter Test Plan -- Modanisa Search

Bu proje, **Apache JMeter** kullanılarak hazırlanmış basit bir test
planı içerir. Testin amacı, `www.modanisa.com` üzerinde arama
fonksiyonunu yük testi altında doğrulamaktır.

## 📂 İçerik

-   **Test Planı**: `search_test_plan.jmx`\
-   **Veri Kaynağı (CSV)**: `src/test/jmeter/search.csv`

## ⚙️ Test Plan Detayları

-   **Thread Group**
    -   Kullanıcı sayısı: `1`
    -   Ramp-up süresi: `10` saniye
    -   Döngü sayısı: `5`
-   **HTTP Defaults**
    -   Domain: `www.modanisa.com`
    -   Protocol: `https`
    -   Implementation: `HttpClient4`
-   **HTTP Request**
    -   Path: `/search`
    -   Method: `GET`
    -   Parametre: `q=${searchString}` (CSV dosyasından alınır)
    -   Headers:
        -   `User-Agent: Mozilla/5.0`
-   **CSV Data Set Config**
    -   Dosya: `src/test/jmeter/search.csv`
    -   Değişken adı: `searchString`
    -   Döngü: Tekrar etmiyor (`recycle=false`)
    -   Eğer satır biterse thread sonlandırılır (`stopThread=true`)
-   **Constant Timer**
    -   Her istek arasında: `3000 ms` bekleme
-   **View Results Tree**
    -   Test sonuçlarını incelemek için eklenmiştir.

## ▶️ Çalıştırma

1.  **JMeter'ı indir ve kur**:\
    [Apache JMeter](https://jmeter.apache.org/download_jmeter.cgi)

2.  **Proje klasörüne git** ve `.jmx` dosyasını aç:

    ``` bash
    jmeter -t search_test_plan.jmx
    ```

3.  `src/test/jmeter/search.csv` dosyasında örnek arama kelimelerini
    gir:

    ``` csv
    elbise
    eşarp
    çanta
    ayakkabı
    ```

4.  Testi başlat ve sonuçları **View Results Tree** üzerinden veya `jtl`
    çıktılarıyla incele.

## 📝 Notlar

-   Test, sadece **1 kullanıcı** ve **5 döngü** için tasarlanmıştır.
    Gerçek yük testi için `Thread Group` ayarları güncellenebilir.\
-   `Constant Timer` değerini artırarak veya azaltarak istekler arası
    bekleme süresini değiştirebilirsiniz.\
-   `CSV Data Set Config` sayesinde farklı arama terimleriyle gerçekçi
    senaryolar oluşturabilirsiniz.

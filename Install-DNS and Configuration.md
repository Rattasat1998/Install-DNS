# การติดตั้ง Domain name server

### DNS Server คืออะไร ?
#### DNS server ย่อมาจาก Domain Name System server คือเครื่องบริการแปลงชื่อเว็บเป็นหมายเลข IP
ก่อนที่จะเริ่มเรามาดูว่า DNS Server ทำหน้าที่อะไรก่อนนะครับ แล้วก็ต้องบอกเลยครับว่า DNS ทำหน้าที่คล้ายกับสมุดสั่งอาหาร เมื่อเราต้องการสั่งอะไรเราก็ต้องเปิดดูรายการอาหารเพื่อสั่งอาหาร computer เช่น กัน
 เมื่อต้องการสื่อสารกับคอมพิวเตอร์เครื่องอื่น เครื่องนั้นก็จะทำการสอบถามหมายเลข IP ของเครื่องที่ต้องการสื่อสารด้วยกับ DNS server ซึ่งจะทำการค้นหาหมายเลขดังกล่าวในฐานข้อมูลแล้วแจ้งให้โฮสต์ดังกล่าว ทราบ

### ระบบ DNS แบ่งออกเป็น 3 ส่วนคือ

1.	Name Resolvers 
     หลักของ DNS คือการแปลงชื่อคอมพิวเตอร์ ให้เป็นหมายเลข IP ในเทอมของ DNS แล้วเครื่องไคลเอนท์ที่ต้องการสอบถามหมายเลข IP จะเรียกว่า  รีโซล์ฟเวอร์ (resolver)
2.	Domain Name Space
     เป็นฐานข้อมูลของ DNS ซึ่งมีโครงสร้างเป็น Tree หรือเป็นลำดับชั้น แต่ละโหนดคือ โดเมนโดยสามารถมีโดเมนย่อย (Sub Domain) ซึ่งจะใช้จุดในการแบ่งแยก 
3.	Name Servers
     คือเครื่องคอมพิวเตอร์ที่รันโปรแกรมที่จัดการฐานข้อมูลบางส่วนของระบบ DNS เนมเซิร์ฟเวอร์จะตอบกลับการร้องขอทันทีโดยการค้นหาข้อมูลในฐานของมูลตัวเอง หรือจะส่งต่อการร้องขอ ไปยังเนมเซิร์ฟเวอร์อื่น ถ้าเนมเซิร์ฟเวอร์มีเร็คคอร์ดของส่วนของโดเมน แสดงว่า เนมเซิร์ฟเวอร์นั้นเป็นเจ้าของโดเมนนั้น (Authoritative) ถ้าไม่มีก็จะเรียกว่า Non-Authoritative

ก่อนที่เราจะติดตั้ง DNS Server สิ่งที่ต้องมี
1.	DNS server in Ubuntu 16.04 LTS
2.	VM Visualbox
DNS server in Ubuntu 16.04 LTS สามารถโหลดได้ที่
http://releases.ubuntu.com/16.04/

![GitHub Logo](https://lh3.googleusercontent.com/OHYFRiU01cSQWOYvIFAFUVkEhyPOANQ5_IUqpNkAIkfbYljBkF1ap28TOMPokF7ea0ABiEz9yflJicU2mBV5CB4eQjM8GY2L8vcHMx73Z-t2cUGKDS6KcMoUjVu0FljKf7lB0wuT7euBUMKZ1qWbjvE-rbxoDdPz1hoXhfE8mr6MTWpKPpCAAaNgI7JDs2SsxwIUo1KVO_bjg9d8GsVmwFgifkTF47jJzHqC5RN-qvIDbIeLH70j7VDqZi5cylhNrEuBWJBug9m2jAe4IDH3YscnYSa5T-qTcMzumfClHha7A8483i0y0f3iq9S2A4ZzMboFp1lVLw8w6uDYyjmmBv0U8ZFmWV36SfHTNUuXNRI3YUlv-zuwgg2ShcxK5EqOOsYrPeVBjxMbsXOpAEo7mf967rVIbWauLu779ypXZ7c2EFkgmmTOjuUtBxK1Ydl4ITfpVv4HU5s4H5xImv4gH-PFb7PMGEtjKb4Lqfy4kPgpoSKS2rQzVDPrKrbnMaw5GARrpoGw4uTga-VpVKnlwJ50O3lJEKghtGTojgQnlyw7j3x0Tri-fb-mOVQ-RGAuYydUxIyKwFZ36ztJZi1gyLJC1jQVI6Z_UlT9XaUon3zJEUOExxto9S1htx4kimNwIBLjdXBlanLak5Q6xQK7IV44ZdIMqmE=w959-h724-no)
เลือก Server install image แบบ 64-bit PC (AMD64) Server install image

STEP 1 : อัพเดทระบบ โดยใช้คำสั่ง 

    $ sudo apt-get update
    $ sudo apt-get upgrade
    $ sudo apt-get dist-upgrade

![GitHub Logo](https://lh3.googleusercontent.com/fUVQNragsgABJvL3Yg0Gr7KOsDbRb6-9LSVlH5151xjXQ4TJwnXA8ig9n_4kW5BqQmJi241ajc-UNekxkmoOH_ftZW0UI4a1QNBAfCBKbdXaaaQRxPLXPb51nGC3LWVPBV_oTY2kjEdCvNs2-cRVQFUHpulraaJshp5e_HKyjMC5aewapEmmHPryTzUWrI3tMcE8xyyBiw67nRtpitYailEk6lTo4BuEQmzUd6zxuIRbHMnUwRjP3wDA5HOvLZJWkUwONng5YjKYWKTYiKWG7WRlZrtAiQOvlZmZY93oDyHiSxCVU7y5Zaoxrvo-pFInN54vpwfb4-RaGNJKZQlMdsie8KPk_nuwKNg3QG_lPukt-EUzKv4xtqVX8YuoFtoAO2O7Ss-59yTThbKrA6JI7exN3P7WH1oocuR619e-nTa9y43em8AVlZUcWpJAeCVDEiAd4ePXFHzzyIMzJQ5Ru0VVrpb518oqkcsbQBsb-QXSwCCPXpJbmlc1bqP5d3MOjSaLZrM2UjSo7O5WKKBGcFo18x4b7dVjkBvRwF5JgUlNrYkQajMLLru33_fj5ObUk50iCdYG4xjC2Dua-IOl75B1QbfhXFrSNoWnAkDnuOiXKPPlixfEDWwKhHvtGWZ-ni8gJ0_ZOl9rfa8DYgVDVhX5nASGLX0=w792-h594-no)

เมื่อเสร็จจะขึ้นดังรูป

### 2. ติดตั้ง BIND9 โดยใช้คำสั่ง
โดยใช้คำสั่ง

    $ sudo apt-get install bind9 bind9utils bind9-doc

![GitHub Logo](https://lh3.googleusercontent.com/JI61W-ZhxxyEA6Kfjn3Ad8UJaj0HB7l70af908dJMzSubjSHLE1W1MFAeblpyTZGoKexR8ZiaeXkPLRiJbkwjUJBWhiuoLchQl3qFWXIOTY_OuRiQcuMB35DxAxccDzI6FB3PelJJEqdcVjNoS1Pgfz7Ue0T00D6LYqehnK9XRwrC-ZE5Mhlat1ABbY3VfiWZSAIBGEGrkcXED-Y7PLMF8o9w1sq0mauANuHNntUwkWzmRyglZaY5uY6xigyyxW9W80KwU5MF8dC6-_HwnxtJoSnPtgzLOedapOcFcseTnz1ARlfHl2BP91boM4mdc3HSFmnUSDlDeOV8eXbNfY2_DGTBmvZSoGStbL6Ftx75ZNin1xzUC12sKFZn-JsxRAB5yuj-L2RfilZx3U71wF5kHk6CtRztJczsZPWkYX3TYK7OiG5SF2c53flVSUOzgQX-q137C1_-ILIV6-kuvC2mDatMAOE0_orfpqtr8t5b07XZXncMAo2yf5f6d1pgMkiAJrrbxWpHh6e3kJfSWuWwMf8HE--Xrt5g-PJuDXAddYIdbz6tLJp9CFFEHRX-yxzui7jn1w0wGVkNNHBZBF386zlYwaCT6oABuNUZ2hgwKHDWRsQDSYO2a11rAQB4Uumdb4WDm7Pi9-j2Th9H4oAdYsVrbTCSpg=w674-h125-no)


### STEP 2 : Install and configure Primary DNS server
1.ไปที่ /etc/bind/named.conf.default-zones แล้วแก้ไขตามนี้

    $ sudo nano /etc/bind/named.conf.default-zones

![GitHub Logo](https://lh3.googleusercontent.com/IFuxNxy3W_S_7h4YG5aGKf3R6HPQZvl2AK4folJ1G-ZSrdrQ6V7lq8UHNmvwpHvYD-t786cJoS_aA35oJoz8owHAzu__MxVZSsSDufxLt0WDTqgimBszzdy_9OroiymwG17gUULsBXNzCJxvbH3cUXxQYXmnUxRrSMUCR7Jo-fOe2DaAogI4Ui3YFfiiGNyUU5CNapqwkyKWYCyTQIjaq6u_XpFtdSuY-NtArKCJNxu5BCJwWUqQA2evQ9IcjtgNk3ZAbZO4aRoAVc0Oc8aJsfuXWyDUMwYrvUXtqDzX_zUfi42vDcBWyge5s0rYKZhs3qvIlxhk7RhYnx1hJTCuh55i1Vs3dXdEGKzsWgZCbjynp8yjY6ccvsaiD2Go94cV-jXfGXLOVgJ09IaxHqP7hC1yZrsU2XUHsFIu3x6f2JOcjyKtMo_hhNki6FxX-cceEtETx9Ac-bTR1Vq072CGpLV23-CMbP6iJztaTtq4hvPV07Tu0_XHcpG_qCjVttboPuDj7_CZTnXCBZDpvgSE-Vg9vq5jogHjX3Y7BLb5I2q7OCbny1p-v8rOCwHqCpZ4CG7NXKB-Z9byCvlpwIEbBOYg3NykUh_F5A9rUabFrHNT6qGVCAGSS0CaG1lo8t0NRVBWFaty6MVyTwEAAKb_R3CnjAIAw6Q=w959-h477-no)

![GitHub Logo](https://lh3.googleusercontent.com/1vuZ1UcMmy5AWf7FdgqUU6-LZcxSElFkkRYxbidPNNkKBDGYxLt_n9xrSC2PbvKNzP-4yOCIqAYmDPLQHBNvLOsyaX-1LbgJ-cmS-OOV7sptWGzWch_A_tT7s4sjLMS2P5-FpXcBcmHRKuJtPG_YidEqmhRtAyetrLqu9EiARVlL1-_lraFLNC6S5MX8f_1RJ1AAdcKTRrnE2P-IobKY-kocn80s1fhRG3yt_DptZgDhtn3nFT6WgRuqEamrmOf8rqY_svZdu8BbelEdt7POSqM43wK_UxytP5e-U4GiHwHtssUdhg3xyV3z_ve3S9kpIhNGDWAB4liMEBPlC9IGORNo1y2PFu_fccfm8VEZ3V3zWO--RJMWhXK0Ol02xAMHT3rMahxdFRfdOXP4NnyzJFCILW1Opjes6G6bSIwZXdvNTJAMNRPmS5q8xlqmFRXsZFO3QwGrYhPN39XzfVjvQKtcgeLzmBnA9zxYBXIk7II-wFxcrSgUUtcylSp79KrNH3558y8pI6LFoWm639VLBzFjQ09UHV2yAdarHltAWIDl7LzthS3deqdmGPTZcocEfQvYmSHnf0kqxCsyKAtqz6k_N4xlx6cF4rscg4_0OsWC4YFDIiGkGQm_sLGPxuiYA02Hm4NleENxkuXuciAKk2FiwuJTDWE=w959-h765-no)

#### 2. แก้ไขไฟล์ .lan

    $ sudo cp db.local db.lan
    $ Sudo nano db.lan

![GitHub Logo](https://lh3.googleusercontent.com/q1hNOCtcVBBb0f6xVvWNgWHcGQH_5CfoaEdif1GWDrVMdS9L6_G7BH1P03G95Z5PeUFXJbxK9z5k_0pJzsXkqiDGcfiXgSosfRyWkYYgpuqmyVQWEkdkmbWvHR8GxTp4u7W8QCos9CONGhR3xisakCHjaSTbzn9mAvfIP-h17G5YGj1Du8xgMVWrGZorhTNM2Ft9VQdbMD-g6otOyZR6IY32jnctHceE06HPDfrbR8rLuoE-KAwOo8KVJ8L3NbX-dSopHm3nhujwQcPSwHgI6Ce3Ssq5s14jsU595IMjr5l6VRNnPu91sfAAaf5qTSVpWJz7X6NnOd0VonU0OGQEMdBtNtSUoVD5T-BBLhobXYKXG8Dx5MdYe9eEZ6vMZDBR29LPS-TaNNvT3kF0AzPt_0iN3DDdi5HVi7L_AXlX27U7kTzxIGEPBCecZ9uK6tJBehB4nIg79KoQvEOngzSeoXIxzLXO85EvvpqtX9n2xD6yDoHEyC9lHIxzca4JG0u6ZW8yGAeGi6PhRtEtooRlO4ibuSIP28q4FQedOWenyMmoKHEHossO-8r_vGC94SaxtJmRohN-FsB3OIZLybebEsz0uQLw7MAxXI8DkVP7_JirI0la3kQj_YrjyGrd85TuOKWJnZs7TqMmCNeIPYBqoh-5tLHNR4U=w780-h403-no)

#### เสร็จแล้วใช้คำสั่ง 

$ sudo service bind9 restart เพื่อ Restart

#### ใช้คำสั่ง 

    $ sudo service bind9 status เพื่อดูการทำงาน
![GitHub Logo](https://lh3.googleusercontent.com/2gFF5mZt55MP61lCpZiaME_Z-2jvAysQE826My0-dqFqcU9ookQar6X4PgpLhBCeVUyFfQ4rpanY7aCydwCcAHQNPw3hsGzDWGDoLhTX--kczdxRbOZDohzwAfUjwErgYy-DXvE3F9ihDs1aoOUgJXqQRmxyi7zzwpHqfPQGWlEE-aP9-95feEidMy5SBmukTOc7KwnRw1h15pGbyPJub-EhynLMhNRg-ZypXTB9U4lHoxFqS5VM6rzKhVVQf-B3AQk--ntV7_rFWUWFhOd8ZgoCc9okQFBI2__Iu8Muu79_rzaPzICjbI87VbiI7ZcoInf98E-STfOYtud9j7ml_iUzSyrS2OcsE2jGrQpTxZuAV4IeJIjmG65rv4Kha5xYHNDQOLKhel5H45_cmWQdUtcGeVU6RSu4djXV-SJgn4idAfZB5LGoWLVSYmEwvqrj9MTj6_rxrLTEE7hM4OKFv-pyZYy-56IG4KjIwNPKBPX-V_94CtVZAnFuNLiKvwK9NLysewCrhE6naKjRwQvr1erCz1y2K6hRP-cgw-DJHPEfZabguYbQ6S9ZtO759H_WtLWKxpbEIrX5eMKynJD6lxhEghLOdEAV15OMXgr9RRWEmbfaM6b2M6vLF9NDIm4lkb85Pp9KplcQQt6oqPaP9MajFbqXUVY=w929-h459-no)

#### 3. ตั้งค่าสิทธิ์ของไดเรกทอรี bind9
ด้วย 2 คำสั่งนี้

    $ sudo chmod -R 755 /etc/bind
    $ sudo chown -R bind:bind /etc/bind
#### 4. Check the DNS configuration files
ด้วย 2 คำสั่งนี้

   	$ sudo named-checkconf /etc/bind/named.conf
  	$ sudo named-checkconf /etc/bind/named.conf.local

ถ้าใช้คำสั่ง 2 คำสั่งนี้แล้วไม่ขึ้นอะไรแสดงว่าทำถูกแล้วจากนั้นตามด้วย

### STEP 3 : Testing

1.ไปที่ /etc/bind/named.conf.default-zones แล้วแก้ไขตามนี้

ใช้คำสั่ง 

    $ nslookup
    > server
    > rat.lan
    > www.google.com
    > www.facebook.com

![GitHub Logo](https://lh3.googleusercontent.com/qBy3OZr_ateiBV057G38CcyhNa9EoUazBlUL_PTLgx9-WQpSY8ZAq8RzPwbwjkjyoy9ByfeCva8Th_n3j7jZA2Xj4k6K-RxiAJwn1NN9GJPrYrpCLVJDqoPpeJ99pZxBuZau_Icjz24PhpwvCelf3jXNTFsR4k-Zd-B_hP1TZLw8feRNSILCThkI-eJuIiPwq3duwum95T7OoOqhb54uAYoC8PTFafeQ-nAVtZk5txh1KQLxwIzidqT6GTqSqOBm8EOmppkbsm282c1hJlWDvcjrYSmO9jh8yzC_g1zVsebSPoTgCnIUjBe3v0ZeT23XazwKGI8rtD2ZGmazoSon_KUTGc8c_8Z3S_edxAI7GELE8qGxFpyq9r-DHLU_VS1QUAF05wUY9PSBZsQSbkaqIpVaBU-0LfFwgJaCQxwcb8bVOz4yBI4y7XoHMTjBOOoXxdgMRCBkqN28Qy0mjlFZJLkYNjbAv0OsvWoNOnPbyR6jJz4A1yG4G-XZqJfBaeBRCNDY5UVck07aEPBngfjjamJmhvXKlhu-Ihtpdujs36W0RrxG3DQwjiHAs6TlLd9D_-C7S6-8A2od98g8n5cZEbnCFe6WH7qGZc1Rs7TGiIeba7WOnBvxUAFGRSsg1EKMiuHbAAtxpVFB8BnMvgVdhrK2o5Zwne8=w959-h769-no)


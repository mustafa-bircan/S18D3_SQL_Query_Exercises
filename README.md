# 📚 Kütüphane Bilgi Sistemi - SQL Sorgu Alıştırmaları

Bu proje, bir hastane bilgi sistemi örneği üzerinden **Spring Data JPA** ve **PostgreSQL** ile ilişkisel veri modelleme ve SQL sorguları geliştirme pratiği yapmanız için tasarlanmıştır.

## 🚀 Proje Hedefi

Bu alıştırma kapsamında temel hedef; ilişkili tablolarla veri tabanı şeması oluşturmak, veri bütünlüğünü sağlamak için **foreign key** ilişkileri kurmak ve SQL sorgularıyla bu veri yapısı üzerinde işlem yapmayı öğrenmektir.

---

## 🛠️ Kurulum

1. Bu repoyu **fork**’layın ve ardından kendi bilgisayarınıza **clone**’layın.
2. Spring Boot projesine PostgreSQL driver ve Spring Data JPA bağımlılıklarını ekleyin.
3. `application.properties` dosyasına aşağıdaki bilgileri **kendi veritabanı kullanıcı adı ve şifrenizle** doldurun:

```properties
spring.datasource.url=jdbc:postgresql://localhost:5432/YOUR_DATABASE_NAME
spring.datasource.username=YOUR_DB_USERNAME
spring.datasource.password=YOUR_DB_PASSWORD
spring.jpa.hibernate.ddl-auto=update




🧱 Oluşturulan Tablolar ve SQL Sorguları
Aşağıda her bir görev için oluşturulan SQL tabloları paylaşılmıştır.

1️⃣ Doctor Tablosu
CREATE TABLE doctor (
    id BIGINT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    name CHARACTER VARYING,
    surname CHARACTER VARYING,
    proficiency CHARACTER VARYING
);

2️⃣ Nurse Tablosu
CREATE TABLE nurse (
    id BIGINT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    name CHARACTER VARYING,
    surname CHARACTER VARYING,
    proficiency CHARACTER VARYING
);


3️⃣ Patient Tablosu
CREATE TABLE patient (
    id BIGINT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    name CHARACTER VARYING,
    surname CHARACTER VARYING,
    email CHARACTER VARYING,
    complaint TEXT
);


4️⃣ Surgery Tablosu (İlişkili Tablo)
CREATE TABLE surgery (
    id BIGINT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    nurse_id BIGINT,
    patient_id BIGINT,
    doctor_id BIGINT,
    CONSTRAINT fk_surgery_nurse FOREIGN KEY (nurse_id) REFERENCES nurse(id),
    CONSTRAINT fk_surgery_patient FOREIGN KEY (patient_id) REFERENCES patient(id),
    CONSTRAINT fk_surgery_doctor FOREIGN KEY (doctor_id) REFERENCES doctor(id)
);


5️⃣ Operation Tablosu (İlişkili Tablo)
CREATE TABLE operation (
    id BIGINT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    patient_id BIGINT,
    doctor_id BIGINT,
    CONSTRAINT fk_operation_patient FOREIGN KEY (patient_id) REFERENCES patient(id),
    CONSTRAINT fk_operation_doctor FOREIGN KEY (doctor_id) REFERENCES doctor(id)
);


📌 Notlar
BIGINT GENERATED ALWAYS AS IDENTITY PostgreSQL’de auto-increment özelliği sağlar.

Tablolardaki FOREIGN KEY tanımlamaları veri bütünlüğü açısından kritik öneme sahiptir.

Tüm tablolar, character varying türünde veri tipleri kullanılarak esnek hale getirilmiştir.

🤝 Katkı Sağlamak
Her katkı değerlidir. Fork’layın, geliştirin ve PR gönderin. Yeni sorgular ya da tablolar eklemek isterseniz issue açmanız yeterlidir.

🧑‍💻 Geliştirici
Mustafa - Senior Full Stack Developer


📝 Lisans
Bu proje eğitim amaçlıdır. Herhangi bir ticari amaçla kullanımı yasaktır.

---

Dilersen bu `README.md` dosyasını projenin kök dizinine koy ve GitHub'a pushla. Projene bakan biri, ne yaptığını anında çözer.

İstersen bonus olarak `Entity` sınıflarını da ekleyebiliriz. Hazırsan devam edelim mi?
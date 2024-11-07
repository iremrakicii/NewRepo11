# SQL Sorgu Örnekleri

Bu dosya, `actor` ve `customer` tabloları üzerinde farklı SQL sorguları içermektedir. Aşağıda her bir sorgunun amacı ve nasıl çalıştığı açıklanmıştır.

## 1. Soru

Bu sorgu, `actor` ve `customer` tablolarını `actor_id` ile `customer_id` alanlarına göre **FULL JOIN** yaparak birleştirir. Bu birleşim türü, her iki tablodan da eşleşen ve eşleşmeyen tüm kayıtları döndürür.

```sql
SELECT actor.first_name AS actor_first_name, customer.first_name AS customer_first_name
FROM actor
FULL JOIN customer ON actor.actor_id = customer.customer_id
ORDER BY actor_first_name, customer_first_name;
```
FULL JOIN kullanımı, her iki tabloda bulunmayan kayıtları da sonuç olarak döndürür.
actor.first_name ve customer.first_name sütunları sırasıyla actor_first_name ve customer_first_name olarak seçilir ve sonuçlar artan sırayla (ORDER BY) sıralanır.

### 2. Soru
Bu sorgu, actor ve customer tablolarını actor_id ve customer_id alanlarına göre INNER JOIN yaparak birleştirir. Bu birleşim türü, yalnızca her iki tabloda da eşleşen kayıtları döndürür.

```sql
SELECT actor.first_name AS actor_first_name, customer.first_name AS customer_first_name
FROM actor
INNER JOIN customer ON actor.actor_id = customer.customer_id
ORDER BY actor_first_name, customer_first_name;
```
INNER JOIN kullanımı, yalnızca her iki tabloda ortak olan kayıtları sonuç olarak döndürür.
Sonuç yine actor_first_name ve customer_first_name sütunları kullanılarak sıralanır.

### 3. Soru
Bu sorgu, actor tablosunda olup customer tablosunda olmayan kayıtları döndürmek için LEFT JOIN kullanır. Bu tür sorgular, bir tablodaki verilerin başka bir tabloda olup olmadığını kontrol etmek için idealdir.

```sql
SELECT actor.first_name
FROM actor
LEFT JOIN customer ON actor.actor_id = customer.customer_id
WHERE customer.customer_id IS NULL;
```
LEFT JOIN ile actor tablosundan tüm kayıtlar alınır ve customer tablosunda eşleşmeyen kayıtlar NULL ile döner.
WHERE customer.customer_id IS NULL ifadesi, yalnızca customer tablosunda olmayan actor kayıtlarını filtrelemek için kullanılır.

 ### Birleşim (UNION) Sorgusu
Bu sorgu, actor ve customer tablolarındaki first_name sütunlarını birleştirir. UNION komutu, her iki tablodaki benzersiz adları tek bir liste olarak döndürür.

```sql
SELECT first_name FROM actor
UNION
SELECT first_name FROM customer;
```
UNION komutu, yinelenen verileri tekilleştirir ve yalnızca benzersiz adları döndürür.

### Kesişim (INTERSECT) Sorgusu
Bu sorgu, her iki tabloda da ortak olan first_name değerlerini döndürür. INTERSECT komutu, sadece her iki sorguda da bulunan kayıtları getirir.

```sql
SELECT first_name FROM actor
INTERSECT
SELECT first_name FROM customer;
```
INTERSECT komutu, sadece her iki tabloda bulunan first_name değerlerini döndürür.

### Fark (EXCEPT) Sorgusu
Bu sorgu, actor tablosunda olup customer tablosunda olmayan first_name değerlerini döndürür. EXCEPT komutu, ilk sorguda olup ikinci sorguda olmayan verileri getirir.

```sql
SELECT first_name FROM actor
EXCEPT
SELECT first_name FROM customer;
```
EXCEPT komutu, yalnızca actor tablosunda bulunan ancak customer tablosunda olmayan first_name değerlerini döndürür.

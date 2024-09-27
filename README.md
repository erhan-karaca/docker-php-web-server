# Docker Web Server (Nginx + Multiple PHP)
Bu proje, yerel ortamda Nginx ve farklı PHP sürümlerinin çalıştırılmasını sağlar. Nginx, 89 numaralı portta çalışır ve hem PHP 7.4 hem de PHP 8.2 sürümlerini içerir.

## Kurulum
Kurulum için proje klasöründeki install klasöründe aşağıdaki komutu çalıştırın:
```
docker compose up -d
```

## Yeni web projesi oluşturma
Yeni bir domain eklemek için aşağıdaki komutları sırasıyla çalıştırın:
````
chmod +x add-domain.ssh
./add-domain.ssh
````

## Genel Bilgi
docker-compose.yml dosyasında hangi servislerin çalıştırılacağı ve isimleri tanımlanır.

phpfpm klasöründe, çalıştırılacak PHP sürümleri için Dockerfile dosyaları bulunmaktadır. Bu dosyalar, PHP versiyonlarının ve gerekli eklentilerin kurulmasını sağlar.

nginx klasöründe bulunan common.conf dosyası, varsayılan sunucu yolu ve kurallarını tanımlar.

conf.d klasöründeki default.conf dosyası, ilgili PHP sürümlerinin hangi konteynerde ve hangi portta çalıştığını belirler. Nginx, varsayılan 80 portuna gelen istekleri hangi klasöre yönlendireceğini ayarlayabilirsiniz.

conf.d klasöründe local.domain.conf isimli yeni konfigürasyon dosyaları oluşturabilirsiniz. Bu dosyalar, hangi domainin çalışacağı, hangi PHP sürümünün kullanılacağı ve hangi klasöre yönlendirileceğini belirler.

domain klasörü altında, public klasörü index dosyası için kullanılır ve bu yapı common.conf dosyasından düzenlenebilir.

docker-compose.yml dosyasında '../www' klasörü, konteyner içerisinde '/var/www' klasörüne bağlanmaktadır.

## Yeni php versiyonu kurulumu
Yeni bir PHP sürümü eklemek için, phpfpm klasöründe ilgili sürüm için yeni bir klasör oluşturun ve içerisine gerekli Dockerfile dosyasını yerleştirin. Diğer sürümlerin Dockerfile dosyasını kopyalayarak düzenleyebilirsiniz.

Yeni sürümü docker-compose.yml dosyasına bir servis olarak eklemeyi unutmayın. Sürümün Dockerfile dosyası ve mount işlemleri tanımlanmalı, konteyner adı belirlenmelidir.

nginx/conf.d klasöründeki default.conf dosyasında, oluşturduğunuz PHP sürümü için servis tanımını sunucu olarak ekleyin.
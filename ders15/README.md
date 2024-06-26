# Ders 15 - Golang ile Web Uygulamaları

Bu derste, Golang kullanarak basit bir web uygulaması geliştireceğiz. Golang'in güçlü ve verimli yapısını kullanarak nasıl web sunucusu oluşturabileceğimizi, HTTP isteklerini nasıl yöneteceğimizi ve temel web uygulaması bileşenlerini nasıl oluşturabileceğimizi öğreneceğiz.

## İçindekiler

1. [Giriş](#giriş)
2. [Golang Web Sunucusu Kurulumu](#golang-web-sunucusu-kurulumu)
3. [HTTP İsteklerini Yönetme](#http-isteklerini-yonetme)
4. [Temel Web Uygulaması Bileşenleri](#temel-web-uygulaması-bileşenleri)
5. [Örnek Proje](#örnek-proje)
6. [Sonuç](#sonuç)

## Giriş

Golang, yüksek performanslı ve verimli bir programlama dili olarak web geliştirme için ideal bir seçenektir. Bu derste, Golang kullanarak basit bir web sunucusu oluşturmayı ve HTTP isteklerini yönetmeyi öğreneceğiz.

## Golang Web Sunucusu Kurulumu

İlk olarak, Golang'i bilgisayarınıza kurmanız gerekmektedir. Golang'in resmi web sitesinden (https://golang.org) en son sürümü indirip kurabilirsiniz.

Kurulum tamamlandıktan sonra, aşağıdaki komutla Golang'in doğru kurulduğunu doğrulayabilirsiniz:

```sh
go version
```

## HTTP İsteklerini Yönetme

Golang'de HTTP isteklerini yönetmek için `net/http` paketini kullanacağız. Basit bir web sunucusu oluşturmak için aşağıdaki adımları izleyebilirsiniz:

```go
package main

import (
    "fmt"
    "net/http"
)

func handler(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintf(w, "Merhaba, Dünya!")
}

func main() {
    http.HandleFunc("/", handler)
    http.ListenAndServe(":8080", nil)
}
```

Yukarıdaki kod, `localhost:8080` adresinde çalışan basit bir web sunucusu oluşturur. Tarayıcınızda bu adresi ziyaret ettiğinizde "Merhaba, Dünya!" mesajını görmelisiniz.

## Temel Web Uygulaması Bileşenleri

Bir web uygulamasının temel bileşenleri şunlardır:

- **Router**: HTTP isteklerini belirli handler fonksiyonlarına yönlendirir.
- **Handler**: HTTP isteklerini işler ve yanıt döner.
- **Middleware**: İstekler ve yanıtlar üzerinde ek işlemler yapar.

Golang'de bu bileşenleri kullanarak daha karmaşık web uygulamaları geliştirebilirsiniz.

## Örnek Proje

Aşağıda, kullanıcıların kayıt olabileceği ve giriş yapabileceği basit bir web uygulaması örneği bulunmaktadır:

```go
package main

import (
    "fmt"
    "net/http"
)

func signupHandler(w http.ResponseWriter, r *http.Request) {
    if r.Method == "POST" {
        // Kullanıcı kayıt işlemleri
        fmt.Fprintf(w, "Kayıt başarılı!")
    } else {
        http.ServeFile(w, r, "signup.html")
    }
}

func loginHandler(w http.ResponseWriter, r *http.Request) {
    if r.Method == "POST" {
        // Kullanıcı giriş işlemleri
        fmt.Fprintf(w, "Giriş başarılı!")
    } else {
        http.ServeFile(w, r, "login.html")
    }
}

func main() {
    http.HandleFunc("/signup", signupHandler)
    http.HandleFunc("/login", loginHandler)
    http.ListenAndServe(":8080", nil)
}
```

Bu örnekte, `/signup` ve `/login` yolları için handler fonksiyonları tanımlanmıştır. Kullanıcılar bu yolları ziyaret ederek kayıt olabilir veya giriş yapabilirler.

## Bonus: Gin Kütüphanesi ile Web Uygulamaları

Gin, Golang için popüler ve performanslı bir web framework'üdür. Gin kullanarak daha hızlı ve daha kolay web uygulamaları geliştirebilirsiniz. Aşağıda, Gin kullanarak basit bir web sunucusu oluşturma adımları bulunmaktadır:

### Gin Kurulumu

Gin'i kurmak için aşağıdaki komutu kullanabilirsiniz:

```sh
go get -u github.com/gin-gonic/gin
```

### Basit Bir Gin Uygulaması

Aşağıda, Gin kullanarak basit bir web sunucusu oluşturma örneği bulunmaktadır:

```go
package main

import (
    "github.com/gin-gonic/gin"
)

func main() {
    r := gin.Default()
    r.GET("/ping", func(c *gin.Context) {
        c.JSON(200, gin.H{
            "message": "pong",
        })
    })
    r.Run() // varsayılan olarak ":8080" portunda çalışır
}
```

Bu kod, `localhost:8080/ping` adresinde çalışan basit bir web sunucusu oluşturur. Tarayıcınızda bu adresi ziyaret ettiğinizde `{"message": "pong"}` yanıtını görmelisiniz.

Gin, daha karmaşık web uygulamaları geliştirmek için birçok özellik sunar. Detaylı bilgi için [Gin belgelerine](https://github.com/gin-gonic/gin) göz atabilirsiniz.

## Sonuç

Bu derste, Golang kullanarak basit bir web uygulaması geliştirmeyi öğrendik. Golang'in güçlü ve verimli yapısını kullanarak daha karmaşık web uygulamaları geliştirebilirsiniz. İyi çalışmalar!

### Sonraki Ders

[# Ders 16 - Golang ile Veritabanı İşlemleri (Database Operations)](../ders16/README.md)
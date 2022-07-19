# Linux  İçin Sunucu Sıkılaştırması
## SSH Sunucusu
### SSH girişini root kullanıcısına kilitlemek

- İlk adım root hesabını ssh kullanımını kapatmak olacaktır.
```
sudo nano /etc/ssh/sshd_config
```
- PermitRootLogin satırı bulunur ve "no" olarak değiştirilir.
```
PermitRootLogin no
```
- Değişiklikler kaydedilir ve dosyadan çıkılır.

- Ssh sunucusu tekrar çalıştırılır.
```
sudo service ssh restart
```
### Default Port Adresini ve Giriş Deneme Sayısını Değiştirme
- Deafult olarak gelen 22 portunu istediğimiz herhangi bir port ile değiştirelim (kullanılan bir port olmaması gerekiyor.)
```
sudo nano /etc/ssh/sshd_config
```
```
Port 222
MaxAuthTries 5
```
MaxAuthTries 5 kez giriş isteğinde bulunup giriş yapamaz ise kicklenir. (isteğe bağlı olarak değiştirilebilir.)

 ### Kullanıcılara SSH Erişimini Kısıtlama
- sshd_config dosyasına 
```
AllowUsers <username> , <username2>
```
 yazılarak sadece ssh ile bağlantı kurmasını istediğiniz kullanıcıların adları girilir.


## Şifresiz protokollerin devre dışı bırakılması
- telnet, rlogin/rsh, FTP vb. Servisleri kullanmaktan kaçınabilirsiniz.
- Çoğu ağ yapılandırmasında, kullanıcı adları, parolalar, FTP, telnet, rsh komutları ve aktarılan dosyalar, bir paket dinleyicisi sayesinde hepsi yakalanabilir. Bu güncel olmayan yazılımların sorununun genel çözümü yazılımı silmek olabilir.
- Bunun için 
```
sudo apt-get --purge remove xinetd nis yp-tools tftpd atftpd tftpd-hpa telnetd rsh-server rsh-redone-server
```

## Gereksiz servisler
- dpkg veya apt gibi RPM paket yöneticileri kullanarak istenmeyen yazılımlar silinebilir.
```
dpkg --list 
```
- Güncellemesi bitmiş eski yazılımlar apt sayesinde otomatik silinir
```
sudo apt autoremove
```
## Linux Kernel ve Yazılımı Güncel Tutulması
- Güvenlik yamaları, linux sunucusu güvenliği için önemlidir. Bu güvenlik güncellemeleri en kısa sürede güncellenmelidir. Bu da yine paket yöneticileri sayesinde kolaylıkla yapılır.
```
sudo apt-get update && sudo apt-get upgrade
```

##  Grafik arayüz erişim protokolleri
- VNC, RDP vs.


# Log denetimi
## fail2ban
- Fail2Ban bir IPS (izinsiz giriş önleme sistemi) 'dir. Logları ve sistemi takip eder. Birden fazla başarısız oturum açma tespit ederse isteklerin geldiği IP adresini kara listeye alır.

- Fail2Ban'ı yüklemek için

```
sudo apt-get install fail2ban
```
- Şimdi yeni jail.local dosyası oluşturacağız. /etc/fail2ban klasöründe jail.conf dosyası bulunur, o dosyayı düzenlemeyeceğiz ve ona dokunmayacağız. jail.conf dosyasının bir kopyası alınacak 
```
sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
```
- Bu dosyayı kopyaladıktan sonra jail.local dosyası üzerinde tercihe bağlı olarak nano üzerinde görüntüleyip düzenlemeler yapılabilir. 
```
sudo nano /etc/fail2ban/jail.local
```
## logwatch
- logwatch komutunu kullanarak, sistem günlüğündeki olağandışı işlemler hakkında bilgi alırsınız. 
- İndirmek için; 
```
sudo apt install logwatch
logwatch
```

## faillog

- Oturum açma hatalarını görmek ve limitlerini belirlemek için "faillog"
kullanılabilir. Faillog, /var/log/faillog/database/log 

## rkhunter

- Sunucuda çeşitli kontroller yaparak rootkit,backdoor,local exploits,malware gibi güvenlik problemlerini tarama yapabileceğiniz bir güvenlik uygulamasıdır.

- Kurulumu için; 
```
sudo apt install rkhunter
```
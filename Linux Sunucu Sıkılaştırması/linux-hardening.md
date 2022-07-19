# Linux  İçin Sunucu Sıkılaştırması
# Uzaktan erişim
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

## Grafik arayüz erişim protokolleri
- VNC, RDP vs.

## Web üzerinden yönetim sistemleri
- webmin, vb.

# Gereksiz servisler
...
# Log denetimi
...
## fail2ban

...
## logwatch
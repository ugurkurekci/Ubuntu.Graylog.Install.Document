# UbuntuGraylog
The construction phase

sudo apt-get update && sudo apt-get upgrade
(Sistem güncellemelerini kontrol et varsa güncelle)
------------------------------------------------------
sudo apt-get install apt-transport-https openjdk-8-jre-headless uuid-runtime pwgen
(Java yükle)
---------------------------------------------------------------------------------

wget -qO – https://www.mongodb.org/static/pgp/server-5.0.asc | sudo apt-key add –
echo “deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/5.0 multiverse” | sudo tee /etc/apt/sources.list.d/mongodb-org-5.0.list
sudo apt-get update
sudo apt-get install -y mongodb-org
(MongoDB indir yükle  sistemi güncelle)

--------------------------------------------------
sudo systemctl enable mongod.service
sudo systemctl restart mongod.service
(MongoDB Servisi başlat)

sudo systemctl status mongod.service
(Mongo durumu bakılıyor activese sorun yok)

------------------------------------------------

wget -qO – https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add –
echo “deb https://artifacts.elastic.co/packages/7.x/apt stable main” | sudo tee /etc/apt/sources.list.d/elastic-7.x.list
sudo apt-get update
sudo apt-get install elasticsearch
(ElasticSearch indir yükle sistemi güncelle) 

-------------------------------------------------------------------

/etc/elasticsearch/elasticsearch.yml yoluna giderek dosyamızı nano ile açıyoruz ve cluster.name kısmını bulup graylog yazıyoruz.
Daha sonra aynı dosyanın en altına inerek action.auto_create_index: false komutunu ekliyoruz.

---------------------------------------------------------------------------------
 sudo systemctl daemon-reload
 sudo systemctl enable elasticsearch.service
 sudo systemctl restart elasticsearch.service
 (Elastic aktif edip çalıştırılır)
 
 sudo systemctl status elasticsearch.service
 (Elastic durumu bakılıyor activese sorun yok)
 ---------------------------------------------------------------
 
 wget https://packages.graylog2.org/repo/packages/graylog-4.2-repository_latest.deb
 sudo dpkg -i graylog-4.2-repository_latest.deb
 sudo apt-get update
 sudo apt-get install graylog-server graylog-enterprise-plugins graylog-integrations-plugins graylog-enterprise-integrations-plugins
 
 (Graylog indir yükle sistemi güncelle)
 
 -------------------------------------------------------------------------
 GRAYLOG CONFIG
 
 Parola koymak için: 
 apt-get install pwgen
 pwgen –N 1 –s 63
 echo –n sifrembu123 | sha256sum
 not (yeni sifre kodu):  echo -n “Enter Password: ” && head -1 </dev/stdin | tr -d ‘\n’ | sha256sum | cut -d” ” -f1
 
 /etc/graylog/server/server.conf
 paswword_secret , Root_Password_Sha2 , Root_TimeZone (Europe/Istanbul ) ,  Root_Email , Http_Bind_Address(web portal erişim ip örn:(192.168.1.150:9000)) , ElasticSearch_Shards(1), 
 ---------------------------------------
sudo systemctl daemon-reload
sudo systemctl enable graylog-server.service
sudo systemctl restart graylog-server.service
(Graylog servis aktif et çalıştır)
sudo systemctl –type=service –state=active | grep graylog
sudo systemctl status graylog-server.service
(Graylog durumu bakılıyor activese sorun yok)
------------------------------------------------
netstat –tuln
(servis portu kontrol)
----------------------------
http://192.168.1.107:9000/ 


<a href="https://sistemdostu.com/ubuntu-cihaza-graylog-kurulumu/">Kaynak</a>

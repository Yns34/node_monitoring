# Haqq Validatorünüz için node takip sistemi kurulumu

## Gereklilikler

### Node kurulu olan sistemde Validator için dış kaynak kurulumları
Öncelikle Validator düğümüne bazı gerekli şeyler kurmamız gerekecek. Bunun için aşağıdaki tek kodu girerek kurulum gerçekleştiriyoruz.
```
wget -O install_exporters.sh https://raw.githubusercontent.com/kj89/cosmos_node_monitoring/master/install_exporters.sh && chmod +x install_exporters.sh && ./install_exporters.sh
```
Token- aISLM   rpc_port: 26657 grpc_port: 9090  bunlara göre gerekli yerleri değiştiriniz ve gerekli izinleri veriniz. sed -i -e "s/prometheus = false/prometheus = true/" $HOME/.sei/config/config.toml

## Farklı makine üzerinde kurulum adımları

```
curl -fsSL https://get.docker.com -o get-docker.sh && sh get-docker.sh

docker_compose_version=$(wget -qO- https://api.github.com/repos/docker/compose/releases/latest | jq -r ".tag_name")

sudo wget -O /usr/bin/docker-compose "https://github.com/docker/compose/releases/download/${docker_compose_version}/docker-compose-`uname -s`-`uname -m`"

sudo chmod +x /usr/bin/docker-compose

```

### İzleme aracı kurulum

 https://telegram.me/getmyid_bot buraya gelerek bottan telegram Id'nizi öğrenin. Alt taraftaki kodlarda telegramID'nizi eşleştiriniz.

```
wget -O install_monitoring.sh https://raw.githubusercontent.com/kj89/cosmos_node_monitoring/master/install_monitoring.sh && chmod +x install_monitoring.sh && ./install_monitoring.sh
```
```
cp $HOME/cosmos_node_monitoring/config/.env.example $HOME/cosmos_node_monitoring/config/.env
```
```
vim $HOME/cosmos_node_monitoring/config/.env
```

```
echo "export $(xargs < $HOME/cosmos_node_monitoring/config/.env)" > $HOME/.bash_profile
source $HOME/.bash_profile
```

###  _prometheus_ configuration dosyasına validattör parametrelerinizi giriniz (`VALIDATOR_IP`, `VALOPER_ADDRESS`, `WALLET_ADDRESS` ve `PROJECT_NAME`)

```
$HOME/cosmos_node_monitoring/add_validator.sh VALIDATOR_IP VALOPER_ADDRESS WALLET_ADDRESS PROJECT_NAME
```

birden fazla validator bilgisi için bu kodu çalıştırabilirsiniz. cd $HOME/cosmos_node_monitoring && docker-compose up -d

## Grafanaya 9999 portu ile giriş yapıp, şifre belirleyerek id yazıp (başlangıçta verdiğin ile) ve  Prometheus data source seçerek  importlayarak yükleyin.(Bşalangıçta standart olarak Admin/Admin olarak giriş yapabilirsiniz.Daha sonra  kurulum alarmının izlenmesi için telegram bilgimizi kullanarak(ya da mail) -erişim ve bildirimleri yapılandırıyoruz.

https://telegram.me/botfather bota giriş yapıp /start - /newbot - herhangibirisim veriyoruz.  Grafana'yı yapılandırmak için HTTP API'yi not alıyoruz.



# Спринт 3

1. Заходим на сервер srv и клонируем репазиторий
```console
ssh ubuntu@51.250.88.220
git clone https://github.com/vggalkin/Monitoring.git
cd Monitoring
```
2. Создаем файл .env с данными для Telegram бота

![env_with_tejegram_bot_key](https://user-images.githubusercontent.com/3630798/197578928-e50683d4-5efc-4768-a9a5-3f5155afc2f7.png)

3. Меняем IP адрес и порт в файлах prometheus/prometheus.yaml и prometheus/alert.rules

prometheus.yaml
```yaml
static_configs:
  - targets:
    - http://178.154.225.218:30007
```
alert.rules
```
- alert: WrongResponse
    expr: probe_http_status_code{instance="http://178.154.225.218:30007", job="blackbox"} != 200
```
```
- alert: SlowResponse
    expr: probe_duration_seconds{instance="http://178.154.225.218:30007", job="blackbox"} > 5
```
4. Запускаем контейнеры
```console
sudo docker-compose up -d
```

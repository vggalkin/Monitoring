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
Результат

![image](https://user-images.githubusercontent.com/3630798/201343057-914ff935-6794-4540-9043-230e5445301b.png)

5. Telegram Bot

![image](https://user-images.githubusercontent.com/3630798/201358936-a0eea1ad-02b7-4ace-91c3-b976ce0db16d.png)

6. Grafana

![image](https://user-images.githubusercontent.com/3630798/201346877-f44f9214-3f45-4c2e-a66f-ec6f75c1cf74.png)

![image](https://user-images.githubusercontent.com/3630798/201347018-117ae1e9-9633-4387-9b99-d18271014d12.png)


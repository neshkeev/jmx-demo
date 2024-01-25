# Метрики

## Сбор метрик

1. Загрузить `jmx_exporter`:
```bash
curl -Lo ./jmx-exporter/jmx_prometheus_javaagent.jar https://repo1.maven.org/maven2/io/prometheus/jmx/jmx_prometheus_javaagent/0.20.0/jmx_prometheus_javaagent-0.20.0.jar
```
2. Запустить сервисы:
```bash
docker compose up
```
3. Дождаться, когда во всех строках в колоке `STATUS` будет написано `healthy`:
```bash
docker compose ps
```
4. Открыть localhost:9090

## Подключение по JMX через JConsole

1. Запустить сервисы (если еще не запущено):
```bash
docker compose up
```
2. Дождаться, когда во всех строках в колоке `STATUS` будет написано `healthy`:
```bash
docker compose ps
```
3. Открыть `jconsole`
```bash
jconsole
```
4. Ввести `localhost:9010` в поле `Remote Process` (Username и Password оставить пустыми)
5. Нажать кнопку `Connect`
6. В всплывающем диалоговом окне нажать кнопку `Insecure Connection`

## Подключение по JMX через VisualVM

1. Запустить сервисы (если еще не запущено):
```bash
docker compose up
```
2. Дождаться, когда во всех строках в колоке `STATUS` будет написано `healthy`:
```bash
docker compose ps
```
3. Загрузить `VisualVM`: [https://visualvm.github.io/](https://visualvm.github.io/)
4. Установить и запустить `VisualVM`
5. В главном меню выбрать `File` | `Add JMX Connection...`
6. Ввести `localhost:9010` в поле `Connection`
7. Нажать `OK`
8. В левой панели `Applications` двойным кликом мыши выбрать `kafka.Kafka`

## Prometheus

Prometheus - это система сбора и хранения метрик. Для работы с ним необходимо:

1. Запустить сервисы (если еще не запущено):
```bash
docker compose up
```
2. Дождаться, когда во всех строках в колоке `STATUS` будет написано `healthy`:
```bash
docker compose ps
```
3. Открыть Prometheus: [http://localhost:9090](http://localhost:9090)
4. В верхнем меню Prometheus нажать `Status` -> `Targets`
5. Рядом со словом `kafka` нажать `show more` и дождаться, когда в колонке `State` будет написано `Up`
6. В верхнем меню Prometheus нажать `Graph`
7. В поле `Expression` написать `gc` и выбрать одно из дополнений
8. Нажать кнопку `Execute` или клавишу `Enter`

### Grafana

Grafana - это система визуализации метрик. Для работы с Grafana необходимо:

1. Запустить сервисы (если еще не запущено):
```bash
docker compose up
```
2. Дождаться, когда во всех строках в колоке `STATUS` будет написано `healthy`:
```bash
docker compose ps
```
3. Запустить нагрузку:
```bash
docker compose exec -T kafka kafka-topics --bootstrap-server kafka:9092 --topic test-topic --create
docker compose exec -T kafka kafka-console-producer --bootstrap-server kafka:9092 --topic test-topic <<<$(yes 'Hello, World!' 2>/dev/null | head -n 100)
```
4. Открыть Grafana: [http://localhost:3000/login](http://localhost:3000/login)
5. Войти под пользователем `admin`, пароль `admin`
6. Grafana попросит поменять пароль, в качестве нового пароля можно снова указать `admin`
7. Развернуть левую панель кнопкой типа "сендвич" (три горизонтальные черточки друг над другом)
8. Открыть страницу `Dashbords`: [http://localhost:3000/dashboards](http://localhost:3000/dashboards)
9. Нажать кнопку `+ Create Dashbord` в середине экрана
10. Нажать кнопку `Import dashboard`
11. Ввести `721` в поле `Find and import dashboards for common applications at grafana.com/dashboards`
12. Нажать кнопку `Load` рядом с полем
13. Выбрать `Prometheus` в поле `Select a Prometheus data source` внизу страницы.
14. Нажать кнопку `Import`.

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

Сбор метрик

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

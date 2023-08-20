Explicación:
1.	Instalar DockerDesktop (mirar los pre requisitos según el SO que tengan)
2.	Si es en entorno Windows hay que instalar el sub sistema de Linux, para esto se abre Powershell con permisos de administrador y ejecutar e comando: wsl --install
3.	Instalar python. Marcar las opciones de variables de entorno en el path y pip
4.	crear una carpeta en tu directorio, de preferencia un lugar facil de acceder, ejemplo: c:\tp-redpando-producer\ 
5.	Dentro de esta carpeta crear subcarpetas para tener todo ordenado, en la carpeta producer ejecutar el comando para crear entorno virtual o virtualenv python -m venv nombre-entorno-virtual 
6.	Se creara una carpeta con el nombre anotado activar el entorno virtual, para ello navegar entrando a la carpertacreada\Scrictp ejecutar actívate
7.	Volver a la carpeta producer y ejecutar el comando pip install kafka-python websocket-client
8.	Crear un archivo producer-trades.py (en adjunto)
9.	navegar hasta ka carpeta c:\tp-redpando-producer\ aqui deberia estar el archivo docker-compose.yml (en adjunto)
10.	Ejecutar el comando docker compose up –d y se levantaran los contenedores de los servicios
11.	Abrir en el navegador localhost:8080, ahi podemos crear el topic finnhub-trades o por línea de comando
12.	docker exec -it redpanda /bin/sh rpk topic create finnhub-trades --brokers=localhost:9092
13.	crear el stream consumidor en ksqldb-server antes darle exit para salir de la consola de redpanda entrar en la consola de ksqldb
14.	 docker exec -it ksqldb-cli ksql http://ksqldb-server:8088 ejecutar este comando
Pasos:
CREATE STREAM finnhub_trades_stream (
    price DOUBLE,
    symbol STRING,
    timestamp STRING,
    volume DOUBLE
) WITH (
    KAFKA_TOPIC='finnhub-trades',
    VALUE_FORMAT='JSON'
);

docker compose up -d

docker ps

docker exec -it redpanda /bin/sh

rpk topic create finnhub-trades --brokers=localhost:9092

docker exec -it ksqldb-cli ksql http://ksqldb-server:8088

//este es el modelo que me funciono

CREATE STREAM finnhub_trades_stream (
    c ARRAY<STRING>,
    p DOUBLE,
    s STRING,
    t BIGINT,
    v DOUBLE
) WITH (
    KAFKA_TOPIC='finnhub-trades',
    VALUE_FORMAT='JSON'
);

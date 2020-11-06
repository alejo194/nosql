#### redis哨兵模式：一主两从，master挂掉，sentinel会将一个slave变成master
version: '2'
services:
  redis:
    image: redis:3.2
    container_name: redis-6380
    hostname: redis
    ports:
      - 6380:6380
    environment:
      - SERVICE_6380_NAME=redis
      - SERVICE_TAGS=master,slave,geo_slave,geo_master
    #labels:
    #  - kongip=192.*.*.*
    volumes:
      - ./conf/redis/redis.conf:/usr/local/etc/redis/redis.conf
      - ./conf/redis/data/sentinel.conf:/usr/local/etc/redis/sentinel.conf
      - ./conf/redis/data:/data
      - /usr/share/zoneinfo/Asia/Bangkok:/usr/share/zoneinfo/Asia/Bangkok
      - /usr/share/zoneinfo/Asia/Bangkok:/etc/localtime/
      - /etc/timezone:/etc/timezone
    restart: always
    command: ["redis-server", "/usr/local/etc/redis/redis.conf"]
    logging:
      driver: "json-file"
      options:
        max-size: "20m"
        max-file: "10"
  redis-sentinel:
    image: redis:4
    container_name: redis-sentinel
    hostname: redis-sentinel
    network_mode: host
    ports:
      - 26379:26379
    environment:
      #- SERVICE_6380_NAME=redis
      #- SERVICE_TAGS=master,slave,geo_slave,geo_master
      SERVICE_IGNORE: 'true'
    #labels:
    #  - kongip=192.*.*.*
    volumes:
      - ./conf/redis/data/sentinel.conf:/usr/local/etc/redis/sentinel.conf
      - ./conf/redis/data:/data
      - /usr/share/zoneinfo/Asia/Bangkok:/usr/share/zoneinfo/Asia/Bangkok
      - /usr/share/zoneinfo/Asia/Bangkok:/etc/localtime/
      - /etc/timezone:/etc/timezone
    restart: always
    command: ["redis-sentinel", "/usr/local/etc/redis/sentinel.conf"]
    logging:
      driver: "json-file"
      options:
        max-size: "20m"
        max-file: "10"

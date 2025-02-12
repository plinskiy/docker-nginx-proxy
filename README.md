# Nginx прокси для перенаправления запросов к внутренним nginx-серверам в докере
Реализовано: автоматическое получение Let`s Encrypt сертификатов для поддержки https
Конфигурация для каждого инстанса создается автоматически, но есть возможно ее конфигурировать руками

# Создание проксируемого Nginx
Добавьте новые контейнеры, указав переменные окружения VIRTUAL_HOST и LETSENCRYPT_HOST в контейнерах ваших приложений:
services:
  my-app:
    image: my-php-app:latest
    environment:
      - VIRTUAL_HOST=${APP_SERVER_DOMAIN}
      - LETSENCRYPT_HOST=${APP_SERVER_DOMAIN}
      - LETSENCRYPT_EMAIL=admin@${APP_SERVER_DOMAIN}
    networks:
      - proxy-network

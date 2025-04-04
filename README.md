# Stack Monitorowania i Automatyzacji Docker

To repozytorium zawiera stos Docker Compose, który konfiguruje kompleksowe środowisko monitorowania i automatyzacji, łączące Grafanę, Prometheusa, Home Assistant, Blackbox Exporter i Semaphore.

## Komponenty

### Monitoring i Wizualizacja
- **Grafana** (Port 3000)
  - Nowoczesna platforma wizualizacji
  - Wstępnie skonfigurowana z bezpiecznymi ustawieniami
  - Dostęp: http://localhost:3000
  - Domyślne dane logowania: admin/admin

- **Prometheus** (Port 9090)
  - Baza danych szeregów czasowych i system monitorowania
  - Skonfigurowany do zbierania metryk z różnych źródeł
  - Dostęp: http://localhost:9090

- **Blackbox Exporter** (Port 9115)
  - Monitoruje punkty końcowe przez HTTP, HTTPS, DNS, TCP i ICMP
  - Używany do monitorowania usług zewnętrznych
  - Dostęp: http://localhost:9115

### Automatyzacja Domowa
- **Home Assistant** (Port 8123)
  - Platforma automatyki domowej open source
  - Działa z uprawnieniami privileged dla kontroli urządzeń
  - Dostęp: http://localhost:8123

### Automatyzacja Zadań
- **Semaphore** (Port 3100)
  - Interfejs użytkownika i runner zadań Ansible
  - Używa Bolt DB do przechowywania danych
  - Dostęp: http://localhost:3100
  - Domyślne dane logowania: admin/admin

## Rozpoczęcie Pracy

1. Sklonuj to repozytorium
2. Upewnij się, że Docker i Docker Compose są zainstalowane
3. Uruchom stos:
   ```bash
   docker compose up -d
   ```

## Zarządzanie Wolumenami

Stos używa nazwanych wolumenów do przechowywania trwałych danych:
- grafana-data: Konfiguracje i dashboardy Grafany
- homeassistant-data: Konfiguracja i stan Home Assistant
- prometheus-data: Dane szeregów czasowych Prometheusa
- semaphore_data: Dane aplikacji Semaphore
- semaphore_config: Konfiguracja Semaphore
- semaphore_tmp: Pliki tymczasowe Semaphore

## Pliki Konfiguracyjne

- `docker-compose.yml`: Główna konfiguracja stosu
- `blackbox.yml`: Konfiguracja Blackbox Exporter
- `prometheus/prometheus.yml`: Konfiguracja zbierania metryk Prometheus
- Playbooki Ansible:
  - `hello.yml`: Test "Hello World"
  - `ping.yml`: Test połączenia Ansible
  - `icmp.yml`: Test dostępności ICMP

## Uwagi Dotyczące Bezpieczeństwa

- Domyślne hasła są ustawione w celach demonstracyjnych. Zmień je w środowisku produkcyjnym.
- Rejestracja w Grafanie jest domyślnie wyłączona
- Home Assistant działa w trybie privileged dla dostępu do urządzeń

## Konserwacja

Aby zaktualizować kontenery do najnowszych wersji:
```bash
docker compose pull
docker compose up -d
```

Aby zobaczyć logi:
```bash
docker compose logs [nazwa-usługi]
```
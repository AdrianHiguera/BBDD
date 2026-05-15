# Backend de Botiga en Línia amb MongoDB i Docker

Aquest projecte consisteix en la creació i gestió d'un entorn de base de dades NoSQL utilitzant **MongoDB** dins de contenidors **Docker**. L'objectiu és simular el sistema de dades d'una botiga en línia, assegurant la persistència de les dades i l'optimització de les consultes.

## Prerequisits
Per poder executar aquest projecte, necessitaràs tenir instal·lat:
- **Docker** (versió 20.10 o superior)
- **Docker Compose** (versió 2.0 o superior)
- **Git**

## Estructura de fitxers
```text
practica-mongodb/
├── docker-compose.yml     # Orquestració dels serveis (MongoDB i interfície)
├── mongo-init/
│   └── init.js            # Script per carregar dades inicials
├── queries/
│   ├── crud.js            # Consultes de creació, lectura, actualització i esborrat
│   └── advanced.js        # Consultes complexes i gestió d'índexs
├── data/                  # Volum on resideixen les dades persistents (ignorat per Git)
├── README.md              # Documentació general del projecte
└── practica.md            # Respostes teòriques i captures de pantalla

## Configuració de l'Entorn (Docker Compose)

Per a aquesta pràctica, utilitzem **Docker Compose** per orquestrar dos serveis principals que es comuniquen entre si en una xarxa aïllada.

### Fitxer `docker-compose.yml`

```yaml
services:
  mongodb-botiga:
    image: mongo:7.0
    container_name: mongodb-botiga
    ports:
      - "27017:27017"
    environment:
      - MONGO_INITDB_ROOT_USERNAME=admin
      - MONGO_INITDB_ROOT_PASSWORD=password123
    volumes:
      - ./data:/data/db
      - ./mongo-init:/docker-entrypoint-initdb.d
    networks:
      - xarxa-botiga

  mongoexpress-botiga:
    image: mongo-express:1.0
    container_name: mongoexpress-botiga
    restart: unless-stopped
    ports:
      - "8081:8081"
    depends_on:
      - mongodb-botiga
    environment:
      - ME_CONFIG_MONGODB_ADMINUSERNAME=admin
      - ME_CONFIG_MONGODB_ADMINPASSWORD=password123
      - ME_CONFIG_MONGODB_URL=mongodb://admin:password123@mongodb-botiga:27017/
    networks:
      - xarxa-botiga

networks:
  xarxa-botiga:
    driver: bridge
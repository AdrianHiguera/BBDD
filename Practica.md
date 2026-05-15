# Seguiment de la Pràctica 1.5 - Docker i MongoDB

**Nom de l'alumne:** [Adrian Higuera]
**Data:** 15-05-2026

## Bloc 0 – Preparació de l’entorn i documentació

### 1. Verificació de l'entorn de treball
S'ha comprovat el correcte funcionament de Docker, Docker Compose i Git al terminal local.

**Captura de pantalla 1: Verificació de versions i Hello World**
![Verificació Docker](./Captures/Verificació.png)

---

### 2. Creació de l'estructura del projecte
S'ha creat l'arbre de directoris i els fitxers base segons les especificacions de la pràctica per garantir un entorn organitzat.

**Captura de pantalla 2: Estructura de fitxers al VS Code**
![Estructura de fitxers](./Captures/Estructura.png)

---

## Bloc 1 – Configuració Docker Compose

### 1.2 Preguntes teòriques

**1. Quina és la diferència entre `docker run` i `docker compose up`?**
- `docker run` s'utilitza per aixecar un sol contenidor de forma individual.
- `docker compose up` s'utilitza per orquestrar diversos serveis alhora definits en un fitxer YAML, gestionant automàticament les xarxes i els volums comuns.

**2. Per a què serveix la instrucció `depends_on`? Garanteix que el servei estigui completament operatiu?**
Defineix l'ordre d'arrencada dels contenidors. En aquest cas, fa que `mongo-express` s'esperi que `mongodb-botiga` s'hagi iniciat. No obstant això, no garanteix que la base de dades estigui a punt per rebre connexions (estat *ready*), només que el procés del contenidor s'ha llançat.

**3. Diferència entre xarxa bridge per defecte i xarxa personalitzada.**
La xarxa personalitzada (`xarxa-botiga`) permet la resolució de noms per DNS intern. Això vol dir que els contenidors es poden comunicar fent servir el seu nom de servei (com `mongodb-botiga`) en lloc d'haver de conèixer la seva adreça IP privada.

---

### Captures del Bloc 1

**Captura de pantalla 3: docker compose up -d**
> Captura de la terminal després d'executar.
![Docker Compose](/Captures/Compose.png)

**Captura de pantalla 4: Contenidors en execució (docker ps)**
> Captura de la terminal després d'executar `docker ps`.
![Docker PS](/Captures/Ps.png)

**Captura de pantalla 5: Interfície Web Mongo Express**
> Captura del navegador a http://localhost:8081.
![Interfície Mongo Express](/Captures/Web.png)
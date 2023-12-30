# **Pokemon API**
Welkom bij de Pokemon API! Dit project is gericht op het creëren van een API waarmee je Pokemon's en trainers kunt beheren. Hiermee kun je gemakkelijk nieuwe Pokemon en trainers aanmaken en toewijzen, waardoor het beheer makkelijker wordt.


## database.py
Deze code is een standaardconfiguratie voor het opzetten van database-interacties met SQLAlchemy.
Het maakt gebruik van SQLAlchemy om met databases te werken. Hierbij word een session gemaakt voor interactie met de database.
De engine initialiseert de database en de sessionmaker maakt een sessionklasse voor het beheren van database interacties.
![Alt text](img/image.png)

## models.py
Hier definieert men twee SQLAlchemy-modellen, Pokemon en Trainer, die overeenkomen met de "Pokemons"- en "Trainers" tabellen in de database. Het Pokemon-model bevat kolommen voor id, name, level en type evenals een relatie (trainers) met het Trainer-model. Aan de andere kant heeft het Trainer-model kolommen voor id, name, hashed_password waarbij de trainer_id een ForeignKey is die verwijst naar het id van een Pokemon. Daarnaast heeft het Trainer-model een relatie (pokemons) met het Pokemon-model, wat de bidirectionele relatie tussen de twee modellen vormt.
![Alt text](img/image-1.png)

## schemas.py
Deze code maakt Pydantic-modellen voor gegevensvalidatie in een webapplicatie. Voor Trainers zijn er vier modellen: **TrainerBase** bevat basisgegevens, **TrainerCreate** wordt gebruikt bij het maken van nieuwe Trainers, **TrainerResponse** voegt een ID-veld en naam toe zonder passwoord voor gebruik met SQLAlchemy-ORM. Pokemon worden vergelijkbare modellen gebruikt. Het model **PokemonUpdateLevel** is voor de PUT endpoint zodat het mogelijk word om levels te veranderen. Deze modellen vergemakkelijken consistent gebruik van gegevens en bieden validatie.
![Alt text](image-4.png)
![Alt text](image-3.png)

## crud.py
Deze file bevat create, read, update en delete functies voor database-interacties in een webapplicatie, gebruikmakend van SQLAlchemy.

Er zijn functies om individuele Trainers & Pokemon op te halen op basis van hun ID, om een lijst met Pokemon & Trainers op te halen met optionele paginering, om nieuwe Pokemon & Trainers te creëren, en om ze te verwijderen.

De code maakt gebruik van modellen (models) en schemas (schemas) om de interactie met de database te structureren en te valideren. Elke functie ontvangt ook een Session-object als een databaseverbinding.
![Alt text](image-5.png)
![Alt text](image-6.png)
![Alt text](image-7.png)

## main.py
Deze code implementeert een FastAPI-webapplicatie voor het beheren van Pokemon en Trainers met behulp van een SQLite-database via SQLAlchemy. De applicatie maakt gebruik van CRUD (Create, Read, Update, Delete) operaties om gegevens te beheren.

Bij het starten van de applicatie wordt gecontroleerd of de map 'sqlitedb' bestaat en zo niet, wordt deze aangemaakt. Daarna worden de database-tabellen aangemaakt met behulp van de SQLAlchemy-modellen.

De app heeft endpoints voor het maken, lezen en verwijderen van Pokemon en Trainers, evenals het toewijzen van een Pokemon aan een Trainer. Pydantic-schemas worden gebruikt voor gegevensvalidatie.

De applicatie maakt ook gebruik van dependency injection om een database-sessie te verkrijgen voor elke endpoint, waardoor de interactie met de database wordt mogelijk gemaakt. Er zijn ook foutafhandelingsmechanismen ingebouwd, zoals het teruggeven van HTTP-foutcodes en details bij ongeldige verzoeken of ontbrekende gegevens.
![Alt text](image-8.png)
![Alt text](image-9.png)
![Alt text](image-10.png)
![Alt text](image-11.png)
![Alt text](image-12.png)

## Auth.py
Deze Python-code implementeert authenticatie en autorisatie in een webapplicatie met behulp van JSON Web Tokens (JWT).

Een CryptContext van de Passlib-bibliotheek wordt gebruikt om wachtwoorden te hashen en te verifiëren. De authenticate_trainer-functie controleert de authenticatie van trainers op basis van gebruikersnaam en wachtwoord. De create_access_token-functie genereert een JWT met een vervaltijd en ondertekent deze met een geheime sleutel.

De code is ontworpen om trainers te authentiseren en JWT's te genereren voor toegangsbeheer in een webapplicatie, met functionaliteiten voor het veilig opslaan en verifiëren van wachtwoorden, evenals het creëren van beveiligde toegangstokens met JWT's.
![Alt text](image-13.png)
![Alt text](image-14.png)

Als we naar de databank gaan zien kunnen we zien dat de hashing zijn werk doet.
![Alt text](image-34.png)


## test_main.py
Deze Python-code voert tests uit op een RESTful API voor Pokémon en trainers. De requests-bibliotheek wordt gebruikt om HTTP-verzoeken te doen en de resultaten te testen. Hier is een beknopte beschrijving van de code:
De **test_read_pokemons-functie** test het lezen van alle Pokémon in de database en controleert of het antwoord een statuscode van 200 heeft en of het een lijst is.
De **test_read_pokemon-functie** test het lezen van één specifieke Pokémon en controleert of het antwoord een statuscode van 200 heeft en of bepaalde eigenschappen zoals 'id', 'name', 'level', en 'type' aanwezig zijn.
De **get_token-functie** verkrijgt een toegangstoken door een POST-verzoek te doen met gebruikersnaam en wachtwoord. De verkregen toegangstoken wordt gebruikt voor het uitvoeren van beveiligde verzoeken.
De **test_read_trainers-functie** test het lezen van alle trainers met behulp van een beveiligd verzoek met een geldig toegangstoken.
De **test_read_trainer-functie** test het lezen van één specifieke trainer met behulp van een beveiligd verzoek met een geldig toegangstoken. Het controleert of bepaalde eigenschappen zoals 'id', 'name' aanwezig zijn en of het wachtwoord is uitgesloten.
![Alt text](image-15.png)
![Alt text](image-16.png)
![Alt text](image-17.png)

## __init__.py
Dit bestand zegt gewoon dat de directory gemarkeerd moet worden als een Python pakket.

## Postman requests
Hier zien we de Postman request dat we sturen naar onze API om data toe te voegen, te lezen en te deleten.

![Alt text](image-23.png)
![Alt text](image-24.png)
![Alt text](image-25.png)
![Alt text](image-26.png)
![Alt text](image-27.png)
Eerst zonder authorisatie de GET trainers en trainerd met id.
![Alt text](image-28.png)
![Alt text](image-29.png)
Nu met authenticatie.
![Alt text](image-30.png)
![Alt text](image-31.png)
![Alt text](image-32.png)
![Alt text](image-33.png)

## Github actions
Deze YAML-configuratie definieert een GitHub Actions-workflow met de naam "Deliver container". De workflow wordt geactiveerd bij elke 'push'-gebeurtenis in de repository.

De workflow heeft een enkele job genaamd "delivery", die wordt uitgevoerd op het nieuwste Ubuntu distro. De stappen binnen deze baan omvatten:

Haal de repository op met behulp van de GitHub Actions-actie 'checkout'.

Meld aan bij Docker Hub met behulp van de opgegeven Docker-gebruikersnaam en -wachtwoord, die als secrets variabelen zijn opgeslagen in GitHub.

Bouw een Docker-container.

Upload de gebouwde Docker-container naar Docker Hub.

Deze workflow automatiseert het proces van het bouwen en leveren van een Docker-container naar Docker Hub wanneer er wijzigingen in de repository zijn gepusht.
![Alt text](image-18.png)
![Alt text](image-19.png)

## docker/docker-compose
Deze Dockerfile definieert de configuratie voor het bouwen van een Docker-img/image. Het begint met het gebruiken van de officiële Python 3.10.0-slim base img/image. Daarna wordt de werkdirectory ingesteld op '/code', en poort 8000 wordt blootgesteld voor het accepteren van verbindingen.

Vervolgens wordt het bestand 'requirements.txt' van het lokale systeem naar de werkdirectory in de img/image gekopieerd. Daarna worden de vereiste Python-pakketten geïnstalleerd met behulp van 'pip' op basis van de inhoud van 'requirements.txt'.

Daarna wordt de inhoud van de lokale 'myproject'-directory naar de werkdirectory in de img/image gekopieerd.

Er wordt ook een map 'sqlitedb' aangemaakt binnen de werkdirectory.

Tenslotte wordt het commando uvicorn main:app --host 0.0.0.0 --port 8000 opgegeven als de standaard opstartopdracht voor de container. Dit commando start een webserver voor het uitvoeren van een FastAPI-applicatie op host "0.0.0.0" en poort "8000"
![Alt text](image-20.png)
![Alt text](image-22.png)

Deze Docker Compose-configuratie definieert een set services binnen een Docker-compose YAML-bestand. In dit geval wordt één service genaamd "pokemon-api-service" gedefinieerd.

De service maakt gebruik van het Docker-img/image "filipkolb/pokemon-api". De service wordt toegankelijk gemaakt op poort 8000 op de hostmachine door deze te koppelen aan poort 8000 in de container. Er wordt ook een volume met de naam "sqlite_pokemon" gecreëerd, dat de '/code/sqlitedb' directory in de container mount naar een volume.

Ten slotte wordt een apart volume met de naam "sqlite_pokemon" gedefinieerd. Dit word gebruikt voor het delen van gegevens tussen services of voor persistente opslag

![Alt text](image-21.png)

## Okteto 
Nu dat we op docker-hub onze img/image hebben van de API kunnen we gaan deployen. We koppelen onze github account en selecteren de repository en starten de dev omgeving op. Nu laten we docker werken om de API te deployen.
![Alt text](image-35.png)
![Alt text](image-36.png)


## Docs
![Alt text](image-37.png)
![Alt text](image-38.png)
![Alt text](image-39.png)
![Alt text](image-40.png)
![Alt text](image-41.png)
![Alt text](image-42.png)
![Alt text](image-43.png)
![Alt text](image-44.png)
![Alt text](image-45.png)
![Alt text](image-46.png)
![Alt text](image-47.png)
![Alt text](image-48.png)
![Alt text](image-49.png)
![Alt text](image-50.png)
![Alt text](image-51.png)
![Alt text](image-52.png)
![Alt text](image-53.png)

[OKTETO HOSTED SITE](https://pokemom-api-service-filipkolb.cloud.okteto.net/docs#/)
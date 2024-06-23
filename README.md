# product-compare-react
Product Compare - Aplikacja do Porównywania Produktów
Spis treści
1.	Opis projektu
2.	Funkcjonalności
3.	Instalacja
4.	Użycie
5.	Frameworki JavaScript i narzędzia
6.	Potencjalne problemy i ich rozwiązania
________________________________________
Opis projektu
"Product Compare" to aplikacja webowa, która umożliwia użytkownikom porównywanie specyfikacji różnych produktów. Dzięki prostemu i intuicyjnemu interfejsowi użytkownik może dodać produkty do listy porównawczej, a następnie zobaczyć ich szczegółowe porównanie.
Funkcjonalności
•	Dodawanie produktów do listy porównawczej.
•	Wyświetlanie szczegółowego porównania wybranych produktów.
•	Interaktywny interfejs pozwalający na dynamiczne dodawanie i usuwanie produktów z porównania.
Instalacja
Aby uruchomić projekt lokalnie, wykonaj poniższe kroki:
1.	Sklonuj repozytorium:
git clone https://github.com/Rhymond/product-compare-react.git
2.	Przejdź do katalogu projektu:
cd product-compare-react
3.	Zainstaluj zależności:
npm install
4.	Uruchom aplikację:
npm start
Użycie
Po uruchomieniu aplikacji, otwórz przeglądarkę i przejdź do http://localhost:3000, aby zobaczyć aplikację w akcji. Możesz dodawać produkty do listy porównawczej i zobaczyć szczegóły ich porównania.
JavaScript i narzędzia
React
React to biblioteka JavaScript do budowania interfejsów użytkownika. W projekcie "Product Compare" React został użyty do tworzenia dynamicznych i responsywnych komponentów UI.
•	Architektura: React opiera się na architekturze komponentowej, gdzie każdy element interfejsu użytkownika jest odrębnym komponentem, co umożliwia łatwe zarządzanie i ponowne wykorzystanie kodu.
a. Generatory komponentów (modeli, kontrolerów, API, …)
W projekcie wykorzystano narzędzie Plop do automatycznego generowania komponentów, co znacznie przyspiesza proces rozwoju aplikacji. Dzięki temu możliwe jest szybkie tworzenie szablonów komponentów, modeli i kontrolerów.
1.	Instalacja Plop:
npm install -g plop
2.	Konfiguracja Plop w pliku plopfile.js:
module.exports = function (plop) {
  plop.setGenerator('component', {
    description: 'Tworzy nowy komponent React',
    prompts: [{
      type: 'input',
      name: 'name',
      message: 'Nazwa komponentu'
    }],
    actions: [{
      type: 'add',
      path: 'src/components/{{pascalCase name}}.js',
      templateFile: 'plop-templates/component.hbs'
    }]
  });
};
3.	Uruchomienie generatora:
plop component --name "NewComponent"
Redux
Redux jest biblioteką do zarządzania stanem aplikacji, używaną do centralnego zarządzania stanem w aplikacji React.
•	Architektura: Redux opiera się na architekturze jednokierunkowego przepływu danych, gdzie stan aplikacji jest przechowywany w jednym globalnym obiekcie store. Zmiany w stanie są realizowane poprzez dispatchowanie akcji, które są następnie obsługiwane przez reducery.
Node.js
Node.js to środowisko uruchomieniowe JavaScript, które pozwala na uruchamianie kodu JavaScript poza przeglądarką, na serwerze.
•	Architektura: W projekcie "Product Compare" Node.js jest używany do uruchamiania serwera backendowego, który obsługuje API i zarządza komunikacją z bazą danych.
Express.js
Express.js to framework webowy dla Node.js, który jest używany do obsługi serwera aplikacji i zarządzania routingiem HTTP.
b. Routery kierujące ruchem HTTP
Express.js pozwala na łatwe definiowanie routerów, które kierują ruchem HTTP w aplikacji. Każdy router jest odpowiedzialny za obsługę określonej ścieżki i metody HTTP (GET, POST, PUT, DELETE).
1.	Przykład routera w Express.js:
const express = require('express');
const router = express.Router();

// GET - Pobieranie listy produktów
router.get('/products', (req, res) => {
  // Logika pobierania produktów
  res.send('Lista produktów');
});

// POST - Dodawanie nowego produktu
router.post('/products', (req, res) => {
  // Logika dodawania produktu
  res.send('Produkt dodany');
});

module.exports = router;
Szablony HTML
c. Szablony HTML
Aplikacja React korzysta z dynamicznie generowanych komponentów, jednak główny szablon HTML znajduje się w katalogu public, w szczególności index.html, który jest używany do osadzania aplikacji React.<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Porównywarka Produktów</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div id="root"></div>
    <script src="bundle.js"></script>
</body>
</html>
Konektory do baz danych
d. Konektory do baz danych
W projekcie "Product Compare" do komunikacji z bazą danych użyto biblioteki Sequelize, która jest ORM-em dla Node.js, pozwalającym na łatwe zarządzanie danymi w bazie.
1.	Instalacja Sequelize:
npm install sequelize
npm install mysql2
2.	Konfiguracja połączenia z bazą danych:
javascript
Копировать код
const { Sequelize } = require('sequelize');

const sequelize = new Sequelize('database', 'username', 'password', {
  host: 'localhost',
  dialect: 'mysql'
});

sequelize.authenticate()
  .then(() => {
    console.log('Połączenie z bazą danych nawiązane.');
  })
  .catch(err => {
    console.error('Nie udało się połączyć z bazą danych:', err);
  });
Współpraca z REST API
e. Współpraca z REST API
Aplikacja "Product Compare" współpracuje z zewnętrznymi REST API w celu pobierania i zarządzania danymi o produktach. Wykorzystano do tego bibliotekę Axios.
1.	Instalacja Axios:
npm install axios
2.	Przykład integracji z API:
import axios from 'axios';

const getProductDetails = async (productId) => {
  try {
    const response = await axios.get(`https://api.example.com/products/${productId}`);
    return response.data;
  } catch (error) {
    console.error('Błąd podczas pobierania danych o produkcie:', error);
  }
};
Potencjalne problemy i ich rozwiązania
W trakcie pracy nad aplikacją "Product Compare" mogą pojawić się różne problemy techniczne. Poniżej przedstawiono niektóre z potencjalnych problemów oraz sposoby ich rozwiązania przy użyciu dostępnych narzędzi i technik.
1. Zarządzanie stanem aplikacji
Problem: Trudność w zarządzaniu dużą ilością stanów w aplikacji.
Rozwiązanie: Użycie Redux do centralnego zarządzania stanem.
•	Opis problemu: Aplikacja zawiera wiele komponentów, które potrzebują dostępu do wspólnego stanu danych, co może prowadzić do trudności w zarządzaniu tymi danymi.
•	Rozwiązanie: Redux umożliwia przechowywanie całego stanu aplikacji w jednym globalnym obiekcie (store), z którego komponenty mogą pobierać dane i do którego mogą wysyłać akcje. Dzięki temu zapewniona jest jednostronność przepływu danych (uni-directional data flow) oraz łatwiejsze debugowanie i testowanie aplikacji.
2. Optymalizacja wydajności aplikacji
Problem: Spowolnienie działania aplikacji przy renderowaniu dużych list produktów.
Rozwiązanie: Użycie technik optymalizacji renderowania w React.
•	Opis problemu: Aplikacja może zacząć działać wolniej, gdy użytkownik porównuje duże ilości produktów lub gdy lista produktów jest dynamicznie renderowana.
•	Rozwiązanie: Można zastosować techniki optymalizacji renderowania w React, takie jak Memoization, React.memo(), useMemo() oraz lazy loading komponentów. Dzięki temu można zmniejszyć liczbę niepotrzebnych renderowań i poprawić wydajność aplikacji.
3. Problemy z integracją z zewnętrznymi API
Problem: Trudności w integracji z zewnętrznymi REST API.
Rozwiązanie: Użycie Axios do obsługi żądań HTTP oraz zarządzania błędami.
•	Opis problemu: Integracja z zewnętrznymi API może prowadzić do problemów z autoryzacją, zarządzaniem błędami sieciowymi oraz obsługą różnych formatów odpowiedzi.
•	Rozwiązanie: Axios jest wszechstronnym narzędziem do wysyłania żądań HTTP w JavaScript, które oferuje obsługę promis i interfejsów do zarządzania odpowiedziami oraz błędami. Można skonfigurować Axios do obsługi autoryzacji, ustawiania nagłówków żądań i obsługi błędów.
Przykład obsługi błędów w Axios:
import axios from 'axios';

const fetchData = async () => {
  try {
    const response = await axios.get('https://api.example.com/data');
    return response.data;
  } catch (error) {
    if (error.response) {
      // Obsługa błędów z serwera (statusy HTTP)
      console.error('Błąd odpowiedzi serwera:', error.response.data);
    } else if (error.request) {
      // Obsługa problemów z żądaniem (brak odpowiedzi)
      console.error('Brak odpowiedzi z serwera:', error.request);
    } else {
      // Obsługa innych błędów
      console.error('Wystąpił błąd podczas żądania:', error.message);
    }
    throw error; // Przekaż błąd dalej
  }
};
4. Konfiguracja środowiska deweloperskiego
Problem: Problemy z konfiguracją środowiska deweloperskiego na różnych systemach operacyjnych.
Rozwiązanie: Użycie narzędzi do zarządzania środowiskiem (np. npm, Yarn) oraz konteneryzacja (Docker).
•	Opis problemu: Deweloperzy mogą napotkać problemy z konfiguracją zależności, ścieżek dostępu oraz różnicami w konfiguracji systemowej.
•	Rozwiązanie: Można użyć menedżerów pakietów jak npm lub Yarn do zarządzania zależnościami i środowiskiem projektu. Konteneryzacja za pomocą Docker może ułatwić uruchomienie aplikacji w izolowanym środowisku, eliminując problemy z różnicami w konfiguracji systemowej.
Przykład użycia Docker Compose do konteneryzacji aplikacji:
version: '3'
services:
  frontend:
    image: node:14
    ports:
      - "3000:3000"
    volumes:
      - ./product-compare-react:/app
    working_dir: /app
    command: npm start



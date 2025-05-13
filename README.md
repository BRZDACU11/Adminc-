Wstęp

Raport przedstawia wyniki analizy i ocenę funkcjonalności systemu
zarządzania bazą danych studentów. Celem systemu jest uproszczenie procesów
związanych z rejestracją użytkowników, przechowywaniem informacji o studentach
oraz ułatwienie wyszukiwania danych. Aplikacja jest szczególnie przydatna w
instytucjach edukacyjnych, takich jak uniwersytety, szkoły wyższe i akademie, które
muszą sprawnie zarządzać danymi swoich studentów.
2. Zakres Funkcjonalności
System został zaprojektowany z myślą o prostocie użytkowania i efektywności.
Oferuje szereg funkcji, takich jak:
● Rejestracja użytkowników (wymaga hasła administratora),
● Logowanie użytkowników,
● Dodawanie nowych studentów do bazy danych,
● Wyświetlanie listy wszystkich studentów,
● Wyszukiwanie studentów według różnych kryteriów,
● Zarządzanie sesjami użytkowników, w tym możliwość wylogowania,
● Zakończenie pracy z systemem (wyjście z aplikacji).

3. Analiza Funkcji Systemu
3.1. Rejestracja Użytkowników
System pozwala na rejestrację nowych użytkowników, jednak dostęp do tej funkcji
jest zastrzeżony dla administratorów. Aby zarejestrować nowego użytkownika,
wymagane jest podanie hasła administratora. Przykładowy kod rejestracji
użytkownika:
cpp

void signup() {
string adminPass;
cout &lt;&lt; &quot;�� Podaj hasło administratora: &quot;;

cin &gt;&gt; adminPass;

if (adminPass != ADMIN_PASSWORD) {
cout &lt;&lt; &quot;❌ Niepoprawne hasło! Dostęp zabroniony.\n&quot;;
return; // Przerywamy rejestrację
} else {
cout &lt;&lt; &quot;✅ Hasło poprawne.\n&quot;;
}

string login, haslo;
cout &lt;&lt; &quot;�� Podaj login dla nowego użytkownika: &quot;;
cin &gt;&gt; login;
cout &lt;&lt; &quot;�� Podaj hasło dla nowego użytkownika: &quot;;
cin &gt;&gt; haslo;

if (userTable.find(login) == userTable.end()) {
userTable[login] = haslo;
cout &lt;&lt; &quot;✅ Użytkownik &#39;&quot; &lt;&lt; login &lt;&lt; &quot;&#39; został zarejestrowany pomyślnie!\n&quot;;
} else {
cout &lt;&lt; &quot;⚠️ Użytkownik już istnieje!\n&quot;;
}
}

3.2. Logowanie Użytkowników
Po rejestracji użytkownik może zalogować się za pomocą loginu i hasła. Zalogowani
użytkownicy uzyskują dostęp do pełnej funkcjonalności systemu. Kod logowania
użytkownika:

cpp

bool login() {
string login, haslo;
cout &lt;&lt; &quot;�� Podaj login: &quot;;
cin &gt;&gt; login;
cout &lt;&lt; &quot;�� Podaj hasło: &quot;;
cin &gt;&gt; haslo;

if (userTable.find(login) != userTable.end() &amp;&amp; userTable[login] == haslo) {
cout &lt;&lt; &quot;✅ Zalogowano pomyślnie!\n&quot;;
return true;
} else {
cout &lt;&lt; &quot;❌ Niewłaściwe dane logowania. Spróbuj ponownie.\n&quot;;
return false;
}
}

3.3. Dodawanie Studentów
System umożliwia dodawanie nowych studentów do bazy danych. Użytkownik
wprowadza dane studenta, takie jak ID, imię, nazwisko, płeć, wiek, miejscowość,
numer albumu i kierunek studiów. Przykładowy kod dodawania studenta:
cpp

void dodajStudenta() {
Student nowyStudent;

cout &lt;&lt; &quot;�� Podaj ID: &quot;;
cin &gt;&gt; nowyStudent.id;
cin.ignore();

cout &lt;&lt; &quot;�� Podaj Imię: &quot;;
getline(cin, nowyStudent.imie);

cout &lt;&lt; &quot;�� Podaj Nazwisko: &quot;;
getline(cin, nowyStudent.nazwisko);

cout &lt;&lt; &quot;�� Podaj Płeć: &quot;;
getline(cin, nowyStudent.plec);

cout &lt;&lt; &quot;�� Podaj Wiek: &quot;;
cin &gt;&gt; nowyStudent.wiek;
cin.ignore();

cout &lt;&lt; &quot;�� Podaj Miejscowość: &quot;;
getline(cin, nowyStudent.miejscowosc);

cout &lt;&lt; &quot;�� Podaj Numer Albumu: &quot;;
cin &gt;&gt; nowyStudent.numer_albumu;
cin.ignore();

cout &lt;&lt; &quot;�� Podaj Kierunek Studiów: &quot;;
getline(cin, nowyStudent.kierunek);

bazaStudentow.push_back(nowyStudent);
cout &lt;&lt; &quot;\n✅ Student został dodany poprawnie!\n&quot;;
}

3.4. Wyświetlanie Wszystkich Studentów
Po zalogowaniu użytkownicy mogą wyświetlić pełną listę studentów zapisanych w
systemie. Funkcja ta jest pomocna w weryfikacji danych. Przykładowy kod
wyświetlania studentów:
cpp

void wyswietlWszystkich() {
if (bazaStudentow.empty()) {
cout &lt;&lt; &quot;\n⚠️ Brak zapisanych studentów.\n&quot;;
return;
}

cout &lt;&lt; &quot;\n�� Lista Studentów:\n&quot;;
for (const auto&amp; s : bazaStudentow) {
cout &lt;&lt; &quot;-------------------------------------\n&quot;;
cout &lt;&lt; &quot;�� ID: &quot; &lt;&lt; s.id &lt;&lt; &quot;\n�� Imię i Nazwisko: &quot; &lt;&lt; s.imie &lt;&lt; &quot; &quot; &lt;&lt; s.nazwisko
&lt;&lt; &quot;\n�� Płeć: &quot; &lt;&lt; s.plec &lt;&lt; &quot;\n�� Wiek: &quot; &lt;&lt; s.wiek &lt;&lt; &quot;\n�� Miejscowość
&lt;&lt; s.miejscowosc
&lt;&lt; &quot;\n�� Kierunek: &quot; &lt;&lt; s.kierunek &lt;&lt; &quot;\n�� Numer Albumu: &quot;
s.numer_albumu &lt;&lt; &quot;\n&quot;;
}
cout &lt;&lt; &quot;-------------------------------------\n&quot;;
}

3.5. Wyszukiwanie Studentów
System oferuje możliwość wyszukiwania studentów według różnych kryteriów, takich
jak imię, nazwisko, płeć, miejscowość, ID, wiek i numer albumu. Przykładowy kod
wyszukiwania:
cpp

void chooseSearchMethod() const {
int method;
cout &lt;&lt; &quot;�� Wybierz metodę wyszukiwania: \n�� 1 - imię\n�� 2 - nazwisko\n��
płeć \n�� 4 - miejscowość \n�� 5 - kierunek\n�� 6 - id \n�� 7 - wiek \n�� 8 -
albumu\n �� Wybór: &quot;;
cin &gt;&gt; method;
cin.ignore(); // ignoruje znak nowej linii po wprowadzeniu metody

if (method &gt;= 1 &amp;&amp; method &lt;= 5) {
string criteria;
cout &lt;&lt; &quot;�� Wprowadź kryteria do wyszukania: &quot;;
getline(cin, criteria);
searchAndPrint(criteria, method);
} else if (method &gt;= 6 &amp;&amp; method &lt;= 8) {
int criteria;
cout &lt;&lt; &quot;�� Wprowadź kryteria do wyszukania: &quot;;
cin &gt;&gt; criteria;
searchAndPrint(criteria, method - 5);
} else {
cout &lt;&lt; &quot;❌ Niewłaściwa metoda wyszukiwania.\n&quot;;
}

}

4. Korzyści dla Firmy lub Instytucji
System zarządzania bazą danych studentów przynosi liczne korzyści:
● Automatyzacja procesów administracyjnych,
● Łatwiejsze zarządzanie danymi,
● Zwiększenie bezpieczeństwa danych,
● Skalowalność systemu.

5. Opis rozwiązania: Dodawanie studentów i wyszukiwanie
Aplikacja umożliwia dodawanie studentów do bazy oraz ich wyszukiwanie według
różnych kryteriów. Poniżej opisano implementację tych funkcji.
5.1. Dodawanie Studenta
Funkcja dodajStudenta() pozwala na wprowadzenie szczegółowych danych studenta i
zapisanie ich w bazie.
5.2. Wyszukiwanie Studenta
Funkcja chooseSearchMethod() pozwala użytkownikowi wybrać metodę
wyszukiwania (po imieniu, nazwisku, ID, itp.). System następnie przeszukuje bazę
danych i wyświetla wyniki.
6. Opis Funkcji Programu
Program oferuje użytkownikowi następujące funkcje:
● Rejestracja nowego użytkownika,
● Logowanie użytkownika,
● Dodawanie studentów do bazy,
● Wyszukiwanie studentów,
● Wylogowanie, zakończenie programu.

7. Zespół Projektowy - System Zarządzania Bazą Danych Studentów

Projekt został zrealizowany przez zespół studentów kierunku Informatyka na uczelni
Pansim. Każdy członek zespołu pełnił określoną rolę, a wspólnym celem było
stworzenie funkcjonalnego, łatwego w obsłudze i estetycznego systemu.
● Wiktor Staniszewski - Team Leader
● Gabryś Wójcik - Grafika
● Jakub Pisarzewski - IT Specialist
● Marcin Ujazdowski - IT Specialist
● Dominik Mach - Testowanie Programu za pomocą AI

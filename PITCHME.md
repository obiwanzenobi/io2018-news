# Google I/O 2018

### Omówienie nowości z zakresu developmentu oraz designu
![io](https://storage.googleapis.com/io-2018.appspot.com/v1/hashtag.gif)
---
### Android Jetpack oraz AndroidX
![jetpack](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTkXbAiokYlzUZ7JfGTs4zFc_bqx6MzxPe_KAbJHtxo_p9IUvk0)
+++
### Co to?
- Android jetpack to zbiór bibliotek, narzędzi oraz poradników, które mają być bazą do budowania nowoczesnych aplikacji. |
- AndroidX to zestaw podstawowych bibliotek, a także nowa przestrzeń nazw dla komponentów dostarczanych poza platformą. |
- Całość składa sie na nową inicjatywe Google, dotyczącą uporządkowania dostarczanych narzędzi. |
+++
### Co się zmieni?
- Znikną prefixy v4, v7, v13 itd. |
- Duże biblioteki zostaną podzielone na mniejsze (np. view pager) |
- Numerowanie wersji zostanie przywrócone z 28.0.0 do 1.0.0 (kompatybilność, feature, bugfix) |
- 28.0.0 będzie ostatnią wersją w starej konwencji |
+++
### Migracja
- Android studio Refactor (3.2 preview 14+) |
- Jetifier (dla zewnętrznych zależności w .aar oraz .jar) |
---
### Navigation
+++
### Cel? Próba uproszczenia zarządzania nawigacją i powiązanymi z nią zagadnieniami: 
- Deep linki |
- Przekazywanie argumentów do ekranów |
- "Backstack" czyli nawigacja wstecz oraz w "góre" |
- Testowanie nawigacji |
- Transakcje fragmentów |
- Animacje |
+++?image=/images/navGraphImg.png&size=auto 70%
### Graficzna wizualizacja nawigacji

+++
### Code behind
```xml
<?xml version="1.0" encoding="utf-8"?>
<navigation ...
            app:startDestination="@id/mainFragment">

    <fragment android:id="@+id/mainFragment"
              android:name="com.lightmobile.io2018_demo.ui.main.MainFragment"
              android:label="main_fragment"
              tools:layout="@layout/main_fragment">
            
        <action android:id="@+id/action_mainFragment_to_navigationFragment"
                app:destination="@id/navigationFragment"/>
        ...
    </fragment>
            
    <fragment android:id="@+id/navigationFragment"
              android:name="com.lightmobile.io2018_demo.ui.navigation.NavigationFragment"
              android:label="fragment_navigation"
              tools:layout="@layout/fragment_navigation"/>
            
    <fragment android:id="@+id/mlKitFragment"
              android:name="com.lightmobile.io2018_demo.ui.mlkit.MlKitFragment"
              android:label="fragment_ml_kit"
              tools:layout="@layout/fragment_ml_kit"/>
</navigation>
```
@[2-3]
@[5-8]
@[10-11]
+++ 
### Code behind
```kotlin
         workManagerButton.setOnClickListener(
                Navigation.createNavigateOnClickListener(R.id.action_mainFragment_to_workManagerFragment)
        )
        navigationbutton.setOnClickListener { 
            navigationbutton.findNavController().navigate(R.id.navigationFragment)
        }
```
---
## Work manager
+++
### Wrapper dla kontrolerów wykonujących zadania w tle
- Gwarantuje wykonanie podczas określonych warunków startowych |
- Nie narusza ograniczeń platformy dotyczących wykonywania zadań w tle |
- Kompatybilnie wstecznie także z urządzeniami bez Google Play Services |
- Pozwala na łączenie oraz grupowanie zadań, a także określanie jednorazowego lub okresowego wywołania |
- Umożliwia obserwowanie stanu wykonywania zadania (LiveData) |
+++
### Przekazywanie parametrów pomiędzy zadaniami
- Możliwe ustawienie parametrów wejściowych oraz wyjściowych w jednym łańcuchu |
- Dane są przekazywane w formie mapy gdzie kluczem jest wartość tekstowa a wartościami typy proste, tablice oraz łańcuchy znaków |
- Wartości są serializowane z górnym limitem 10KB. |
+++
### Tagi oraz zadanie "Unikalne"
- Istnieje możliwość przypisania jednego lub wiecej tagów podczas inicjalizacji |
- Pozwala na określenie logiki postępowania w przypadku kolejnych zadań w obrębie jednego tagu: |
- "KEEP" anuluje zadanie gdy inne z tą samą nazwą jeszcze się nie zakończyło. |
- "REPLACE" zastępuje aktualnie wykonywane zadanie z tą samą nazwą. |
- "APPEND" ustawia zadania w kolejce z zachowaniem kolejności. |

+++
### Jednolite API zastępujące (oraz rozszerzające możliwości) :
- JobScheduler |
- FirebaseJobDispatcher |
- Evernote Android Job |
- Ygit's Android Priority Jobqueue |
---
### Paging Library
- Umożliwia efektywne przedstawienie danych w RecyclerView z wykorzystaniem paginacji |
- Wymusza zdefiniowanie jednego lub więcej źródła danych (lokalnego lub zdalnego)|
- Pozwala na ustawienie prefetch'a oraz niestandardowej wielkości pierwszej parti danych |
- Udostępnia mechanizm łączenia danych lokalnych oraz tych z sieci w jedno wyjściowe źródło dla aplikacji |
+++
### Placeholders
- Aby skorzystać źródło danych musi udostępniać całkowitą liczbe elementów a wysokość każdego wiersza musi być stała |
- Użytkownik może przewinąć listę w miejsce gdzie jeszcze nie ma danych i zostaną one automatycznie doładowane |
- Zwalnia nas to z obowiązku wykorzystania widoków-loaderów |

---?image=https://material.io/design/assets/1j52aydOeI2nYsCBrPRkYpbHQRffAyg0D/casestudies-reply-main.png&size=auto 75%&position=center
### Nowości w Material Design
+++?image=https://material.io/design/assets/1331BmAsV6l543NIfc6_9cgbpQvVE4eel/casestudies-shrine-hero.png&opacity=65&size=auto 100%
### Material Theming
- Większe możliwości brandowania elementów Material Design |
- Dodano możliwość ekspresji kształtu |
- Elementy udostępnione jako Material Theme Components (wcześniej Design Support Library) dla Web, Android, iOS oraz Flutter |
+++?image=https://material.io/design/assets/10o5IbEbDt5axb8z8vwC-pJh6WyWTCgjT/masonry-crane.png&opacity=65&size=auto 100%
### Nowe narzędzia
- Zmodernizowana strona material.io |
- Material Plugin do Sketch'a |
- Gallery do dzielenia się designem (gallery.io)| 
---
### Slices
![slices](https://developer.android.com/guide/slices/images/slices-landing-example-3.png)
+++ 
### Slices
- Interaktywne zdalne widoki, które umożliwiają użytkownikowi interakcje z elementami aplikacji z poziomu systemu |
- Poczatkowo będą dostępne z poziomu Google Search |
- Dobierane na podstawie URI |
- Aplikacja Slice Viewer do podglądu tworzonych Slice |
---
### Integracja z asystentem (Actions)
![actions](/images/actions.png)
+++
### Actions
- Aplikacja musi zarejestrować dostępność wykonania jednej z zdefiniowanych akcji podstawowych (PLAY_MUSIC, EDIT_PHOTO) |
- System asystenta przetworzy wypowiedź użytkownika i dostarczy nam parametry potrzebne do wykonania akcji |
- Dzięki warstwie pośredniej całość ma sprawiać wrażenie konwersacji |
---

### ML kit
#### Machine lerning dla (prawie) każdego
+++ 
### Co udostępnia?
![mlkit](/images/mlkit.png)
+++
### Ograniczenia?
- Używa Firebase |
- Przetwarzanie w chmurze jest płatne (w przeciwieństwie do tego na urzadzeniu) |
- Nie wszystkie opcje dostępne są offline |
---
### Co jeszcze?
![magic1](https://betanews.com/wp-content/uploads/2018/05/android-jetpack.jpg)
+++
### Data Binding v2
- Umożliwia połączenie z LiveData |
- Od teraz kompiluje się (częściowo) inkrementacyjnie |
- Współpracuje z Instant Apps |
+++
### Room
- Równoczesny (oraz szybszy) dostęp wielu wątków (AheadTimeLogging dla Androida 4.3+ jeśli nie ma ograniczonej pamięci) |
- @RawQuery - dynamiczne zapytania przyjmujące SQL query zwracające zmapowane obiekty (wcześniej jedyną opcją był cursor) |
+++
### Lifecycle
- Wydzielenie cyklu życia widoku fragmentu |
- ! |
+++
### Constraint Layout 1.1 oraz 2.0
- Wersja 1.1 jest dostępna w wersji stable |
- Oferuje Bariery, Procentowe wartości szerokości i długości, Zależności kątowe (na okręgu), Grupy |
- Wersja 2.0 nie jest jeszcze oficjalnie dostępna |
- Dodatkowe Helpery wpływające na rozmieszczenie widoków, ich zachowanie oraz animacje |
- Motion Layout pozwoli na animacje z wykorzystaniem KeyFrame'ów |
+++
### D8 oraz R8
- Szybsza kompilacja (takze inkrementacyjna) i poprawione debugowanie
- Bardziej czytelne komunikaty błędów |
- Optymalizacje pod Kotlin "
- R8 wykorzystuje składnie (rule) ProGuarda. Rownocześnie może robić desugar.
+++
### Oraz
- RecyclerView selection - zaznaczanie |
- RecyclerView ListAdapter |
- androidx.webkit.* wraz z Safe Browsing (Webview) |
- Zbiór kotlin extensions dla kodu platformowego Android KTX |
---
## Bonus
```kotlin
fun printNumberSign(num: Int) {
    if (num < 0) {
         "negative"
    } else if (num > 0) {
         "positive"
    } else {
         "zero"
    }.let { print(it) }
}
printNumberSign(-2)
print(",")
printNumberSign(0)
print(",")
printNumberSign(2)
```
---
### Questions?

<br>

@fa[twitter gp-contact](@wojciech_warwas)

@fa[github gp-contact](@obiwanzenobi)

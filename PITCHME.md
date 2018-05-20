# Google I/O 2018

### Omówienie nowości z zakresu developmentu oraz designu
---
### Android Jetpack oraz AndroidX
![jetpack](https://developer.android.com/static/images/jetpack/jetpack-hero.svg)

### Navigation
+++
### Cel? Próba uproszczenia zarządzania nawigacją i powiązanymi z nią zagadnieniami: 
- Deep linki |
- Przekazywanie argumentów do ekranów |
- "Backstack" czyli nawigacja wstecz oraz w "góre" |
- Testowanie nawigacji |
- Transakcje fragmentów |
- Animacje |
+++
### Graficzna wizualizacja nawigacji
![navGraph](/images/navGraphImg.png)
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

---
## Work manager
+++
### Wrapper dla kontrolerów wykonujących zadania w tle
- Gwarantuje wykonanie podczas określonych warunków startowych |
- Nie narusza ograniczeń platformy dotyczących wykonywania zadań w tle |
- Kompatybilnie wstecznie także z urządzeniami bez Google Play Services |
- Pozwala na łączenie oraz grupowanie zadań |
- Umożliwia obserwowanie stanu wykonywania zadania (LiveData) |
- Pozwala określić czy zależy nam na jednorazowym lub okresowym wywoływaniu |
+++
### Przekazywanie parametrów pomiędzy zadaniami
- Możliwe ustawienie parametrów wejściowych oraz wyjściowych w jednym łańcuchu |
- Dane są przekazywane w formie mapy gdzie kluczem jest wartość tekstowa a wartościami typy proste, tablice oraz łańcuchy znaków |
- Wartości są serializowane z górnym limitem 10KB. |
+++
### Tagi oraz zadanie "Unikalne"
- Istnieje możliwość przypisania jednego lub wiecej tagów podczas inicjalizacji |
- Pozwala na określenie logiki postępowania w przypadku kolejnych zadań w obrębie jednego tagu: |
-- "KEEP" anuluje zadanie gdy inne z tą samą nazwą jeszcze się nie zakończyło. Użyteczne w synchronizacjach gdzie chcemy ograniczyć ilośc jednakowych zapytań itp.
-- "REPLACE" zastępuje aktualnie wykonywane zadanie z tą samą nazwą. Do zastosowania przy aktualizacjach satusów gdzie tylko ostatnia wartość ma znaczenie
-- "APPEND" ustawia zadania w kolejce z zachowaniem kolejności. (np. lista zakupów, playlista, itp.)

+++
### Jednolite API zastępujące (oraz rozszerzające możliwości) :
- JobScheduler |
- FirebaseJobDispatcher |
- Evernote Android Job |
- Ygit's Android Priority Jobqueue |

---
### Where is the magic?
![magic1](/assets/wizardMagic1.jpg)

+++?code=sample/java/Hello.java&lang=java&title=Dagger Hello world 
@[1-14](Basic module with unscoped provider.)
@[16-20](Component with just a single inject.)
@[22-34](Application with component initialization)
@[45-56](Activity inject.)

---

## Look deeper
![magic2](https://o.aolcdn.com/images/dims?thumbnail=640%2C480&quality=80&image_uri=https%3A%2F%2Fs.aolcdn.com%2Fhss%2Fstorage%2Fadam%2F78a605cfc9682db8038816df349dd9e3%2Fgandalf+lotr+macbook+apple.jpg&client=cbc79c14efcebee57402&signature=a9cba48bbfc7a8c7cc7176923a06d0482cd8bd91)
+++
![structure0](/assets/01HelloDaggerGeneratedStructure.png)

+++?code=sample/java/HelloGeneratedFactory.java&lang=java&title=Provider factory
@[24-26]
@[28-36]
@[2-6]
@[8-12]

+++?code=sample/java/HelloGeneratedComponent.java&lang=java&title=Generated Component
@[28-31]
@[48-51]
@[33-38]
@[40-46]
@[17-26]


+++?code=sample/java/HelloGeneratedInjector.java&lang=java&title=Generated Injector 
@[4-10]
@[12-19]

+++
![structure1](/assets/01HelloStructure.png)
<br/>
![structure2](/assets/01HelloDaggerSmallStructure.png)
---

## Scoped provides
![magic3](/assets/scopes.jpg)

+++?code=sample/java/ScopedComponent.java&lang=java&title=Scopes
@[1-4]
@[15-19]
@[22-23]
@[33-37]
@[44-50]
@[52-57]

+++
![diagram1](assets/singleScopeDiagram.png)

+++?code=sample/java/ScopedDoubleCheck.java&lang=java&title=Double check provider
@[8-14]
@[16-24]
@[34-37]
---
## Nested Scopes
![magic4](assets/matrioshki.jpg)

+++
![diagram2](assets/activityComponents.png)

+++?code=sample/java/NestedScopesComponents.java&lang=java&title=Nested components
@[1-5]
@[7-14]
@[16-23]
@[37-47]
@[66-74]
@[78-84]
@[86-93]
@[95-99]
@[102-105]
@[121-132]
@[144-147]
@[154-158]
@[164-167]
@[174-178]
@[185-190]
@[202-206]
@[279-291]

+++
![diagram2](assets/sessionComponents.png)

---
## Subcomponents
![magic5](http://i0.kym-cdn.com/photos/images/facebook/000/531/557/a88.jpg)

+++?code=sample/java/SubcomponensComponent.java&lang=java&title=Subcomponents approach
@[1-10]
@[12-16]
@[18-29]
@[31-37]
@[39-44]
@[46-52]
@[61-70]

---
### Should we scope everything?
![magic6](assets/scopeAll.jpg)

+++
![scopeNo](https://ic.pics.livejournal.com/deathnoteuser07/61110878/23829/23829_900.png)

+++?code=sample/java/ReusableComponent.java&lang=java&title=Reusability
@[16-26]
@[38-42]
@[88-98]
@[45-54]
@[102-111]

---
## Statics for the rescue

![magic7](https://i.imgflip.com/29rpa2.jpg)

+++?code=sample/java/StaticComponent.java&lang=java&title=Static provides
@[1-9]
@[11-18]
@[20-27]
@[29-34]
@[36-44]

---
## Bonus
+++?code=sample/java/Kotlin.kt&lang=kotlin

+++?code=sample/java/KotlinResolve.kt&lang=kotlin
---
### Questions?

<br>

@fa[twitter gp-contact](@wojciech_warwas)

@fa[github gp-contact](@obiwanzenobi)

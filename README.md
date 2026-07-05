# Instalacja wybranych aplikacji Office za pomocą Office Deployment Tool (ODT)

Poradnik dotyczy instalacji **tylko wybranych aplikacji** z pakietu Office, wykorzystając oficjalne narzędzie Microsoftu  (**ODT - Office Deployment Tool**) oraz gotowy plik konfiguracyjny `configuration.xml`

Moja przykładowa konfiguracja instaluje pakiet Office 2021 Pro Plus **z wyłączeniem**:
- Access
- Skype for Business (Lync)
- OneDrive
- OneNote
- Outlook
- Publisher
- Teams

Czyli zostaje tylko Word, Excel i PowerPoint

---

## 1. Wymagania

- Windows 10/11 (64-bit lub 32-bit)
- Uprawnienia Administratora
- Połączenie z internetem (ODT pobiera pliki instalacyjne bezpośrednio z serwerów Microsoft)

---

## 1. Odinstalowanie poprzednich wersji Office

Aby całkowicie odinstalować pozostałości po innych wersjach Office, użyj [oficjalnego narzędzia](https://aka.ms/SaRA-officeUninstallFromPC)

---

## 2. Pobranie Office Deployment Tool

1. Wejdź na oficjalną stronę Microsoftu: [Office Deployment Tool](https://www.microsoft.com/en-us/download/details.aspx?id=49117)
2. Pobierz plik `officedeploymenttool_XXXXX-XXXXX.exe`
3. Uruchom go i rozpakuj do dowolnego folderu, np. Pobrane:
4. Po rozpakowaniu w wybranym folderze pojawią się pliki:
   - `setup.exe`
   - przykładowe pliki konfiguracyjne w formacie `.xml`

---

## 3. Plik konfiguracyjny `configuration.xml`

W folderze, w którym rozpakowano ODT utwórz plik o nazwie **`configuration.xml`** z poniższą zawartością (lub pobierz mój plik z GitHuba):

```xml
<Configuration>
  <Add OfficeClientEdition="64" Channel="Current"> # Zmień 64 na 32 jeśli używasz systemu w wersji 32-bitowej
    <Product ID="ProPlus2021Retail"> # Zmień ProPlus2021Retail na swoją wersję pakietu Office (spis wersji znajdziesz poniżej)
      <Language ID="pl-pl" /> # Zmień pl-pl na język, w którym chcesz zainstalować Office
      <ExcludeApp ID="Access" />
      <ExcludeApp ID="Lync" />
      <ExcludeApp ID="OneDrive" />
      <ExcludeApp ID="OneNote" />
      <ExcludeApp ID="Outlook" />
      <ExcludeApp ID="Publisher" />
      <ExcludeApp ID="Teams" />
    </Product>
  </Add>
</Configuration>
```
---

## Wersje Office:

### Do użytku domowego:
- HomeStudent2021Retail
- HomeBusiness2021Retail
- Home2024Retail
- HomeBusiness2024Retail
- Personal2021Retail
- O365HomePremRetail

### Profesjonalne:
- Professional2021Retail
- Professional2024Retail

### Profesjonalne Plus:
- ProPlus2021Retail
- ProPlus2024Retail
- ProPlus2021Volume
- ProPlus2024Volume
- ProPlusSPLA2021Volume

### Standardowe:
- Standard2021Volume
- Standard2024Volume
- StandardSPLA2021Volume

---

## Wersje Microsoft Project:

### Profesjonalne:
- ProjectPro2021Retail
- ProjectPro2024Retail
- ProjectPro2021Volume
- ProjectPro2024Volume

### Standardowe:
- ProjectStdRetail
- ProjectStd2021Retail
- ProjectStd2024Retail
- ProjectStd2021Volume
- ProjectStd2024Volume

---

## Wersje Microsoft Visio:

### Profesjonalne:
- VisioPro2021Retail
- VisioPro2024Retail
- VisioPro2021Volume
- VisioPro2024Volume

### Standardowe:
- VisioStdRetail
- VisioStd2021Retail
- VisioStd2024Retail
- VisioStd2021Volume
- VisioStd2024Volume

---

## Rodzaje licencji:

| Licencja | Przeznaczenie
|---------------|---------------|
| **Retail (FPP)** | Użytkownicy indywidualni i małe firmy |
| **Volume (VL)** | Firmy, szkoły i instytucje |
| **SPLA** | Dostawcy usług hostingowych |
| **Microsoft 365** | Użytkownicy domowi i firmy |

---

## 4. Jak dodać lub usunąć aplikacje z wykluczeń

Aby zmienić, które aplikacje mają być pominięte, edytuj listę `ExcludeApp`.
Dostępne aplikacje dla Office 2021:

| ID | Aplikacja |
|---|---|
| `Access` | Microsoft Access |
| `Excel` | Microsoft Excel |
| `Groove` | OneDrive dla Biznesu |
| `Lync` | Skype dla Biznesu |
| `OneDrive` | Microsoft OneDrive |
| `OneNote` | Microsoft OneNote |
| `Outlook` | Microsoft Outlook |
| `PowerPoint` | Microsoft PowerPoint |
| `Publisher` | Microsoft Publisher |
| `Teams` | Microsoft Teams |
| `Word` | Microsoft Word |

**Przykład:** jeśli chcesz np. zainstalować tylko Worda i Excela, dodaj wszystkie pozostałe jako `ExcludeApp`:

```xml
<ExcludeApp ID="Access" />
<ExcludeApp ID="Lync" />
<ExcludeApp ID="OneDrive" />
<ExcludeApp ID="OneNote" />
<ExcludeApp ID="Outlook" />
<ExcludeApp ID="Publisher" />
<ExcludeApp ID="Teams" />
<ExcludeApp ID="PowerPoint" />
```

> ⚠️ Nie da się wykluczyć **wszystkich** aplikacji (przynajmniej jedna musi zostać).

---

## 5. Instalacja

1. Otwórz **wiersz poleceń (cmd)** jako Administrator.
2. Przejdź do folderu z ODT:
   ```
   cd C:\Users\TwojaNazwaUżytkownika\Downloads
   ```
3. Rozpocznij instalację Office zgodnie z stworzoną konfiguracją:
   ```
   setup.exe /configure configuration.xml
   ```
4. Poczekaj, aż instalacja się zakończy (może potrwać kilka minut, w zależności od prędkości internetu).

---

## 6. Weryfikacja instalacji

Po zakończeniu instalacji sprawdź w menu Start, czy zostały zainstalowane tylko wybrane aplikacje **(np. Word, Excel i PowerPoint)**, a wykluczone aplikacje **(np. Access, Outlook, OneNote)** się nie pojawiają.

---

## Spodobał Ci się ten poradnik?

Jeśli mój poradnik okazał się być przydatny, rozważ:

- zostawienie **⭐ gwiazdki** na GitHubie - aby przekazać podziękowania i pomóc innym trafić na ten poradnik
- zgłoszenie **🐛 issue**, jeśli znajdziesz błąd lub potrzebujesz pomocy
- udostępnienie **🔗 linku** znajomym, którzy borykają się z tym samym problemem.

---

### 💙 Wesprzyj przez PayPal

Jeśli poradnik Ci pomógł i chcesz dodatkowo docenić moją pracę, możesz wesprzeć mnie przez PayPal:

[![Donate PayPal](https://img.shields.io/badge/PayPal-wesprzyj-blue?style=for-the-badge&logo=paypal&logoColor=white)](https://www.paypal.me/xdawidpvp)

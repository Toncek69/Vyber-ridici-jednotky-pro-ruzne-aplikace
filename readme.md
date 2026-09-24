[Co dodělat ]: #
[pojmy ]: #

# Výběr řídící jednotky pro různé aplikace

$${\color{#FFA500}E9 \space \color{#4682B4}A1 }$$

## Cíle 

- **Kategorizovat a porovnat** architektury řídicích systémů (MCU, MPU, embedded systémy, PLC, iPC, programovatelná relé) podle výkonu, paměti, determinismu a spolehlivosti.
- **Analyzovat provozní prostředí a vnější vlivy** (krytí IP, teplotní rozsah, EMC rušení, vibrace) a stanovit požadavky na mechanickou a elektrickou odolnost hardware.
- **Sestavit I/O bilanci** a navrhnout optimální řídicí jednotku z reálných katalogů výrobců pro konkrétní průmyslovou či IoT aplikaci včetně projektové rezervy.
- **Vypracovat vícekriteriální rozhodovací matici** a obhájit zvolenou platformu z technického a ekonomického hlediska (pořizovací cena, náročnost vývoje, údržba a spolehlivost).
- **Provést kritický technický audit (troubleshooting)** nevhodného návrhu řízení, identifikovat bezpečnostní a provozní rizika a navrhnout certifikované řešení v souladu s průmyslovými standardy.

## Ověření cílů 

Výběr řídící jednotky pro různé aplikace

1. Příklady řídících jednotek
2. Jejich základní vlastnosti z hlediska výpočetního výkonu a velikosti paměťového prostoru
3. A z hlediska odolnosti
4. Příklady použití v praxi (kde se používají MCU, a kde ř. j. s MPU)


%% 1. Správné vysvětlení pojmů, architektur a zkratek z oblasti řídicích systémů. %%
%% 2. Schopnost posoudit vliv prostředí na výběr hardwaru a dešifrovat IP kód. %%
%% 3. Vypracování rozhodovací matice pro volbu vhodné platformy (MCU vs. PLC vs. iPC). %%
%% 4. Návrh konkrétní konfigurace řídicí jednotky na základě zadané I/O bilance a provozních podmínek. %%
%% 5. Kritická technická oponentura (audit) nevhodně navrženého řešení. %%

---

## Úlohy


### 1. Základní pojmy a architektury řídicích jednotek

*Časová dotace: 10–15 minut | Úvodní orientační úloha*

Doplňte do níže uvedené tabulky význam zkratek, základní princip a typický příklad reálného nasazení nebo zástupce:

| Zkratka / Pojem          | Co zkratka znamená (česky / anglicky) | Základní charakteristika (architektura, kde běží program)                                            | Typický zástupce (konkrétní rodina / model) | Příklad reálného nasazení                |
| :----------------------- | :------------------------------------ | :--------------------------------------------------------------------------------------------------- | :------------------------------------------ | :--------------------------------------- |
| **MCU**                  | Microcontroller Unit / mikrokontrolér                                      | Integrovaný čip (CPU + RAM + Flash na jednom substrátu), deterministický běh bez OS nebo RTOS        | např. ESP32, PIC16LF1xxx, RP2040            |        Chytré termostaty, čidla IoT, dálková ovládání, drobná elektronika                                  |Routery, multimediální přehrávače, pokladní systémy (POS), smartphony
| **MPU**                  | microprocessor unit / mikroprocesová jednotka                                      | Samostatný procesor vyžadující externí RAM a úložiště, zpravidla běží plnohodnotný OS (Linux)        |  např. Broadcom BCM2711 (Raspberry Pi 4), NXP i.MX8, Intel Atom                                           |  Routery, multimediální přehrávače, pokladní systémy (POS), smartphony                                        |
| **Embedded**             | Embedded System / vestavěný systém                                      |   Jednoúčelový počítačový systém zabudovaný do většího zařízení, navržený pro konkrétní řídicí funkce                                                                                                      | Embedded PLC, Embedded PC                   | Bílá technika, bankomaty, regulace kotlů |   
| **PLC**                  |  Programmable Logic Controller / programovatelný logický automat                                     | Průmyslový automat pro cyklické deterministické řízení procesů, vysoká odolnost, modulární/kompaktní |   Siemens SIMATIC S7-1200/1500, Allen-Bradley ControlLogix                                          |  Řízení výrobních linek, balicí stroje, automatizace čističek odpadních vod                                        |
| **iPC**                  | Industrial PC / průmyslové PC                                      |Počítač architektury x86/ARM s vysokou odolností (vibrace, prach, teploty) pro náročné výpočetní úlohy a vizualizaci                                                                                                      |  Beckhoff C60xx, Advantech UNO, Siemens Microbox                                           |Vizualizace procesů (SCADA), strojové vidění, pokročilé řízení robotických pracovišť                                          |
| **Programovatelné relé** |   Programmable Relay / programovatelné relé                                   | Zjednodušené kompaktní PLC pro méně náročné úlohy, nahrazuje časovací relé a stykačové kombinace     |  LOGO! (Siemens), Zelio Logic (Schneider Electric), EASY (Eaton)                                           | Řízení osvětlení a žaluzií, automatické otevírání bran, malé čerpací stanice                                         |

> :key: **Vysvětlení pojmů a odborné zdroje:**
> - **SoC (System on Chip):** Integrovaný obvod sdružující všechny klíčové elektronické obvody a komponenty celého počítače či elektronického systému na jediném křemíkovém čipu. 
> 	 Systém na čipu. *Wikipedie: Otevřená encyklopedie* [online]. San Francisco (CA): Wikimedia Foundation, 2024, 2024-06-07 [cit. 2026-09-17]. Dostupné z: https://cs.wikipedia.org/wiki/Syst%C3%A9m_na_%C4%8Dipu
> - **DSP (Digital Signal Processor):** Specializovaný mikroprocesor architektury Harvard optimalizovaný pro matematické výpočty v reálném čase (rychlá Fourierova transformace FFT, filtrace šumu, digitální vektorové řízení střídavých motorů). 
> 	Digitální signálový procesor. In: _Wikipedia: otevřená encyklopedie_ [online]. St. Petersburg (Florida): Wikimedia Foundation, 2006, poslední editace 28. 2. 2026 [cit. 2026-09-14]. Dostupné z: [Digitální signálový procesor – Wikipedie](https://cs.wikipedia.org/wiki/Digit%C3%A1ln%C3%AD_sign%C3%A1lov%C3%BD_procesor)
> - **FPGA (Field-Programmable Gate Array):** Programovatelné logické hradlové pole, jehož vnitřní struktura logických bloků a propojení je konfigurovatelná až u zákazníka. Umožňuje masivní paralelní zpracování s hardwarovou latencí v řádu nanosekund. 
> 	Programovatelné hradlové pole. *Wikipedie: Otevřená encyklopedie* [online]. San Francisco (CA): Wikimedia Foundation, 2024, 2024-01-10 [cit. 2026-09-17]. Dostupné z: https://cs.wikipedia.org/wiki/Programovateln%C3%A9_hradlov%C3%A9_pole


<details>
<summary> :bulb: Tip k doplnění tabulky: </summary>
<p>Zaměřte se na čas náběhu a architekturu: U MCU je kód ve vnitřní paměti Flash procesoru a vykonává se okamžitě po přivedení napájení (řádově milisekundy). U systémů s MPU a iPC musí BIOS/bootloader nejprve zavést jádro operačního systému (OS Linux, Windows) z disku/eMMC/SD karty do operační paměti RAM, což trvá desítky sekund.</p>
</details>

:star2: **Bonusová otázka k úloze 1:**
Proč se u kritických aplikací v letectví (např. systém řízení letu Fly-by-Wire) nebo v jaderné energetice stále upřednostňují jednoduché deterministické mikrořadiče s několika desítkami kilobajtů paměti nebo obvody FPGA před moderními vícejádrovými gigahertzovými procesory s gigabajty RAM?

*Vaše odpověď:*
`...`

---

### 2. Parametry, paměti a provozní odolnost (IP krytí)

*Časová dotace: max. 15 minut | Mírně náročnější úloha propojující parametry a praxi*

1. **Typy pamětí v řídicích jednotkách:**
   - Doplňte porovnání pamětí z hlediska stálosti dat a rychlosti:
     - **RAM:** 
	     - **Je volatilní (energeticky závislá)?**  [ **Ano** / Ne]
	     - **Rychlost zápisu:** Velmi vysoká (v řádu nanosekund)
	     - **K čemu se využívá v PLC/MCU:** K ukládání dočasných dat během chodu programu (proměnné, stav časovačů, čítačů, mezipaměť)
     - **Flash (ROM):** 
	     - Je volatilní? Ano / **Ne**
	     - **K čemu se využívá v PLC/MCU:** K trvalému uložení samotného řídicího programu (firmwaru) a konfigurace zařízení
     - **EEPROM / NVRAM:** 
	     - Je volatilní? Ano / **Ne**
	     - **K čemu se využívá v PLC/MCU:** K ukládání remanentních dat (konfigurační parametry, provozní statistiky, kalibrační hodnoty), která musí zůstat zachována i po vypnutí napájení
   - *Otázka z praxe:* Kam se v průmyslovém PLC ukládají aktuální provozní proměnné (např. čítače vyrobených kusů nebo motohodiny), aby se při nečekaném výpadku napájení neztratily (tzv. remanentní / retain data)?
     - Odpověď: Do remanentní paměti (NVRAM / EEPROM), případně do částí paměti RAM zálohovaných baterií či superkondenzátorem (NVRAM / BBRAM).

2. **Reálný čas a determinismus (Hard vs. Soft Real-Time):**
   - Proč pro reakci na nouzové zastavení lisu (požadavek reakce do 5 ms) použijeme PLC či mikrokontrolér s RTOS, a nikoliv běžné Raspberry Pi s operačním systémem Raspberry Pi OS (standardní Linux)?
     - Odpověď: Běžný Raspberry Pi OS je univerzální, preemptivní víceúlohový operační systém (**Soft Real-Time**). Jeho plánovač procesů nedokáže garantovat maximální dobu odezvy (*deadline*), protože může být pozdržen obsluhou systémového přerušení, diskem, síťovým provozem nebo správou paměti, což způsobuje zpoždění v řádu desítek až stovek milisekund. Pro nouzové zastavení lisu do 5 ms je vyžadován **Hard Real-Time** determinismus – PLC či mikrokontrolér s RTOS vykonává řídicí cyklus v garantovaném čase bez vlivu aplikací na pozadí, kde jakékoliv překročení limitu 5 ms představuje riziko havárie či úrazu.

3. **Odolnost vůči vlivům prostředí a dešifrování kódu IP:**
   - Dešifrujte kód **IP68**:
     - **První číslice (6):** Zcela prachotěsné zařízení (úplná ochrana před vniknutím prachu a dotykem jakýmkoliv nástrojem).
     - **Druhá číslice (8):** Ochrana proti nepřetržitému ponoření do vody za podmínek určených výrobcem (tlak a čas).
   - Jaké minimální krytí IP musí mít rozváděč umístěný ve venkovním nekrytém prostředí, kde na něj přímo dopadá déšť a fouká polétavý prach?
     - Označte správnou volbu: `[ ] IP20` | `[ ] IP44` | `[X] IP65` | `[ ] IP00`
     - Zdůvodnění: Krytí **IP65** poskytuje úplnou prachotěsnost (1. číslice **6**) a ochranu proti tryskající vodě ze všech směrů (2. číslice **5**). Krytí IP44 nechrání před jemným prachem (pouze před částicemi >1 mm) a nezaručuje dostatečnou ochranu před hnaným deštěm. IP20 a IP00 nemají žádnou ochranu proti vodě.

> :key: **Vysvětlení pojmů a odborné zdroje:**
> - **Determinismus (Real-Time):** Vlastnost systému, která zaručuje, že odezva na vstupní událost proběhne vždy v přesně definovaném a předvídatelném čase (deadline). V *Hard Real-Time* systémech znamená nedodržení časového limitu fatální havárii celého procesu. 
> 	Operační systém reálného času. *Wikipedie: Otevřená encyklopedie* [online]. San Francisco (CA): Wikimedia Foundation, 2024, 2024-05-12 [cit. 2026-09-17]. Dostupné z: https://cs.wikipedia.org/wiki/Opera%C4%8Dn%C3%AD_syst%C3%A9m_re%C3%A1ln%C3%A9ho_%C4%8Dasu
> - **Krytí IP (Ingress Protection):** Mezinárodní standard dle normy **ČSN EN 60529** určující stupeň ochrany krytem před vniknutím pevných cizích těles včetně prachu (1. číslice 0–6) a vniknutím vody (2. číslice 0–9K).
> 	ČESKÝ NORMALIZAČNÍ INSTITUT. *ČSN EN 60529 (33 0330) Stupně ochrany krytem (krytí - IP kód)*. Praha: Český normalizační institut, 1993. Třídící znak 330330.
> - **Remanentní paměť (Retain):** Paměťový prostor v PLC, jehož obsah zůstává zachován i po přerušení napájecího napětí (využívá zálohovací baterii, superkondenzátor nebo zápis do FRAM/MRAM/EEPROM).

<details>
<summary> :bulb: Tip k otázce determinismu: </summary>
<p>Běžný Linux je <b>preemptivní víceúlohový systém</b>, který se snaží spravedlivě rozdělit čas procesoru mezi stovky procesů. Může se stát, že kvůli obsluze disku, správě paměti nebo síťovému provozu se proces řízení pozdrží na desítky milisekund. PLC naproti tomu vykonává cyklus v pevném taktu bez zpoždění vyvolaného aplikacemi na pozadí.</p>
</details>

:star2: **Bonusová otázka k úloze 2:**
Co označuje doplňkové písmeno **K** v kódu krytí **IP69K** a v jakém průmyslovém odvětví je toto krytí bezpodmínečně vyžadováno?

*Vaše odpověď:*
Písmeno **K** označuje ochranu proti vysokotlakému a vysokoteplotnímu tryskání vody (tlak 80–100 bar, teplota vody +80 °C, čištění pomocí WAP). Toto krytí je vyžadováno v **potravinářském a farmaceutickém průmyslu** a u zemědělské/užitkové techniky, kde probíhá pravidelná chemická a tlaková sanitace zařízení.

---

### 3. Rozhodovací matice platforem (MCU vs. PLC vs. iPC) 

*Časová dotace: 20–25 minut | :star: Klasifikovaná inženýrská úloha na známky*

Jste v pozici nezávislého konzultanta automatizace. Tři různí zákazníci požadují navrhnout optimální kategorii řízení.

#### Příklad aplikace (vzorové řešení):
- **Vzorová aplikaci 0 – Automatická vjezdová závora na parkoviště:** Jednoduchý jednoúčelový systém s indukční detekční smyčkou vozidla, bezpečnostní optozávorou, koncovými spínači polohy ramene, motorem závory (vpřed/vzad) a výstražným semaforem (červená/zelená). Požadavek na jednoduchou správu správcem objektu a spolehlivý chod v rozváděči u vjezdu.

#### Popis zadaných aplikací pro studenty:
1. **Aplikace A – Chytrý pokojový termostat (IoT):** Bateriově napájený přístroj měřící teplotu a vlhkost v místnosti, zobrazující údaje na e-ink displeji a odesílající data přes protokol ZigBee/Wi-Fi do domácí brány. Plánovaná sériová výroba: 10 000 kusů ročně.
2. **Aplikace B – Automatická balicí linka:** Průmyslová linka ve výrobní hale. Obsahuje 28 optických snímačů, 14 pneumatických válců, 3 dopravníkové pásy s asynchronními motory a bezpečnostní světelnou závoru. Vyžaduje se nepřetržitý provoz 24/7 a snadná údržba podnikovým elektrikářem.
3. **Aplikace C – Kontrolní stanice optické jakosti svarů:** Pracoviště se 2 vysokorychlostními průmyslovými GigE kamerami snímajícími svary na karoserii automobilu. Snímky v rozlišení 4K jsou analyzovány neuronovou sítí v reálném čase, vady jsou označeny a ukládány do podnikové relační databáze (SQL / MES).

#### Váš úkol:
Vyplňte rozhodovací matici. Jako vzor poslouží vyplněný sloupec pro **Vzorovou aplikaci 0**. Přiřaďte každé aplikaci nejvhodnější platformu (**MCU / Embedded SoC**, **Kompaktní/modulární PLC**, **Průmyslové PC – iPC**) a doplňte multikriteriální posouzení:

| Kritérium hodnocení | **Vzorová aplikace 0 (Vjezdová závora - VZOR)** | Aplikace A (Pokojový termostat) | Aplikace B (Balicí linka) | Aplikace C (Kamerová kontrola svarů) |
| :--- | :--- | :--- | :--- | :--- |
| **Doporučená platforma** *(MCU / PLC / iPC)* | **Programovatelné relé / kompaktní PLC** *(např. Siemens LOGO!, Eaton easyE4)* | **MCU / Embedded SoC** *(např. ESP32, STM32, nRF52)* | **Kompaktní / modulární PLC** *(např. Siemens S7-1200 / S7-1500)* | **Průmyslové PC (iPC)** *(např. Beckhoff, Advantech, Siemens SIMATIC)* |
| **Pořizovací cena HW na 1 kus** *(nízká < 500 Kč / střední 5–30 tis. Kč / vysoká > 50 tis. Kč)* | **Střední** *(cca 3 500 – 6 000 Kč)* | **Nízká** *(< 500 Kč / ks při sérii 10k ks)* | **Střední** *(15 000 – 35 000 Kč)* | **Vysoká** *(> 60 000 Kč)* |
| **Primární programovací jazyk** *(C/C++/MicroPython vs. IEC 61131-3 ST/LAD vs. Python/C#/C++ pod OS)* | **FBD / LAD** *(grafické funkční bloky nebo liniové schéma dle IEC 61131-3)* | **C / C++ / MicroPython** | **IEC 61131-3 (LAD / ST / FBD)** | **Python / C# / C++** *(s akcelerací GPU/NPU)* |
| **Klíčový technický argument pro volbu** *(např. spotřeba, determinismus, grafický výkon)* | Montáž přímo na DIN lištu v rozváděči, integrovaný displej pro nastavení časovačů přímo na místě, robustní reléové výstupy pro motor a semafor, napájení 24 V DC / 230 V AC bez nutnosti vývoje vlastního plošného spoje. | Extrémně nízká spotřeba proudu (spánkové režimy pro bateriový provoz), nízké výrobní náklady při sérii 10 000 ks, integrovaný modul Wi-Fi/ZigBee. | Vysoký determinismus, spolehlivost 24/7, modulární I/O na DIN lištu, přehledná diagnostika a úprava programu údržbářem v LAD. | Vysoký výpočetní a grafický výkon (GPU/AI) pro analýzu 4K obrazu z 2× GigE kamer v reálném čase a přímá konektivita do SQL/MES databází. |
| **Hlavní riziko při volbě špatné platformy** *(proč by neuspěly ostatní dvě varianty)* | **MCU:** Nutnost vývoje vlastní desky, nízká odolnost vůči venkovnímu rušení a obtížný servis údržbou.<br>**iPC:** Zbytečně extrémní cena (> 30 tis. Kč), dlouhý start po výpadku napájení a vysoká spotřeba. | **PLC / iPC:** Nelze napájet z baterie, obrovské rozměry, neakceptovatelně vysoká cena pro masovou výrobu spotřební elektroniky. | **MCU:** Složitý vývoj vlastního HW, problém se servisem.<br>**iPC:** Zbytečně vysoké náklady, zranitelnost výpadkem OS pokud není použit SoftPLC. | **MCU / PLC:** Nemají dostatek operační paměti, výpočetního grafického výkonu pro AI ani rozhraní pro přenos 4K videa v reálném čase. |

> **Kritéria hodnocení úlohy 3 (bodování a známka):**
> - :star: **Správnost technického přiřazení platforem (30 %):** Stoprocentně logické a obhajitelné přiřazení všech 3 technologií.
> - :star: **Inženýrská a ekonomická argumentace (40 %):** Zohlednění ekonomiky sériovosti (kusová vs. masová výroba), spotřeby energie, náročnosti vývoje a schopností servisního personálu.
> - :star: **Analýza rizik nevhodné platformy (30 %):** Věcné zdůvodnění, proč je v daném případě jiná platforma neefektivní, příliš drahá nebo neschopná úlohu odbavit.

> :key: **Vysvětlení pojmů a odborné zdroje:**
> - **Norma ČSN EN 61131-3:** Mezinárodní standard pro programovací jazyky PLC automatů. Definuje dva textové jazyky (ST – strukturovaný text, IL – seznam instrukcí) a tři grafické jazyky (LD – příčkový diagram / kontaktní schéma, FBD – funkční blokové schéma, SFC – sekvenční funkční schéma).
> 	ČESKÝ NORMALIZAČNÍ INSTITUT. *ČSN EN 61131-3 ed. 3 (18 0080) Programovatelné řídicí jednotky - Část 3: Programovací jazyky*. Praha: Úřad pro technickou normalizaci, metrologii a státní zkušebnictví, 2014. Třídící znak 180080.
> - **GigE Vision:** Komunikační standard rozhraní pro průmyslové kamery využívající gigabitový Ethernet, umožňující přenos nekomprimovaného videa vysokou rychlostí na velké vzdálenosti.

<details>
<summary> :bulb: Tip pro Aplikaci A vs. B vs. C: </summary>
<p>U aplikace A rozhoduje kusová cena a odběr proudu z baterie (PLC ani iPC z baterie nerozběhnete). U aplikace B potřebujete vyměnitelný modul na DIN lištu s diagnostickými LED, který přeprogramuje běžný údržbář v jazyce LAD. U aplikace C potřebujete obrovský výpočetní výkon pro AI a ovladače pro průmyslové kamery, což MCU ani běžné PLC nezvládne.</p>
</details>

:star2: **Bonusová otázka k úloze 3:**
Co je to tzv. **SoftPLC** a jak umožňuje průmyslovému PC (iPC) kombinovat výhody operačního systému Windows/Linux a deterministického řízení reálného času v jediném fyzickém počítači?

*Vaše odpověď:*
**SoftPLC** je softwarové řešení (např. *Beckhoff TwinCAT* nebo *CODESYS Control RTX*), které pomocí hypervizoru nebo RTOS rozšíření vyhradí jedno nebo více jader CPU výhradně pro deterministické řízení reálného času s nejvyšší prioritou. Zbylá jádra procesoru obsluhují standardní operační systém (Windows/Linux) pro vizualizaci, databáze a komunikaci. Pokud běžný operační systém zamrzne nebo vykáže chybu (BSOD), RTOS jádro s řízením technologie běží nepřerušovaně dál.

---

### 4. Návrh a konfigurace řídicí jednotky pro čerpací stanici

*Časová dotace: 25–30 minut | :star: Klasifikovaná inženýrská úloha na známky*

Jste v roli projektanta automatizace. Zákazník poptává zhotovení řízení pro obecní přečerpávací stanici odpadních vod.

#### Zadání technologického procesu a periferií:
- **Snímače a vstupy:**
  - 3× plovákový hladinový spínač (havarijní spodní hladina proti chodu nasucho, zapínací hladina, havarijní přepad) – bezpotenciálový kontakt spínající 24 V DC.
  - 1× hydrostatická ponorná sonda výšky hladiny v jímce – výstupní signál 4–20 mA.
  - 1× termistorové ochranné relé přehřátí motoru čerpadla – poruchový kontakt 24 V DC.
- **Akční členy a výstupy:**
  - 2× stykač pro spouštění motorů hlavního a záložního čerpadla – spínání cívky stykače 230 V AC / 0,5 A.
  - 1× opticko-akustický výstražný maják – napájení 24 V DC / 0,3 A.
  - 1× řízení otáček frekvenčního měniče hlavního čerpadla – analogový signál 0–10 V.
- **Komunikace a přenos dat:**
  - Odesílání údajů o hladině a poruchách na dispečink vodáren (Ethernet / Modbus TCP nebo GSM/LTE modul).
- **Provozní podmínky:**
  - Venkovní nekrytý terén, rozváděč vystavený dešti, prachu a teplotám v rozmezí **-20 °C až +45 °C**.

#### Váš úkol:

1. **Sestavte tabulku I/O bilance** a spočtěte celkový počet signálů. Připočtěte rezervu min. 20 % pro budoucí rozšíření:

| Typ signálu | Požadavek aplikace (kusy) | Popis signálů v aplikaci | Počet po započtení rezervy (+20 %) |
| :--- | :--- | :--- | :--- |
| **Digitální vstup (DI)** | **4** | 3× plovákový spínač (havarijní dno, start, přepad), 1× porucha termistoru | **5** *(po zaokrouhlení nahoru)* |
| **Digitální výstup (DO) – reléový** | **2** | 2× cívka stykače motorů čerpadel (spínání 230 V AC přes pomocná relé) | **3** |
| **Digitální výstup (DO) – tranzistorový** | **1** | 1× opticko-akustický maják (24 V DC / 0,3 A) | **2** |
| **Analogový vstup (AI)** | **1** | 1× hydrostatická sonda výšky hladiny (4–20 mA) | **2** |
| **Analogový výstup (AO)** | **1** | 1× řízení otáček frekvenčního měniče (0–10 V) | **2** |

2. **Výběr konkrétního hardwaru z katalogu výrobce:**
   - Navrhněte konkrétní přístroj z praxe (např. *Siemens LOGO! 24RCE + rozšiřující moduly*, *Siemens S7-1200 CPU 1212C/1214C DC/DC/RLY*, *Schneider Modicon M221*, *Eaton easyE4-UC-12RC1*, *WAGO 750*, případně průmyslový IoT kontrolér typu *UniPi Neuron*).
   - Uveďte:
     - Výrobce a přesný model CPU: Siemens SIMATIC S7-1200, CPU 1214C DC/DC/DC
     - Objednací kód (Part Number / Order Code): `6ES7214-1AG40-0XB0` *(obsahuje 14× DI 24V DC, 10× DO 24V DC, 2× AI 0–10V)*
     - Rozšiřující moduly (pokud jsou nutné pro AI 4–20 mA nebo AO 0–10 V): Signal Board SB 1232 1 AO (`6ES7232-4HA30-0XB0`) pro výstup 0–10 V, Signal Module SM 1231 4 AI (`6ES7231-4HD32-0XB0`) pro proudové vstupy 4–20 mA.
     - Napájecí napětí zvolené jednotky: 24 V DC (napájeno průmyslovým zdrojem Siemens SITOP PSU100S 24V/2,5A)
     - Jak je vyřešeno odesílání dat na dispečink: Integrované PROFINET rozhraní s protokolem Modbus TCP propojené s průmyslovým 4G/LTE routerem (např. Teltonika RUT241) přes zabezpečený VPN tunel na dispečink.
     - Odkaz na technický list (datasheet): https://mall.industry.siemens.com
     - Odkazy na další použité zdroje: Siemens SIMATIC S7-1200 System Manual.

3. **Technické ověření z datasheetu:**
   - Zvládá zvolená jednotka garantovaný provoz při -20 °C? Doložte údaj z datasheetu: Áno, jednotky Siemens S7-1200 CPU 1214C mají dle datasheetu garantovaný rozsah provozních teplot **-20 °C až +60 °C** (při svislé montáži -20 °C až +50 °C).
   - Jakým způsobem spínáte cívku stykače 230 V AC (reléový výstup jednotky přímo, nebo přes pomocné mezilehlé relé)? Zdůvodněte: Spínání probíhá **přes pomocné mezilehlé relé** (např. *Finder 38 Series* nebo *Phoenix Contact RIF*). Indukční zátěž cívky stykače vyvolává při rozpojení napěťové špičky; mezilehlé relé zajišťuje galvanické oddělení tranzistorového výstupu PLC a v případě opotřebení kontaktů představuje snadno a levně vyměnitelný prvek.

4. **Krytí rozváděče:**
   - Jaké minimální krytí **IP skříně** zvolíte? Jak v rozváděči zajistíte provoz v mrazech -20 °C a v letních vedrech?
     - Zvolené krytí rozváděče: **IP65** *(nerezová nebo sklolaminátová skříň Rittal odolná vůči dešti a prachu)*.
     - Teplotní management skříně: Pro mrazy (-20 °C) instalace odporového **topného tělesa s termostatem** (např. 50 W na DIN lištu) pro udržení vnitřní teploty nad +5 °C a zabránění kondenzaci vlhkosti. Pro letní vedra (+45 °C) použití **stříšky proti slunečnímu záření** a **větrací mřížky s filtrem IP55 a ventilátorem** spínaným termostatem.

> **Kritéria hodnocení úlohy 4 (bodování a známka):**
> - :star: **Správnost I/O bilance a dimenzování (30 %):** Správný součet všech signálů, korektní rozlišení reléových vs. tranzistorových výstupů a správné započtení rezervy min. 20 %.
> - :star: **Reálnost výběru a kompatibilita HW (40 %):** Zvolený přístroj skutečně existuje na trhu, konfigurace plně pokrývá všechny vstupy/výstupy (včetně analogů 4–20 mA a 0–10 V) a komunikaci.
> - :star: **Posouzení provozních podmínek a instalace (30 %):** Správná volba krytí rozváděče (min. IP65), vyřešení vytápění/ventilace pro mráz a spolehlivé galvanické oddělení výkonových akčních členů.

> :key: **Vysvětlení pojmů a odborné zdroje:**
> - **Proudová smyčka 4–20 mA:** Průmyslový standard pro přenos analogových signálů ze senzorů. Výhodou oproti napěťovému signálu 0–10 V je vysoká odolnost proti elektromagnetickému rušení, nezávislost na odporu dlouhého vedení a detekce přetržení vodiče (pokud je proud roven 0 mA, jde o poruchu vedení – tzv. živá nula / live zero).
> 	Proudová smyčka. *Wikipedie: Otevřená encyklopedie* [online]. San Francisco (CA): Wikimedia Foundation, 2023, 2023-04-18 [cit. 2026-09-17]. Dostupné z: https://cs.wikipedia.org/wiki/Proudov%C3%A1_smy%C4%8Dka
> - **Galvanické oddělení:** Elektrické oddělení dvou elektrických obvodů (např. pomocí optočlenů nebo relé), které zabraňuje přenosu rušení, rozdílům zemních potenciálů a chrání citlivé vstupy řídicí jednotky před zničením přepětím.
> - **Bezpotenciálový kontakt** (označovaný také jako **dry contact**) je elektrický kontakt, který sám o sobě nemá žádné vlastní napětí ani neposkytuje žádný proud. Funguje čistě jako mechanický nebo elektronický spínač (jako klasický vypínač na zdi), který pouze spojí nebo rozpojí dva vodiče v externím obvodu.

<details>
<summary> :bulb: Tip pro výběr modulů: </summary>
<p>Pozor na analogové vstupy: Základní kompaktní jednotky (např. LOGO! nebo S7-1200) mívají integrované analogové vstupy pouze pro napětí 0–10 V. Vstupní signál 4–20 mA ze sondy vyžaduje buď speciální rozšiřující modul pro proudové signály, nebo zařazení přesného paralelního odporu 500 Ω (převod 4–20 mA na 2–10 V).</p>
</details>

:star2: **Bonusová otázka k úloze 4:**
Proč se u čerpadel v čistírnách odpadních vod a jímkách striktně upřednostňuje měření hladiny pomocí proudového signálu 4–20 mA před napěťovým signálem 0–10 V a proč se do jímky nepoužívá ultrazvukový senzor, pokud v ní vzniká hustá pěna?

*Vaše odpověď:*
1. **4–20 mA vs. 0–10 V:** Proudová smyčka je imunní vůči úbytkům napětí na dlouhém vedení a elektromagnetickému rušení. Navíc má „živou nulu“ (4 mA = dno jímky); pokud proud klesne na 0 mA, systém okamžitě detekuje poruchu či přerušení kabelu.
2. **Ultrazvuk vs. pěna:** Ultrazvukový senzor měří odraz akustické vlny od hladiny. Hustá pěna akustický signál pohlcuje a rozptyluje (funguje jako zvuková izolace), což vede ke ztrátě měření nebo chybnému odečtu výšky pěny namísto kapaliny. Hydrostatická sonda měří tlak u dna, který závisí výhradně na sloupci vody.

---

### 5. Technický audit a oponentura nevhodného návrhu

*Časová dotace: 20–25 minut | :star: Klasifikovaná inženýrská úloha na známky*

Jako vedoucí inženýr jste převzal projekt po nezkušeném brigádníkovi, který navrhl řízení automatizovaného tvářecího a lisovacího stroje v prašné kovářské dílně následovně:
- **Řídicí deska:** Běžná vývojová deska **Arduino Uno (Rev3)** s mikrokontrolérem ATmega328P.
- **Pouzdro a umístění:** Plastová krabička vytištěná na 3D tiskárně z materiálu **PLA**, přišroubovaná přímo na těleso vibrujícího hydraulického lisu.
- **Napájení:** 5V USB nabíječka na mobilní telefon zapojená do prodlužovacího kabelu 230 V.
- **Spínání zátěže:** 4kanálový hobby reléový modul z čínského e-shopu propojený s Arduinem tenkými nepájenými vodiči (DuPont propojky). Modul přímo spíná 400V ventily hydrauliky.
- **Bezpečnost (Safety):** Nouzové stop tlačítko (E-Stop) je zapojeno přímo do digitálního pinu D2 Arduina jako softwarové přerušení (interrupt), které v kódu nastaví výstupy na `LOW`.

#### Váš úkol:

1. **Zpracujte písemný audit rizik (minimálně 4 fatální technická selhání):**
   Vyplňte protokol o zjištěných vadách a popište konkrétní fyzikální mechanismus, jak daná chyba způsobí havárii stroje či ohrožení lidského života:

| Oblast auditu | Zjištěná vada v amatérském návrhu | Fyzikální mechanismus selhání (proč to selže) | Následek pro stroj nebo obsluhu |
| :--- | :--- | :--- | :--- |
| **Elektromagnetická kompatibilita (EMC)** | Hobby reléový modul spínající 400V ventily bez odrušení (RC členů/varistorů). | Rozpínání indukční zátěže ventilů generuje vysokonapěťové špičky, které se indukují do nekrytých vodičů a napájení Arduina. | Zasekávání procesoru, resetování programu, zamrznutí řízení a nebezpečné neřízené spínání ventilů. |
| **Mechanická a teplotní odolnost** | PLA plast a montáž na těleso lisu | PLA plast má nízkou teplotu skelného přechodu ($T_g \approx 60\ \text{°C}$) a pod vlivem stálých vibrací křehne a praská. | Deformace nebo rozpad krabičky, upadnutí Arduina, zkrat o těleso stroje a mechanické zničení desky. |
| **Konektivita a propojení vodičů** | DuPont propojovací kabely bez aretace | Vibrace lisu způsobí uvolnění nepájených konektorů, oxidaci kontaktů a přechodový odpor. | Náhodné výpadky signálů, falešná spínání a ztráta řízení nad strojem. |
| **Funkční bezpečnost (Safety)** | Nouzový stop řešený softwarově v čipu | Při zamrznutí procesoru či chybě programu softwarový interrupt neselže. Návrh nesplňuje normu ČSN EN ISO 13849-1. | Nemožnost zastavit lis při havárii. Riziko těžkého nebo smrtelného úrazu obsluhy. |

2. **Návrh profesionálního nápravného řešení:**
   - Navrhněte, jakými certifikovanými průmyslovými komponenty tento celek nahradíte při zachování minimálního rozpočtu:
     - *Náhrada řídicí jednotky:* Certifikované průmyslové PLC / programovatelné relé (např. *Siemens S7-1200* nebo *Siemens LOGO! 24RCE*) umístěné do oceloplechového rozváděče na DIN lištu mimo vibrace.
     - *Náhrada napájecího zdroje:* Stabilizovaný průmyslový zdroj 24 V DC na DIN lištu (např. *Mean Well NDR-120-24*) s odrušovacím filtrem, nadproudovou a přepěťovou ochranou.
     - *Způsob zapojení bezpečnostního okruhu (Safety):* Jak musí být podle norem zapojeno tlačítko Emergency Stop (E-Stop)? Smí být spoléháno pouze na software mikrokontroléru? Zdůvodněte: Tlačítko E-Stop musí mít **dvoukanálový rozpínací kontakt (2 NC)** zapojený hardwarově do **bezpečnostního relé** (např. *Pilz PNOZ* nebo *Schneider Preventa*). Toto relé při stisknutí tlačítka **přímo a galvanicky odpojí napájení silových stykačů** hydraulických ventilů na hardwarové úrovni nezávisle na procesoru PLC/MCU. Na software mikrokontroléru se nesmí spoléhat, protože může zamrznout.

> **Kritéria hodnocení úlohy 5 (bodování a známka):**
> - :star: **Odborná úroveň identifikace závad (35 %):** Přesná technická terminologie (např. elektromagnetická indukce, absence odrušovacích varistorů, skelný přechod PLA plastu při 60 °C, studené spoje a vyklepání konektorů vibracemi).
> - :star: **Pochopení norem funkční bezpečnosti Safety (35 %):** Znalost základního principu bezpečnosti strojních zařízení – nouzové zastavení musí být řešeno hardwarově přes certifikované bezpečnostní relé s nuceně vedenými kontakty, nikoliv pouhým softwarovým vstupem MCU.
> - :star: **Kvalita a realizovatelnost nápravného řešení (30 %):** Návrh odpovídá robustní průmyslové praxi s montáží do oceloplechového rozváděče na DIN lištu.

> :key: **Vysvětlení pojmů a odborné zdroje:**
> - **Funkční bezpečnost (Safety) vs. Kybernetická bezpečnost (Security):** *Safety* (dle ČSN EN ISO 13849-1) zajišťuje, že strojní zařízení nezpůsobí úraz člověku ani při vnitřní poruše řídicího systému (využívá redundantní obvody, bezpečnostní relé, optické závory, kategorii spolehlivosti PL a až PL e / SIL 3). *Security* řeší ochranu dat a systému před úmyslným napadením zvenčí (hackeři, malware).
> - **EMC (Elektromagnetická kompatibilita):** Schopnost zařízení spolehlivě pracovat v prostředí s elektromagnetickým rušením (odolnost / imunita) a současně nezpůsobovat nepřípustné rušení jiným zařízením (emise).
> 	Elektromagnetická kompatibilita. *Wikipedie: Otevřená encyklopedie* [online]. San Francisco (CA): Wikimedia Foundation, 2023, 2023-11-20 [cit. 2026-09-17]. Dostupné z: https://cs.wikipedia.org/wiki/Elektromagnetick%C3%A1_kompatibilita

<details>
<summary> :bulb: Tip k bezpečnostnímu okruhu (Safety): </summary>
<p>Základní pravidlo bezpečnosti: <strong>Software může selhat, zacyklit se nebo zamrznout.</strong> Bezpečnostní okruh nouzového zastavení (červený hřib) musí být vždy dvoukanálový, zapojený do hardwarového bezpečnostního relé (např. Pilz, Schneider Preventa, Siemens SIRIUS), které odpojí silové napájení stykačů ventilů přímo na hardwarové úrovni nezávisle na procesoru!</p>
</details>

:star2: **Bonusová otázka k úloze 5:**
Proč hobby reléové moduly s optočleny určené pro Arduino v průmyslovém rozváděči často shoří nebo způsobí trvalé sepnutí zátěže (tzv. přivaření kontaktů), i když jmenovitý proud relé je 10 A a cívka stykače odebírá jen 0,5 A?

*Vaše odpověď:*
Cívky stykačů představují silně **indukční zátěž (kategorie AC-15 / DC-13)**. Při rozpojení obvodu se indukuje vysoké napětí, které vytvoří silný elektrický oblouk. Levná hobby relé nemají zhášecí komory ani kontakty ze slitin stříbra (AgSnO2). Elektrický oblouk roztaví povrch kontaktů a způsobí jejich trvalé **přivaření (svaření)** k sobě, takže zátěž zůstane trvale pod napětím i po odpojení budicí cívky.

---

### 6. Rozšiřující inženýrská výzva: TCO a životní cyklus v automatizaci

*Časová dotace: 15–20 minut | :star2: Bonusová výzva pro pokročilé studenty*

V průmyslové automatizaci nákupní cena řídicí jednotky (CAPEX) často tvoří méně než 15 % celkových nákladů na životní cyklus zařízení (OPEX / TCO).

Představte si, že management firmy rozhoduje mezi dvěma variantami řízení pro sérii 50 kusů výrobních linek s plánovanou životností 15 let:
- **Varianta 1 (Nízkonákladová na pořízení):** Využití levných embedded mikrokontrolérových desek s vlastním zákaznickým návrhem plošného spoje (cena HW: 2 500 Kč / kus, vývoj firmwaru v C/C++ od externího programátora bez dokumentace).
- **Varianta 2 (Průmyslový standard):** Využití modulárního PLC renomovaného výrobce (Siemens / Rockwell / Schneider) s cenou 22 000 Kč / kus, programováno v normovaném jazyce LAD/ST dle IEC 61131-3.

#### Váš úkol:
1. Srovnejte obě varianty v níže uvedené tabulce a uveďte předpokládaná skrytá rizika a náklady v horizontu 10–15 let:

| Aspekt životního cyklu | Varianta 1 (Custom Embedded MCU) | Varianta 2 (Průmyslové PLC) |
| :--- | :--- | :--- |
| **Dostupnost náhradních dílů za 10 let** | **Nízká až nulová.** Ukončení výroby čipů (*obsolescence*), nutnost nového vývoje vlastního PCB od nuly. | **Garantovaná.** Průmysloví výrobci garantují dostupnost kompatibilních dílů po dobu 10–20 let. |
| **Servisovatelnost podnikovým elektrikářem** | **Nemožná.** Elektrikář nezná architekturu desky ani kód v C++ bez dokumentace od externisty. | **Snadná.** Běžný údržbář provádí diagnostiku v normovaném jazyce LAD/ST a výměnu modulů kus za kus. |
| **Doba odstávky linky při poruše CPU** | **Dny až týdny.** Čekání na vývojáře, výrobu nového PCB a nahrávání firmwaru. | **Minuty až hodiny.** Výměna vadného modulu ze skladu a nahrání programu z paměťové karty. |
| **Cena vývojových nástrojů a licencí IDE** | **Nízká / Zdarma.** Využití volně dostupného vývojového prostředí (Open-source IDE, GCC). | **Vyšší.** Jednorázový nákup inženýrského softwaru (např. Siemens TIA Portal). |
| **Závěrečné doporučení (kterou variantu vybrat a proč)** | **Nevhodné.** Obrovské riziko finančních ztrát z neplánovaných odstávek vysoce převýší úsporu při nákupu HW. | **DOPORUČENO.** Vyšší pořizovací cena (CAPEX) se vrátí v podobě nízkých provozních nákladů (OPEX) a spolehlivosti. |

> :key: **Vysvětlení pojmů a odborné zdroje:**
> - **CAPEX (Capital Expenditure)**: Zjednodušeně jde o jednorázové kapitálové výdaje na pořízení samotného zařízení (hardware, licence).
> - **OPEX (Operating Expense)**: Zjednodušeně jde o průběžné provozní náklady nutné k udržení zařízení v chodu (energie, servis, podpora).
> - **TCO (Total Cost of Ownership):** Finanční odhad celkových přímých i nepřímých nákladů spojených s pořízením, provozem, servisem, údržbou a likvidací produktu po celou dobu jeho životnosti. Zjednodušeně je to součet CAPEX + OPEX za celou dobu životnosti zařízení. 
> 	Total cost of ownership. *Wikipedia: The Free Encyclopedia* [online]. St. Petersburg (Florida): Wikimedia Foundation, 2024, 2024-08-14 [cit. 2026-09-17]. Dostupné z: https://en.wikipedia.org/wiki/Total_cost_of_ownership
> - **Vendor Lock-in:** Stav závislosti zákazníka na konkrétním dodavateli produktů nebo služeb, kdy je přechod k jiné platformě spojen s neúměrně vysokými finančními i časovými náklady.

<details>
<summary> :bulb: Tip k úvaze o TCO: </summary>
<p>Když za 7 let odejde custom deska z Varianty 1 a původní vývojář již ve firmě nepracuje a čip se nevyrábí, musí firma vyvinout celou řídicí elektroniku znovu od nuly. Hodina odstávky automobilové linky přitom stojí desítky až stovky tisíc korun.</p>
</details>

:star2: **Bonusová otázka k úloze 6:**
Co znamená pojem **MTBF (Mean Time Between Failures)** v datasheetech průmyslových řídicích jednotek a jaký vliv má okolní teplota v rozváděči na tuto hodnotu (tzv. Arrheniovo pravidlo)?

*Vaše odpověď:*
**MTBF (Střední doba mezi poruchami)** udává očekávanou provozní spolehlivost hardwaru vyjádřenou v hodinách. Podle **Arrheniova pravidla** (pravidlo 10 °C) vede každé zvýšení provozní teploty elektroniky o **10 °C ke zdvojnásobení rychlosti degradačních procesů** v součástkách (zejména v elektrolytických kondenzátorech a polovodičích). V praxi to znamená, že **zvýšení teploty uvnitř rozváděče o 10 °C zkrátí životnost a hodnotu MTBF řídicí jednotky přibližně na polovinu**.

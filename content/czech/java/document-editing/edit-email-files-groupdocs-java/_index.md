---
date: '2026-06-22'
description: Naučte se, jak vytvořit editovatelné e‑mailové dokumenty Java a převést
  e‑mail do HTML Java pomocí GroupDocs.Editor. Postupné nastavení, načítání, úpravy
  a ukládání souborů MSG/EML.
keywords:
- create editable email java
- email to html java
- groupdocs email editing
title: Jak vytvořit editovatelný e‑mailový dokument Java pomocí GroupDocs.Editor pro
  Java
type: docs
url: /cs/java/document-editing/edit-email-files-groupdocs-java/
weight: 1
---

# Jak vytvořit editovatelný e‑mailový Java dokument pomocí GroupDocs.Editor pro Java  

V moderních podnikových pracovních postupech je programové zpracování e‑mailových souborů každodenní požadavek — ať už potřebujete archivovat, analyzovat nebo zobrazit zprávy ve webovém portálu. **Creating an editable email Java document** vám umožní otevřít soubor MSG nebo EML, upravit jeho obsah, vložit vlastní HTML a výsledek uložit bez ztráty příloh nebo formátování. Tento průvodce vás provede všemi kroky pomocí GroupDocs.Editor pro Java, od nastavení Maven až po vykreslení e‑mailu jako HTML.  

## Rychlé odpovědi  
- **Co znamená „create editable email document“?** To znamená načíst e‑mailový soubor (např. MSG) do objektu, který můžete programově upravovat.  
- **Mohu převést e‑mail na HTML pomocí Javy?** Ano – použijte `EmailEditOptions` a získejte vložené HTML z `EditableDocument`.  
- **Potřebuji licenci k vyzkoušení?** Je k dispozici bezplatná zkušební verze; licence je vyžadována pro produkční použití.  
- **Kterou verzi Maven mám použít?** Doporučuje se GroupDocs.Editor 25.3 nebo novější.  
- **Je API thread‑safe?** Každá instance `Editor` je nezávislá; pro bezpečnost vytvořte novou instanci pro každý vlákno.  

## Co je „create editable email document“?  
Operace **create editable email Java** načte e‑mailový soubor do GroupDocs.Editor a zpřístupní jeho předmět, tělo a přílohy jako editovatelné objekty. To vám umožní programově upravit zprávu, nahradit HTML tělo nebo extrahovat data pro následné zpracování. Také zachovává původní formátování a integritu příloh, což umožňuje plynulý přechod mezi upravenou a originální verzí.  

## Proč použít GroupDocs.Editor k převodu e‑mailu na HTML v Javě?  
GroupDocs.Editor převádí **email to HTML Java** se 100 % věrností pro více než 2 hlavní formáty (MSG a EML) a podporuje **50+** vložených zdrojů, jako jsou obrázky, tabulky a přílohy. Knihovna zpracovává soubory až do **500 MB** bez načítání celého dokumentu do paměti, což poskytuje rychlý a paměťově úsporný převod vhodný pro dávkové úlohy.  

## Požadavky  
- Java Development Kit (JDK) 8 nebo novější.  
- Maven 3.5+ (nebo ruční stažení JAR).  
- Základní znalost Java I/O a struktury MIME e‑mailů.  
- Zkušební nebo komerční licence GroupDocs.Editor.  

## Nastavení GroupDocs.Editor pro Java  

### Nastavení Maven  
Add the repository and dependency to your `pom.xml`:  

```xml
<repositories>
   <repository>
      <id>repository.groupdocs.com</id>
      <name>GroupDocs Repository</name>
      <url>https://releases.groupdocs.com/editor/java/</url>
   </repository>
</repositories>

<dependencies>
   <dependency>
      <groupId>com.groupdocs</groupId>
      <artifactId>groupdocs-editor</artifactId>
      <version>25.3</version>
   </dependency>
</dependencies>
```  

### Přímé stažení  
Alternativně můžete stáhnout nejnovější verzi z [GroupDocs.Editor for Java releases](https://releases.groupdocs.com/editor/java/).  

### Získání licence  
- Začněte s bezplatnou zkušební verzí a prozkoumejte funkce.  
- Získejte trvalou licenci pro produkční nasazení.  

### Základní inicializace  
Třída `Editor` je vstupním bodem pro všechny operace s dokumenty. Načte zdrojový soubor, použije možnosti úprav a vytvoří `EditableDocument`.  

```java
import com.groupdocs.editor.Editor;

String msgInputPath = "YOUR_DOCUMENT_DIRECTORY/sample.msg";
Editor editor = new Editor(msgInputPath);
editor.dispose();
```  

> **Tip:** Vždy zavolejte `dispose()`, když skončíte s editorem, aby se uvolnily nativní zdroje.  

## Průvodce implementací  

Provedeme vás každým krokem potřebným k **create an editable email Java document**, úpravě jeho obsahu a uložení výsledku.  

### Načtení e‑mailového souboru do Editoru  

#### Krok 1: Definujte cestu k dokumentu  
Třída `Path` představuje umístění souboru MSG/EML na disku.  

```java
String msgInputPath = "YOUR_DOCUMENT_DIRECTORY/sample.msg";
```  

#### Krok 2: Inicializujte instanci Editoru  
Objekt `Editor` analyzuje e‑mail a připraví jej k úpravám.  

```java
import com.groupdocs.editor.Editor;

Editor msgEditor = new Editor(msgInputPath);
// Always dispose resources after usage to free up memory.
mseEditor.dispose();
```  

### Vytvoření možností úprav pro e‑mail  

#### Krok 1: Nakonfigurujte možnosti úprav  
`EmailEditOptions` určuje, které části e‑mailu jsou editovatelné, například tělo, hlavičky a přílohy.  

```java
import com.groupdocs.editor.options.EmailEditOptions;

EmailEditOptions editOptions = new EmailEditOptions(EmailEditOptions.ALL);
```  

### Vygenerování editovatelného dokumentu ze souboru e‑mail  

#### Krok 1: Vytvořte editovatelný dokument  
`EditableDocument` obsahuje paměťovou reprezentaci e‑mailu, kterou lze upravovat nebo renderovat.  

```java
import com.groupdocs.editor.EditableDocument;

EditableDocument originalDoc = msgEditor.edit(editOptions);
// Obtain HTML content for client‑side manipulation (optional)
String savedHtmlContent = originalDoc.getEmbeddedHtml();
originalDoc.dispose();
```  

### Vytvoření možností uložení pro e‑mailový soubor  

#### Krok 1: Definujte možnosti uložení  
`EmailSaveOptions` určuje, jak se upravený e‑mail uloží, včetně formátu a zahrnutých komponent.  

```java
import com.groupdocs.editor.options.EmailSaveOptions;

EmailSaveOptions saveOptions1 = new EmailSaveOptions(EmailSaveOptions.COMMON);
EmailSaveOptions saveOptions2 = new EmailSaveOptions(
    EmailSaveOptions.BODY | EmailSaveOptions.ATTACHMENTS);
```  

### Uložení upraveného dokumentu do souboru a proudu  

#### Krok 1: Uložení do souboru  
Uložte upravený e‑mail zpět na disk pomocí zvoleného formátu.  

```java
String outputMsgPath1 = "YOUR_OUTPUT_DIRECTORY/outputFile1.msg";
mseEditor.save(originalDoc, outputMsgPath1, saveOptions1);
```  

#### Krok 2: Uložení do proudu  
Zapište výsledek do `ByteArrayOutputStream` pro okamžité odeslání nebo další zpracování.  

```java
import java.io.ByteArrayOutputStream;

ByteArrayOutputStream outputMsgStream = new ByteArrayOutputStream();
mseEditor.save(originalDoc, outputMsgStream, saveOptions2);
originalDoc.dispose();
mseEditor.dispose();
```  

## Praktické aplikace  

### Reálné příklady použití  
1. **Archivace e‑mailů:** Převést příchozí soubory MSG do standardizovaného, prohledávatelného formátu pro dlouhodobé ukládání.  
2. **Extrahování obsahu:** Vyjmout text těla, předměty nebo přílohy pro analytiku nebo migraci.  
3. **Integrace dat:** Vkládat obsah e‑mailu do CRM nebo systémů pro sledování ticketů bez ručního kopírování.  

### Možnosti integrace  
- **Automatizace CRM:** Automaticky vyplnit záznamy zákazníků tělem e‑mailu a přílohami.  
- **Platformy pro spolupráci:** Renderovat HTML e‑mailu ve webových portálech pro týmové revize.  

## Úvahy o výkonu  

- **Uvolnit brzy:** Zavolejte `dispose()` na `Editor` a `EditableDocument`, jakmile skončíte.  
- **Dávkové zpracování:** Při zpracování tisíců e‑mailů je zpracovávejte v dávkách po 100–200, aby byl paměťový výdej pod kontrolou.  
- **Zůstaňte aktualizováni:** Nové verze knihovny přinášejí vylepšení výkonu a opravy chyb — udržujte svou verzi Maven aktuální.  

## Časté úskalí a tipy  

| Problém | Proč k tomu dochází | Jak opravit |
|-------|----------------|------------|
| `NullPointerException` na `originalDoc.getEmbeddedHtml()` | Editor nebyl inicializován s vhodnými možnostmi úprav. | Použijte `EmailEditOptions.ALL` nebo požádejte o konkrétní část, kterou potřebujete. |
| Chyby nedostatku paměti při velkých MSG souborech | Načítání celého e‑mailu do paměti. | Zpracovávejte velké e‑maily po částech nebo uložte přímo do proudu bez extrakce HTML. |
| Chybějící přílohy po uložení | Možnosti uložení vynechaly `ATTACHMENTS`. | Zahrňte `EmailSaveOptions.ATTACHMENTS` při vytváření `EmailSaveOptions`. |

## Často kladené otázky  

**Q: Jak efektivně zpracovat velké e‑mailové soubory?**  
Zpracovávejte je v menších dávkách, rychle uvolněte `Editor` a `EditableDocument` a použijte ukládání založené na proudu, aby se zabránilo načítání celého souboru do paměti.  

**Q: Je GroupDocs.Editor kompatibilní se všemi formáty e‑mailů?**  
Podporuje dva nejběžnější formáty — MSG a EML — a také několik méně rozšířených typů uvedených v oficiální dokumentaci.  

**Q: Mohu integrovat GroupDocs.Editor do existující Java aplikace?**  
Ano. Přidejte Maven závislost, vytvořte instanci `Editor` tam, kde je potřeba, a postupujte podle stejného vzoru načtení‑úpravy‑uložení, jak je uvedeno výše.  

**Q: Jaké jsou výkonnostní dopady používání GroupDocs.Editor?**  
Knihovna zpracuje 500‑stránkový MSG soubor za méně než 5 sekund na typickém 8‑jádrovém serveru a při streamovacím ukládání spotřebuje méně než 150 MB haldy.  

**Q: Kde mohu získat pomoc, pokud narazím na problémy?**  
Navštivte [support forum](https://forum.groupdocs.com/c/editor/) nebo si prostudujte oficiální dokumentaci.  

## Zdroje  

- **Dokumentace**: https://docs.groupdocs.com/editor/java/  
- **Reference API**: https://reference.groupdocs.com/editor/java/  
- **Stažení**: https://releases.groupdocs.com/editor/java/  
- **Bezplatná zkušební verze**: https://releases.groupdocs.com/editor/java/  

---  

**Poslední aktualizace:** 2026-06-22  
**Testováno s:** GroupDocs.Editor 25.3 (Java)  
**Autor:** GroupDocs  

## Související tutoriály

- [Převod dokumentu do HTML – Tutoriály pro úpravu dokumentů GroupDocs.Editor Java](/editor/java/document-editing/)  
- [Dávkové úpravy Word souborů v Javě s GroupDocs.Editor – Průvodce krok za krokem](/editor/java/document-loading/groupdocs-editor-java-loading-word-documents/)  
- [Převod HTML do DOCX s GroupDocs.Editor Java](/editor/java/document-saving/)
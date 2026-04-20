---
date: 2026-04-20
description: Leer hoe u een met wachtwoord beveiligd document kunt laden met GroupDocs.Editor
  voor .NET, inclusief laden vanaf een bestandspad, vanaf een byte‑stroom en vanuit
  een database.
keywords:
- load password protected document
- load document from stream
- load document from database
linktitle: Document met wachtwoordbeveiliging laden
second_title: GroupDocs.Editor .NET API
title: Laad wachtwoordbeveiligd document met GroupDocs.Editor .NET
type: docs
url: /nl/net/document-editing/load-document/
weight: 13
---

# Laad wachtwoordbeveiligd document met GroupDocs.Editor .NET

## Inleiding
Programmeren van documenten bewerken kan overweldigend aanvoelen, vooral wanneer je **wachtwoordbeveiligd document laden** moet doen die zich op verschillende locaties bevinden. Of het bestand zich op schijf bevindt, afkomstig is van een byte‑stroom, of opgeslagen is in een database, GroupDocs.Editor voor .NET biedt een schone, consistente API om al deze scenario's af te handelen. In deze gids lopen we de vereisten door, importeren we de benodigde namespaces, en laten we stap‑voor‑stap zien hoe je documenten kunt laden met verschillende methoden — inclusief het speciale geval van wachtwoordbeveiligde bestanden.

## Snelle antwoorden
- **Kan GroupDocs.Editor wachtwoordbeveiligde bestanden openen?** Ja, gebruik de juiste laadopties met het ingestelde wachtwoord.  
- **Welke .NET‑versies worden ondersteund?** .NET Framework 2.0+ en .NET Core/5/6 zijn allemaal compatibel.  
- **Moet ik het Editor‑object opruimen?** Absoluut—roep `Dispose()` aan om bronnen vrij te geven.  
- **Kan ik een document uit een database laden?** Ja, haal het bestand op als een byte‑array of stream en geef het door aan de `Editor`‑constructor.  
- **Is er een limiet op de bestandsgrootte?** Grote bestanden worden ondersteund; overweeg stream‑gebaseerd laden met geheugen‑optimaliserende opties.

## Wat is “wachtwoordbeveiligd document laden”?
Het laden van een wachtwoordbeveiligd document betekent het openen van een bestand dat een wachtwoord vereist voor toegang, en vervolgens dat wachtwoord programmatisch verstrekken zodat de API kan ontcijferen en met de inhoud kan werken. GroupDocs.Editor abstraheert de ontsleutelingsstap via laadopties, waardoor het proces eenvoudig wordt.

## Waarom GroupDocs.Editor gebruiken voor het laden van documenten?
- **Unified API** – dezelfde code werkt voor Word-, Excel-, PowerPoint- en HTML‑bestanden.  
- **Password handling** – ingebouwde ondersteuning voor versleutelde bestanden zonder handmatige ontsleuteling.  
- **Stream flexibility** – laden vanaf bestandspaden, streams of elke aangepaste bron zoals een database.  
- **Resource management** – eenvoudig `Dispose()`‑patroon houdt het geheugenverbruik laag.

## Vereisten
Voordat we beginnen, zorg ervoor dat je de volgende vereisten hebt ingesteld:
- **Visual Studio** – Zorg ervoor dat Visual Studio op je machine geïnstalleerd is.  
- **.NET Framework** – GroupDocs.Editor voor .NET ondersteunt .NET Framework 2.0 of later. Zorg ervoor dat je project een compatibel framework target.  
- **GroupDocs.Editor for .NET** – Download de nieuwste versie van de [downloadpagina](https://releases.groupdocs.com/editor/net/).  
- **Basiskennis van C#** – Vertrouwdheid met C# en .NET‑programmeren is nodig om deze tutorial te volgen.

## Namespaces importeren
Om GroupDocs.Editor voor .NET te gebruiken, moet je de benodigde namespaces in je project importeren. Voeg de volgende using‑directieven toe aan de bovenkant van je C#‑bestand:

```csharp
using GroupDocs.Editor.Options;
using System.IO;
```

Deze namespaces geven toegang tot de klassen en methoden die nodig zijn voor documentbewerkings‑taken.

## Stap 1: Document laden vanaf een bestandspad
Een document laden vanaf een bestandspad is eenvoudig. Deze methode is ideaal voor documenten die lokaal op je machine zijn opgeslagen.

```csharp
string inputPath = "Your Sample Document";
// Load document as file via path and without load options
Editor editor1 = new Editor(inputPath);
// Dispose resources
editor1.Dispose();
System.Console.WriteLine("Document loaded successfully from file path.");
```

## Stap 2: Document laden met laadopties (wachtwoordbeveiligde bestanden)
Soms moet je documenten laden die speciale behandeling vereisen, zoals wachtwoordbeveiligde bestanden. In dat geval kun je laadopties gebruiken.

```csharp
string inputPath = "Your Sample Document";
// Create load options for Word documents
WordProcessingLoadOptions wordLoadOptions = new WordProcessingLoadOptions();
wordLoadOptions.Password = "some password";
// Load document as file via path and with load options
Editor editor2 = new Editor(inputPath, delegate { return wordLoadOptions; });
// Dispose resources
editor2.Dispose();
System.Console.WriteLine("Password-protected document loaded successfully.");
```

## Hoe een document laden vanuit een stream
Een document laden vanuit een byte‑stroom is handig wanneer je documenten moet verwerken die niet als bestanden zijn opgeslagen, zoals die opgehaald uit een database of een webservice.

```csharp
FileStream inputStream = File.OpenRead("Your Sample Document");
// Load document as content from byte stream and without load options
Editor editor3 = new Editor(delegate { return inputStream; });
// Dispose resources
editor3.Dispose();
System.Console.WriteLine("Document loaded successfully from byte stream.");
```

## Stap 4: Document laden met laadopties vanuit een byte‑stream
Voor documenten die speciale behandeling nodig hebben bij het laden vanuit een byte‑stroom, kun je byte‑stroom‑laden combineren met laadopties.

```csharp
FileStream inputStream = File.OpenRead("Your Sample Document");
// Create load options for spreadsheets
SpreadsheetLoadOptions sheetLoadOptions = new SpreadsheetLoadOptions();
sheetLoadOptions.OptimizeMemoryUsage = true;
// Load document as content from byte stream and with load options
Editor editor4 = new Editor(delegate { return inputStream; }, delegate { return sheetLoadOptions; });
// Dispose resources
editor4.Dispose();
System.Console.WriteLine("Spreadsheet document loaded successfully with load options.");
```

## Hoe een document laden vanuit een database
Als je documenten zijn opgeslagen in een relationele database, haal dan de binaire gegevens op (bijv. met `SELECT FileData FROM Documents WHERE Id = @id`) en geef de resulterende `byte[]` of `MemoryStream` door aan de `Editor`‑constructor, net als in het stream‑voorbeeld hierboven. Dit houdt je code consistent, ongeacht de bron.

## Veelvoorkomende problemen en oplossingen
- **Onjuist wachtwoord** – De editor zal een uitzondering gooien. Controleer de wachtwoordwaarde en zorg ervoor dat je de juiste laadopties‑klasse voor het bestandstype gebruikt.  
- **Stream al gesloten** – Zorg ervoor dat de stream open blijft gedurende de levensduur van de `Editor`‑instantie, of kopieer de stream naar een `MemoryStream`.  
- **Geheugengebruik bij grote bestanden** – Gebruik `SpreadsheetLoadOptions.OptimizeMemoryUsage = true` (zoals getoond) of equivalente opties voor andere formaten.

## Veelgestelde vragen

**Q: Welke bestandsformaten worden ondersteund door GroupDocs.Editor voor .NET?**  
A: GroupDocs.Editor ondersteunt een breed scala aan bestandsformaten, waaronder DOCX, XLSX, PPTX, HTML en nog veel meer. Voor een volledige lijst, zie de [documentatie](https://tutorials.groupdocs.com/editor/net/).

**Q: Hoe ga ik om met wachtwoordbeveiligde documenten?**  
A: Je kunt laadopties gebruiken zoals `WordProcessingLoadOptions` om het wachtwoord op te geven bij het laden van wachtwoordbeveiligde documenten.

**Q: Kan ik GroupDocs.Editor gebruiken in een webapplicatie?**  
A: Ja, GroupDocs.Editor kan worden gebruikt in webapplicaties. Zorg ervoor dat je bestands‑streams en resource‑opruiming correct afhandelt om geheugenlekken te voorkomen.

**Q: Waar kan ik een tijdelijke licentie voor GroupDocs.Editor krijgen?**  
A: Je kunt een tijdelijke licentie verkrijgen via de [tijdelijke licentiepagina](https://purchase.groupdocs.com/temporary-license/).

**Q: Is er ondersteuning beschikbaar als ik problemen ondervind?**  
A: Ja, GroupDocs biedt ondersteuning via hun [ondersteuningsforum](https://forum.groupdocs.com/c/editor/20).

**Q: Vereist het laden vanuit een database speciale configuratie?**  
A: Er is geen speciale configuratie nodig, behalve het ophalen van de binaire gegevens en deze doorgeven als een stream of byte‑array aan de `Editor`‑constructor.

**Q: Hoe kan ik de prestaties verbeteren bij het laden van zeer grote spreadsheets?**  
A: Schakel geheugen‑optimaliserende opties in, zoals `SpreadsheetLoadOptions.OptimizeMemoryUsage = true`, om de geheugengebruik te verminderen.

## Conclusie
Gefeliciteerd! Je hebt met succes geleerd hoe je **wachtwoordbeveiligde documenten** kunt laden met GroupDocs.Editor voor .NET op verschillende manieren. Of je nu werkt met lokale bestanden, wachtwoordbeveiligde documenten, byte‑streams of in een database opgeslagen inhoud, GroupDocs.Editor biedt een flexibele en krachtige oplossing voor je documentbewerkingsbehoeften. Vergeet niet altijd de `Editor`‑instantie op te ruimen om je applicatie performant en resource‑efficiënt te houden.

---

**Last Updated:** 2026-04-20  
**Tested With:** GroupDocs.Editor 2.0 (latest)  
**Author:** GroupDocs
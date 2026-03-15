# MCP Osnovni Koncepti: Ovladavanje Protokolom Modelnog Konteksta za AI Integraciju

[![MCP Osnovni Koncepti](../../../translated_images/hr/02.8203e26c6fb5a797.webp)](https://youtu.be/earDzWGtE84)

_(Kliknite na gornju sliku za pregled videa ovog sata)_

[Model Context Protocol (MCP)](https://github.com/modelcontextprotocol) je moćan, standardizirani okvir koji optimizira komunikaciju između Velikih Jezičnih Modela (LLM) i vanjskih alata, aplikacija i izvora podataka.  
Ovaj vodič će vas provesti kroz osnovne koncepte MCP-a. Naučit ćete o njegovoj arhitekturi klijent-poslužitelj, ključnim komponentama, mehanizmima komunikacije i najboljim praksama implementacije.

- **Izričiti pristanak korisnika**: Sav pristup podacima i operacije zahtijevaju izričitu korisničku suglasnost prije izvršenja. Korisnici moraju jasno razumjeti koji se podaci pristupaju i koje se radnje izvode, s granularnom kontrolom nad dozvolama i ovlastima.

- **Zaštita privatnosti podataka**: Korisnički podaci izlažu se samo uz izričitu suglasnost i moraju biti zaštićeni robusnom kontrolom pristupa tijekom cijelog životnog ciklusa interakcije. Implementacije moraju sprječavati neovlašteni prijenos podataka i održavati stroga pravila privatnosti.

- **Sigurnost izvršavanja alata**: Svako pokretanje alata zahtijeva izričitu suglasnost korisnika s jasnim razumijevanjem funkcionalnosti alata, parametara i potencijalnog utjecaja. Robusne sigurnosne granice moraju spriječiti neželjeno, nesigurno ili zlonamjerno izvršavanje alata.

- **Sigurnost sloja prijenosa**: Svi komunikacijski kanali trebaju koristiti odgovarajuće mehanizme enkripcije i autentifikacije. Udaljene veze trebaju implementirati sigurne protokole prijenosa i pravilno upravljanje vjerodajnicama.

#### Smjernice za implementaciju:

- **Upravljanje dopuštenjima**: Implementirajte sustave finog upravljanja dozvolama koji omogućuju korisnicima kontrolu pristupa poslužiteljima, alatima i resursima  
- **Provjera autentičnosti i autorizacija**: Koristite sigurne metode autentifikacije (OAuth, API ključevi) s pravilnim upravljanjem tokenima i istekom  
- **Validacija unosa**: Validirajte sve parametre i ulaze podataka prema definiranim shemama kako biste spriječili napade ubrizgavanja  
- **Evidentiranje nadzora**: Održavajte opsežne zapisnike svih operacija za sigurnosno praćenje i usklađenost  

## Pregled

Ovaj sat istražuje temeljnu arhitekturu i komponente koje čine ekosustav Model Context Protocol-a (MCP). Naučit ćete o arhitekturi klijent-poslužitelj, ključnim komponentama i komunikacijskim mehanizmima koji pokreću MCP interakcije.

## Ključni ciljevi učenja

Do kraja ovog sata vi ćete:

- Razumjeti MCP arhitekturu klijent-poslužitelj.  
- Identificirati uloge i odgovornosti Hostova, Klijenata i Poslužitelja.  
- Analizirati ključne značajke koje čine MCP fleksibilnim slojem za integraciju.  
- Naučiti kako informacije teku unutar MCP ekosustava.  
- Steći praktične uvide kroz primjere koda u .NET, Javi, Pythonu i JavaScriptu.

## MCP Arhitektura: Dubinski pogled

MCP ekosustav baziran je na modelu klijent-poslužitelj. Ova modularna struktura omogućuje AI aplikacijama učinkovitu interakciju s alatima, bazama podataka, API-ima i kontekstualnim resursima. Razložimo ovu arhitekturu na njezine osnovne komponente.

U svojoj je osnovi MCP arhitektura klijent-poslužitelj gdje host aplikacija može uspostaviti veze s više poslužitelja:

```mermaid
flowchart LR
    subgraph "Vaše Računalo"
        Host["Domaćin s MCP (Visual Studio, VS Code, IDE-i, Alati)"]
        S1["MCP Poslužitelj A"]
        S2["MCP Poslužitelj B"]
        S3["MCP Poslužitelj C"]
        Host <-->|"MCP Protokol"| S1
        Host <-->|"MCP Protokol"| S2
        Host <-->|"MCP Protokol"| S3
        S1 <--> D1[("Lokalni\Izvor Podataka A")]
        S2 <--> D2[("Lokalni\Izvor Podataka B")]
    end
    subgraph "Internet"
        S3 <-->|"Web API-ji"| D3[("Udaljene\Usluge")]
    end
```
- **MCP Hostovi**: Programi poput VSCode, Claude Desktop, IDE-a ili AI alata koji žele pristupiti podacima preko MCP-a  
- **MCP Klijenti**: Klijenti protokola koji održavaju 1:1 veze s poslužiteljima  
- **MCP Poslužitelji**: Laki programi koji svaki izlažu specifične mogućnosti putem standardiziranog Model Context Protocol-a  
- **Lokalni izvori podataka**: Datoteke, baze podataka i servisi na vašem računalu kojima MCP poslužitelji mogu sigurno pristupiti  
- **Udaljene usluge**: Vanjski sustavi dostupni preko interneta s kojima se MCP poslužitelji mogu povezati putem API-ja.

MCP Protokol je standard u razvoju koji koristi verzioniranje temeljeno na datumu (format YYYY-MM-DD). Trenutna verzija protokola je **2025-11-25**. Najnovije izmjene možete vidjeti u [specifikaciji protokola](https://modelcontextprotocol.io/specification/2025-11-25/)

### 1. Hostovi

U Model Context Protocolu (MCP), **Hostovi** su AI aplikacije koje služe kao primarno sučelje kroz koje korisnici komuniciraju s protokolom. Hostovi koordiniraju i upravljaju vezama s više MCP poslužitelja stvaranjem zasebnih MCP klijenata za svaku poslužiteljsku vezu. Primjeri Hostova su:

- **AI aplikacije**: Claude Desktop, Visual Studio Code, Claude Code  
- **Razvojna okruženja**: IDE-i i uređivači koda s MCP integracijom  
- **Prilagođene aplikacije**: Specijalizirani AI agenti i alati

**Hostovi** su aplikacije koje koordiniraju interakcije AI modela. Oni:

- **Orkestriraju AI modele**: Izvršavaju ili komuniciraju s LLM-ovima kako bi generirali odgovore i koordinirali AI tijekove rada  
- **Upravljaju klijentskim vezama**: Stvaraju i održavaju po jednog MCP klijenta za svaku vezu prema MCP poslužitelju  
- **Kontroliraju korisničko sučelje**: Rukovode tokom razgovora, korisničkim interakcijama i prikazom odgovora  
- **Provode sigurnost**: Kontroliraju dozvole, sigurnosne restrikcije i autentifikaciju  
- **Rukovode korisničkim pristankom**: Upravljaju dozvolama za dijeljenje podataka i izvršenje alata  


### 2. Klijenti

**Klijenti** su ključne komponente koje održavaju posvećene jedan-na-jedan veze između Hostova i MCP poslužitelja. Svaki MCP klijent inicijalizira se od strane Host aplikacije za povezivanje s određenim MCP poslužiteljem, osiguravajući organizirane i sigurne kanale komunikacije. Više klijenata omogućuje Hostovima istovremeno povezivanje na više poslužitelja.

**Klijenti** su spojne komponente unutar host aplikacije. Oni:

- **Komunikacija protokolom**: Šalju JSON-RPC 2.0 zahtjeve poslužiteljima s promptovima i uputama  
- **Pregovaranje mogućnosti**: Pregovaraju podržane značajke i verzije protokola s poslužiteljima pri inicijalizaciji  
- **Izvršavanje alata**: Upravljaju zahtjevima za izvršenje alata od modela i procesuiraju odgovore  
- **Ažuriranja u stvarnom vremenu**: Rukovode notifikacijama i ažuriranjima u stvarnom vremenu od poslužitelja  
- **Obrada odgovora**: Procesuiraju i oblikuju odgovore poslužitelja za prikaz korisnicima  

### 3. Poslužitelji

**Poslužitelji** su programi koji pružaju kontekst, alate i sposobnosti MCP klijentima. Oni mogu raditi lokalno (na istom računalu kao Host) ili udaljeno (na vanjskim platformama) i odgovorni su za rukovanje zahtjevima klijenata te pružanje strukturiranih odgovora. Poslužitelji izlažu specifične funkcionalnosti putem standardiziranog Model Context Protocol-a.

**Poslužitelji** su servisi koji pružaju kontekst i sposobnosti. Oni:

- **Registracija značajki**: Registriraju i izlažu dostupne primitivne resurse (resurse, promtove, alate) klijentima  
- **Obrada zahtjeva**: Primaju i izvršavaju pozive alata, zahtjeve za resurse i zahtjeve promptova od klijenata  
- **Dostava konteksta**: Pružaju kontekstualne informacije i podatke za poboljšanje odgovora modela  
- **Upravljanje stanjem**: Održavaju stanje sesije i rukovode interakcijama sa stanjem po potrebi  
- **Notifikacije u stvarnom vremenu**: Šalju obavijesti o promjenama mogućnosti i ažuriranjima povezanim klijentima  

Poslužitelji mogu biti razvijeni od strane bilo koga kako bi proširili mogućnosti modela specijaliziranim funkcionalnostima, i podržavaju i lokalne i udaljene scenarije implementacije.

### 4. Poslužiteljske primitivne jedinice

Poslužitelji u Model Context Protocolu (MCP) pružaju tri osnovne **primitivne jedinice** koje definiraju temeljne građevne blokove za bogate interakcije između klijenata, hostova i jezičnih modela. Ove primitivne jedinice specificiraju vrste kontekstualnih informacija i radnji dostupnih putem protokola.

MCP poslužitelji mogu izlagati bilo koju kombinaciju sljedeće tri osnovne primitivne jedinice:

#### Resursi

**Resursi** su izvori podataka koji pružaju kontekstualne informacije AI aplikacijama. Predstavljaju statički ili dinamički sadržaj koji može unaprijediti razumijevanje modela i donošenje odluka:

- **Kontekstualni podaci**: Strukturirane informacije i kontekst za konzumaciju AI modela  
- **Baze znanja**: Repozitoriji dokumenata, članci, priručnici i istraživački radovi  
- **Lokalni izvori podataka**: Datoteke, baze podataka i lokalne sistemske informacije  
- **Vanjski podaci**: API odgovori, web servisi i podaci udaljenih sustava  
- **Dinamički sadržaj**: Podaci u stvarnom vremenu koji se ažuriraju na temelju vanjskih uvjeta

Resursi se identificiraju URI-jevima i podržavaju otkrivanje putem `resources/list` i dohvat putem `resources/read` metoda:

```text
file://documents/project-spec.md
database://production/users/schema
api://weather/current
```

#### Prompti

**Prompti** su predlošci koji se mogu višekratno koristiti za strukturiranje interakcija s jezičnim modelima. Oni pružaju standardizirane obrasce interakcije i predloške tijeka rada:

- **Interakcije temeljene na predlošcima**: Unaprijed strukturirane poruke i početci razgovora  
- **Predlošci tijeka rada**: Standardizirani slijedovi za uobičajene zadatke i interakcije  
- **Few-shot primjeri**: Primjeri temeljen na predlošcima za upute modelu  
- **Sistemski prompti**: Temeljni prompti koji definiraju ponašanje modela i kontekst  
- **Dinamički predlošci**: Parametrizirani prompti koji se prilagođavaju specifičnim kontekstima  

Prompti podržavaju zamjenu varijabli i mogu se otkriti putem `prompts/list` te dohvatiti pomoću `prompts/get`:

```markdown
Generate a {{task_type}} for {{product}} targeting {{audience}} with the following requirements: {{requirements}}
```

#### Alati

**Alati** su izvršne funkcije koje AI modeli mogu pozivati za obavljanje specifičnih radnji. Predstavljaju "glagole" MCP ekosustava, omogućujući modelima interakciju s vanjskim sustavima:

- **Izvršne funkcije**: Diskretne operacije koje modeli mogu pozvati s određenim parametrima  
- **Integracija s vanjskim sustavima**: API pozivi, upiti baza podataka, rad s datotekama, izračuni  
- **Jedinstveni identitet**: Svaki alat ima jedinstveno ime, opis i shemu parametara  
- **Strukturirani ulaz/izlaz**: Alati prihvaćaju validirane parametre i vraćaju strukturirane, tipizirane odgovore  
- **Sposobnosti akcija**: Omogućuju modelima izvođenje radnji u stvarnom svijetu i dohvat aktualnih podataka  

Alati se definiraju JSON Shemom za validaciju parametara i otkrivaju kroz `tools/list`, a izvršavaju putem `tools/call`. Alati također mogu sadržavati **ikone** kao dodatne metapodatke za bolji vizualni prikaz.

**Podnaslovi za alate**: Alati podržavaju opisne oznake ponašanja (npr. `readOnlyHint`, `destructiveHint`) koje upućuju je li alat samo za čitanje ili destruktivan, pomažući klijentima u donošenju informiranih odluka o njihovom izvršavanju.

Primjer definicije alata:

```typescript
server.tool(
  "search_products", 
  {
    query: z.string().describe("Search query for products"),
    category: z.string().optional().describe("Product category filter"),
    max_results: z.number().default(10).describe("Maximum results to return")
  }, 
  async (params) => {
    // Izvrši pretraživanje i vrati strukturirane rezultate
    return await productService.search(params);
  }
);
```

## Klijentske primitivne jedinice

U Model Context Protocolu (MCP), **klijenti** mogu izlagati primitivne jedinice koje omogućuju poslužiteljima da zatraže dodatne mogućnosti od host aplikacije. Ove klijentske primitivne jedinice omogućuju bogatije, interaktivnije implementacije poslužitelja koje mogu pristupiti sposobnostima AI modela i korisničkim interakcijama.

### Uzorkovanje (Sampling)

**Uzorkovanje** omogućuje poslužiteljima da zatraže završetke jezičnog modela iz AI aplikacije klijenta. Ova primitivna jedinica omogućuje poslužiteljima pristup LLM sposobnostima bez ugrađivanja vlastitih ovisnosti o modelima:

- **Pristup neovisno o modelu**: Poslužitelji mogu zatražiti završetke bez uključivanja LLM SDK-ova ili upravljanja pristupom modelima  
- **AI iniciran od strane poslužitelja**: Omogućuje poslužiteljima autonomno generiranje sadržaja koristeći model klijenta  
- **Rekurzivne LLM interakcije**: Podržava složene scenarije gdje poslužitelji trebaju AI pomoć pri obradi  
- **Dinamička generacija sadržaja**: Omogućuje poslužiteljima kreiranje kontekstualnih odgovora koristeći model hosta  
- **Podrška za pozivanje alata**: Poslužitelji mogu uključiti `tools` i `toolChoice` parametre za omogućavanje pozivanja alata tijekom uzorkovanja

Uzorkovanje se inicira metodom `sampling/complete`, gdje poslužitelji šalju zahtjeve za završetke klijentima.

### Korijeni (Roots)

**Korijeni** pružaju standardizirani način za klijente da izlože granice datotečnog sustava poslužiteljima, pomažući poslužiteljima razumjeti koje direktorije i datoteke imaju pravo pristupa:

- **Granice datotečnog sustava**: Definiraju granice unutar kojih poslužitelji mogu raditi u datotečnom sustavu  
- **Kontrola pristupa**: Pomažu poslužiteljima da razumiju kojim direktorijima i datotekama imaju dopuštenje pristupa  
- **Dinamička ažuriranja**: Klijenti mogu obavijestiti poslužitelje kada se lista korijena promijeni  
- **Identifikacija temeljem URI-ja**: Korijeni koriste `file://` URI-je za identifikaciju dostupnih direktorija i datoteka  

Korijeni se otkrivaju putem metode `roots/list`, a klijenti šalju `notifications/roots/list_changed` kada korijeni promijene.

### Ispitivanje (Elicitation)

**Ispitivanje** omogućuje poslužiteljima da zatraže dodatne informacije ili potvrdu od korisnika putem klijentskog sučelja:

- **Zahtjevi za unos korisnika**: Poslužitelji mogu zatražiti dodatne informacije kada su potrebne za izvršenje alata  
- **Dijalozi za potvrdu**: Zahtijevaju odobrenje korisnika za osjetljive ili značajne operacije  
- **Interaktivni tijekovi rada**: Omogućuju poslužiteljima stvaranje korak-po-korak interakcija s korisnikom  
- **Dinamičko prikupljanje parametara**: Prikupljanje nedostajućih ili opcionalnih parametara tijekom izvršavanja alata  

Zahtjevi ispitivanja šalju se metodom `elicitation/request` kako bi se prikupili korisnički podaci putem sučelja klijenta.

**Ispitivanje putem URL načina**: Poslužitelji također mogu zatražiti korisničke interakcije temeljene na URL-u, omogućujući im usmjeravanje korisnika na vanjske web stranice za autentifikaciju, potvrdu ili unos podataka.

### Evidentiranje (Logging)

**Evidentiranje** omogućuje poslužiteljima slanje strukturiranih zapisničkih poruka klijentima radi otklanjanja pogrešaka, nadzora i operativne vidljivosti:

- **Podrška za otklanjanje pogrešaka**: Omogućuje poslužiteljima da pruže detaljne zapise izvršenja za rješavanje problema  
- **Operativni nadzor**: Šalje klijentima statuse i metrike izvedbe  
- **Prijava pogrešaka**: Pruža detaljan kontekst pogrešaka i dijagnostičke informacije  
- **Revizijski zapisi**: Stvara opsežne zapise poslužiteljskih operacija i odluka  

Poruke evidentiranja šalju se klijentima radi pružanja transparentnosti u rad poslužitelja i olakšavanja otklanjanja pogrešaka.

## Tok informacija u MCP-u

Model Context Protocol (MCP) definira strukturirani tok informacija između hostova, klijenata, poslužitelja i modela. Razumijevanje tog toka pomaže u razjašnjavanju kako se procesiraju korisnički zahtjevi i kako se vanjski alati i podaci integriraju u odgovore modela.
- **Host inicira vezu**  
  Host aplikacija (kao što je IDE ili chat sučelje) uspostavlja vezu s MCP serverom, obično putem STDIO, WebSocket ili nekog drugog podržanog transporta.

- **Pregovaranje o mogućnostima**  
  Klijent (ugrađen u host) i server razmjenjuju informacije o svojim podržanim značajkama, alatima, resursima i verzijama protokola. Ovo osigurava da obje strane razumiju koje su mogućnosti dostupne za sesiju.

- **Korisnički zahtjev**  
  Korisnik komunicira s hostom (npr. unosi upit ili naredbu). Host prikuplja ovaj unos i prosljeđuje ga klijentu na obradu.

- **Korištenje resursa ili alata**  
  - Klijent može zatražiti dodatni kontekst ili resurse od servera (kao što su datoteke, unosi baze podataka ili članci baze znanja) kako bi obogatio razumijevanje modela.  
  - Ako model utvrdi da je potreban alat (npr. za dohvat podataka, izvođenje izračuna ili pozivanje API-ja), klijent šalje zahtjev za pokretanje alata serveru, navodeći ime alata i parametre.

- **Izvršavanje na serveru**  
  Server prima zahtjev za resursom ili alatom, izvršava potrebne radnje (kao što su pokretanje funkcije, upit prema bazi podataka ili dohvat datoteke) i vraća rezultate klijentu u strukturiranom formatu.

- **Generiranje odgovora**  
  Klijent integrira odgovore servera (podatke resursa, izlaze alata itd.) u tijek interakcije s modelom. Model koristi ove informacije za generiranje sveobuhvatnog i kontekstualno relevantnog odgovora.

- **Prikaz rezultata**  
  Host prima konačni izlaz od klijenta i prezentira ga korisniku, često uključujući kako tekst generiran modelom tako i bilo kakve rezultate izvršenja alata ili traženja u resursima.

Ovaj proces omogućava MCP da podrži napredne, interaktivne i kontekstno osviještene AI aplikacije besprijekornim povezivanjem modela s vanjskim alatima i izvorima podataka.

## Arhitektura protokola i slojevi

MCP se sastoji od dva zasebna arhitektonska sloja koja zajedno rade na pružanju potpunog komunikacijskog okvira:

### Sloj podataka

**Sloj podataka** implementira osnovni MCP protokol koristeći **JSON-RPC 2.0** kao temelj. Ovaj sloj definira strukturu poruka, semantiku i obrasce interakcija:

#### Ključne komponente:

- **JSON-RPC 2.0 protokol**: Sva komunikacija koristi standardizirani JSON-RPC 2.0 format poruka za pozive metoda, odgovore i notifikacije  
- **Upravljanje životnim ciklusom**: Rukuje inicijalizacijom veze, pregovaranjem o mogućnostima i završetkom sesije između klijenata i servera  
- **Server primitivci**: Omogućuje serverima pružanje osnovne funkcionalnosti kroz alate, resurse i promptove  
- **Klijent primitivci**: Omogućuje serverima zahtjev za generiranjem uzorka (sampling) iz LLM-a, traženjem korisničkog unosa i slanje zapisnika  
- **Notifikacije u stvarnom vremenu**: Podržava asinkrone notifikacije za dinamičke nadopune bez upitavanja

#### Ključne značajke:

- **Pregovaranje o verziji protokola**: Koristi verzije temeljene na datumu (GGGG-MM-DD) za osiguranje kompatibilnosti  
- **Otkrivanje mogućnosti**: Klijenti i serveri razmjenjuju informacije o podržanim značajkama tijekom inicijalizacije  
- **Stanje sesije**: Održava status veze kroz više interakcija radi kontinuiteta konteksta

### Transportni sloj

**Transportni sloj** upravlja komunikacijskim kanalima, formatiranjem poruka i autentifikacijom između sudionika MCP-a:

#### Podržani transportni mehanizmi:

1. **STDIO transport**:  
   - Koristi standardne ulazno/izlazne tokove za direktnu komunikaciju procesa  
   - Optimalno za lokalne procese na istom računalu bez mrežnog opterećenja  
   - Često se koristi za lokalne MCP server implementacije  

2. **Streamable HTTP transport**:  
   - Koristi HTTP POST za poruke klijent–server  
   - Opcionalni Server-Sent Events (SSE) za streamanje server–klijent  
   - Omogućava udaljenu komunikaciju servera preko mreža  
   - Podržava standardnu HTTP autentifikaciju (bearer tokeni, API ključevi, prilagođeni headeri)  
   - MCP preporučuje OAuth za sigurnu autentifikaciju temeljenu na tokenima

#### Apstrakcija transporta:

Transportni sloj apstrahira detalje komunikacije od sloja podataka, omogućujući isti format poruka JSON-RPC 2.0 preko svih transportnih mehanizama. Ova apstrakcija dopušta aplikacijama da bez problema prebacuju između lokalnih i udaljenih servera.

### Sigurnosne napomene

MCP implementacije moraju se pridržavati nekoliko ključnih sigurnosnih načela kako bi osigurale sigurne, pouzdane i zaštićene interakcije u svim operacijama protokola:

- **Sklonost korisničkom pristanku i kontroli**: Korisnici moraju dati izričiti pristanak prije bilo kakvog pristupa podacima ili izvršenja radnji. Trebaju imati jasnu kontrolu nad time koji se podaci dijele i koje su akcije autorizirane, uz intuitivna korisnička sučelja za pregled i odobravanje aktivnosti.

- **Privatnost podataka**: Korisnički podaci smiju se izlagati samo uz izričit pristanak i moraju biti zaštićeni odgovarajućim kontrolama pristupa. MCP implementacije moraju spriječiti neovlašten prijenos podataka i osigurati privatnost u svim interakcijama.

- **Sigurnost alata**: Prije pozivanja bilo kojeg alata potreban je izričiti korisnički pristanak. Korisnici bi trebali imati jasno razumijevanje funkcionalnosti svakog alata, a čvrste sigurnosne granice moraju biti provedene kako bi se spriječilo neželjeno ili nesigurno izvršenje alata.

Slijedeći ta sigurnosna načela, MCP osigurava povjerenje korisnika, privatnost i sigurnost u svim interakcijama protokola istovremeno omogućavajući moćne AI integracije.

## Primjeri koda: ključne komponente

Ispod su primjeri koda u nekoliko popularnih programskih jezika koji ilustriraju kako implementirati ključne MCP server komponente i alate.

### Primjer u .NET-u: Kreiranje jednostavnog MCP servera s alatima

Evo praktičnog .NET primjera koda koji pokazuje kako implementirati jednostavan MCP server s prilagođenim alatima. Ovaj primjer prikazuje kako definirati i registrirati alate, rješavati zahtjeve i povezati server koristeći Model Context Protocol.

```csharp
using System;
using System.Threading.Tasks;
using ModelContextProtocol.Server;
using ModelContextProtocol.Server.Transport;
using ModelContextProtocol.Server.Tools;

public class WeatherServer
{
    public static async Task Main(string[] args)
    {
        // Create an MCP server
        var server = new McpServer(
            name: "Weather MCP Server",
            version: "1.0.0"
        );
        
        // Register our custom weather tool
        server.AddTool<string, WeatherData>("weatherTool", 
            description: "Gets current weather for a location",
            execute: async (location) => {
                // Call weather API (simplified)
                var weatherData = await GetWeatherDataAsync(location);
                return weatherData;
            });
        
        // Connect the server using stdio transport
        var transport = new StdioServerTransport();
        await server.ConnectAsync(transport);
        
        Console.WriteLine("Weather MCP Server started");
        
        // Keep the server running until process is terminated
        await Task.Delay(-1);
    }
    
    private static async Task<WeatherData> GetWeatherDataAsync(string location)
    {
        // This would normally call a weather API
        // Simplified for demonstration
        await Task.Delay(100); // Simulate API call
        return new WeatherData { 
            Temperature = 72.5,
            Conditions = "Sunny",
            Location = location
        };
    }
}

public class WeatherData
{
    public double Temperature { get; set; }
    public string Conditions { get; set; }
    public string Location { get; set; }
}
```

### Primjer u Javi: MCP server komponente

Ovaj primjer pokazuje isti MCP server i registraciju alata kao i gore u .NET primjeru, ali implementiran u Javi.

```java
import io.modelcontextprotocol.server.McpServer;
import io.modelcontextprotocol.server.McpToolDefinition;
import io.modelcontextprotocol.server.transport.StdioServerTransport;
import io.modelcontextprotocol.server.tool.ToolExecutionContext;
import io.modelcontextprotocol.server.tool.ToolResponse;

public class WeatherMcpServer {
    public static void main(String[] args) throws Exception {
        // Kreirajte MCP poslužitelj
        McpServer server = McpServer.builder()
            .name("Weather MCP Server")
            .version("1.0.0")
            .build();
            
        // Registrirajte vremenski alat
        server.registerTool(McpToolDefinition.builder("weatherTool")
            .description("Gets current weather for a location")
            .parameter("location", String.class)
            .execute((ToolExecutionContext ctx) -> {
                String location = ctx.getParameter("location", String.class);
                
                // Dohvati podatke o vremenu (pojednostavljeno)
                WeatherData data = getWeatherData(location);
                
                // Vrati formatirani odgovor
                return ToolResponse.content(
                    String.format("Temperature: %.1f°F, Conditions: %s, Location: %s", 
                    data.getTemperature(), 
                    data.getConditions(), 
                    data.getLocation())
                );
            })
            .build());
        
        // Spojite poslužitelj koristeći stdio transport
        try (StdioServerTransport transport = new StdioServerTransport()) {
            server.connect(transport);
            System.out.println("Weather MCP Server started");
            // Držite poslužitelj aktivnim dok proces ne bude zaustavljen
            Thread.currentThread().join();
        }
    }
    
    private static WeatherData getWeatherData(String location) {
        // Implementacija bi pozvala vremenski API
        // Pojednostavljeno za svrhe primjera
        return new WeatherData(72.5, "Sunny", location);
    }
}

class WeatherData {
    private double temperature;
    private String conditions;
    private String location;
    
    public WeatherData(double temperature, String conditions, String location) {
        this.temperature = temperature;
        this.conditions = conditions;
        this.location = location;
    }
    
    public double getTemperature() {
        return temperature;
    }
    
    public String getConditions() {
        return conditions;
    }
    
    public String getLocation() {
        return location;
    }
}
```

### Primjer u Pythonu: Izgradnja MCP servera

Ovaj primjer koristi fastmcp, stoga ga prvo instalirajte:

```python
pip install fastmcp
```
Primjer koda:

```python
#!/usr/bin/env python3
import asyncio
from fastmcp import FastMCP
from fastmcp.transports.stdio import serve_stdio

# Kreiraj FastMCP server
mcp = FastMCP(
    name="Weather MCP Server",
    version="1.0.0"
)

@mcp.tool()
def get_weather(location: str) -> dict:
    """Gets current weather for a location."""
    return {
        "temperature": 72.5,
        "conditions": "Sunny",
        "location": location
    }

# Alternativni pristup korištenjem klase
class WeatherTools:
    @mcp.tool()
    def forecast(self, location: str, days: int = 1) -> dict:
        """Gets weather forecast for a location for the specified number of days."""
        return {
            "location": location,
            "forecast": [
                {"day": i+1, "temperature": 70 + i, "conditions": "Partly Cloudy"}
                for i in range(days)
            ]
        }

# Registriraj alate klase
weather_tools = WeatherTools()

# Pokreni server
if __name__ == "__main__":
    asyncio.run(serve_stdio(mcp))
```

### Primjer u JavaScriptu: Kreiranje MCP servera

Ovaj primjer prikazuje kreiranje MCP servera u JavaScriptu i registraciju dva alata vezana uz vremensku prognozu.

```javascript
// Korištenje službenog Model Context Protocol SDK-a
import { McpServer } from "@modelcontextprotocol/sdk/server/mcp.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";
import { z } from "zod"; // Za validaciju parametara

// Kreiraj MCP server
const server = new McpServer({
  name: "Weather MCP Server",
  version: "1.0.0"
});

// Definiraj alat za vremensku prognozu
server.tool(
  "weatherTool",
  {
    location: z.string().describe("The location to get weather for")
  },
  async ({ location }) => {
    // Ovo bi obično pozvalo API za vremensku prognozu
    // Pojednostavljeno za demonstraciju
    const weatherData = await getWeatherData(location);
    
    return {
      content: [
        { 
          type: "text", 
          text: `Temperature: ${weatherData.temperature}°F, Conditions: ${weatherData.conditions}, Location: ${weatherData.location}` 
        }
      ]
    };
  }
);

// Definiraj alat za prognozu
server.tool(
  "forecastTool",
  {
    location: z.string(),
    days: z.number().default(3).describe("Number of days for forecast")
  },
  async ({ location, days }) => {
    // Ovo bi obično pozvalo API za vremensku prognozu
    // Pojednostavljeno za demonstraciju
    const forecast = await getForecastData(location, days);
    
    return {
      content: [
        { 
          type: "text", 
          text: `${days}-day forecast for ${location}: ${JSON.stringify(forecast)}` 
        }
      ]
    };
  }
);

// Pomoćne funkcije
async function getWeatherData(location) {
  // Simuliraj poziv API-ja
  return {
    temperature: 72.5,
    conditions: "Sunny",
    location: location
  };
}

async function getForecastData(location, days) {
  // Simuliraj poziv API-ja
  return Array.from({ length: days }, (_, i) => ({
    day: i + 1,
    temperature: 70 + Math.floor(Math.random() * 10),
    conditions: i % 2 === 0 ? "Sunny" : "Partly Cloudy"
  }));
}

// Spoji server koristeći stdio transport
const transport = new StdioServerTransport();
server.connect(transport).catch(console.error);

console.log("Weather MCP Server started");
```

Ovaj JavaScript primjer demonstrira kako kreirati MCP server koji registrira vremenski povezane alate i povezuje se koristeći stdio transport za rukovanje dolaznim zahtjevima klijenata.

## Sigurnost i autorizacija

MCP uključuje nekoliko ugrađenih koncepta i mehanizama za upravljanje sigurnošću i autorizacijom kroz cijeli protokol:

1. **Kontrola dopuštenja za alate**:  
  Klijenti mogu specificirati koje alate model smije koristiti tijekom sesije. Ovo osigurava da su samo eksplicitno autorizirani alati dostupni, smanjujući rizik od neželjenih ili nesigurnih radnji. Dozvole se mogu dinamički konfigurirati na temelju korisničkih postavki, organizacijskih politika ili konteksta interakcije.

2. **Autentikacija**:  
  Serveri mogu zahtijevati autentikaciju prije nego što dopuste pristup alatima, resursima ili osjetljivim operacijama. To može uključivati API ključeve, OAuth tokene ili druge sheme autentikacije. Ispravna autentikacija osigurava da samo pouzdani klijenti i korisnici mogu pozivati mogućnosti sa servera.

3. **Validacija**:  
  Validacija parametara provodi se za sva pozivanja alata. Svaki alat definira očekivane tipove, formate i ograničenja za svoje parametre, a server validira dolazne zahtjeve u skladu s tim. To sprječava nepravilne ili zlonamjerne unose da dođu do implementacije alata i pomaže održati integritet operacija.

4. **Ograničenje brzine (rate limiting)**:  
  Kako bi spriječili zloupotrebu i osigurali poštenu uporabu resursa servera, MCP serveri mogu implementirati ograničenja brzine za pozive alata i pristup resursima. Ograničenja se mogu primjenjivati po korisniku, po sesiji ili globalno, pomažući u zaštiti od napada uskraćivanja usluge ili prekomjerne potrošnje resursa.

Kombinirajući ove mehanizme, MCP pruža siguran temelj za integraciju jezičnih modela s vanjskim alatima i izvorima podataka, dajući korisnicima i developerima detaljnu kontrolu nad pristupom i korištenjem.

## Poruke protokola i tijek komunikacije

MCP komunikacija koristi strukturirane **JSON-RPC 2.0** poruke kako bi omogućila jasne i pouzdane interakcije između hostova, klijenata i servera. Protokol definira specifične obrasce poruka za različite vrste operacija:

### Osnovne vrste poruka:

#### **Poruke za inicijalizaciju**
- **Zahtjev `initialize`**: Uspostavlja vezu i pregovara verziju protokola i mogućnosti  
- **Odgovor `initialize`**: Potvrđuje podržane značajke i informacije o serveru  
- **`notifications/initialized`**: Signalizira da je inicijalizacija završena i sesija spremna

#### **Poruke za otkrivanje**
- **Zahtjev `tools/list`**: Otkriva dostupne alate na serveru  
- **Zahtjev `resources/list`**: Popis dostupnih resursa (izvori podataka)  
- **Zahtjev `prompts/list`**: Dohvaća dostupne predloške prompta

#### **Poruke za izvršenje**  
- **Zahtjev `tools/call`**: Izvršava određeni alat s navedenim parametrima  
- **Zahtjev `resources/read`**: Dohvaća sadržaj određenog resursa  
- **Zahtjev `prompts/get`**: Dohvaća predložak prompta s opcionalnim parametrima

#### **Klijentske poruke**
- **Zahtjev `sampling/complete`**: Server traži dovršetak LLM-a od klijenta  
- **`elicitation/request`**: Server traži korisnički unos putem klijentskog sučelja  
- **Poruke zapisnika (Logging Messages)**: Server šalje strukturirane log poruke klijentu

#### **Poruke notifikacija**
- **`notifications/tools/list_changed`**: Server obavještava klijenta o promjenama alata  
- **`notifications/resources/list_changed`**: Server obavještava klijenta o promjenama resursa  
- **`notifications/prompts/list_changed`**: Server obavještava klijenta o promjenama promptova

### Struktura poruke:

Sve MCP poruke slijede JSON-RPC 2.0 format s:  
- **Zahtjevne poruke**: Sadrže `id`, `method` i opcionalno `params`  
- **Odgovorne poruke**: Sadrže `id` i ili `result` ili `error`  
- **Poruke notifikacija**: Sadrže `method` i opcionalno `params` (bez `id` i nije očekivan odgovor)

Ova strukturirana komunikacija osigurava pouzdane, pratljive i proširive interakcije koje podržavaju napredne scenarije poput ažuriranja u stvarnom vremenu, povezivanja alata i robusnog upravljanja pogreškama.

### Zadaci (eksperimentalno)

**Zadaci** su eksperimentalna značajka koja pruža trajne omotače za izvršenje koji omogućuju odgođeno preuzimanje rezultata i praćenje statusa MCP zahtjeva:

- **Dugotrajne operacije**: Praćenje skupih izračuna, automatizacije tijeka rada i obrade u serijama  
- **Odgođeni rezultati**: Upit za status zadatka i dohvat rezultata nakon završetka operacija  
- **Praćenje statusa**: Nadzor napretka zadatka kroz definirane faze životnog ciklusa  
- **Višestepene operacije**: Podrška složenim tijekovima rada koji obuhvaćaju više interakcija

Zadaci obavijaju standardne MCP zahtjeve kako bi omogućili asinkrone obrasce izvršenja za operacije koje se ne mogu odmah dovršiti.

## Ključni zaključci

- **Arhitektura**: MCP koristi klijent-server arhitekturu gdje hostovi upravljaju višestrukim klijentskim vezama prema serverima  
- **Sudionici**: Ekosustav uključuje hostove (AI aplikacije), klijente (protokol konektore) i servere (pružatelje mogućnosti)  
- **Transportni mehanizmi**: Komunikacija podržava STDIO (lokalni) i Streamable HTTP s opcionim SSE (udaljeni)  
- **Osnovni primitivci**: Serveri izlažu alate (izvršne funkcije), resurse (izvore podataka) i promptove (predloške)  
- **Klijentski primitivci**: Serveri mogu tražiti uzorkovanje (dovršetke LLM-a uz pozivanje alata), traženje unosa (uključujući URL mod), "roots" (granice datotečnog sustava) i logiranje od klijenata  
- **Eksperimentalne značajke**: Zadaci pružaju trajne omotače izvršenja za dugotrajne operacije  
- **Temelj protokola**: Izgrađen na JSON-RPC 2.0 s verzioniranjem temeljenim na datumu (trenutno: 2025-11-25)  
- **Mogućnosti u stvarnom vremenu**: Podržava notifikacije za dinamička ažuriranja i sinkronizaciju u stvarnom vremenu  
- **Sigurnost na prvom mjestu**: Izričiti korisnički pristanak, zaštita privatnosti podataka i siguran transport su ključni zahtjevi

## Vježba

Dizajnirajte jednostavan MCP alat koji bi vam bio koristan u vašem području. Definirajte:  
1. Kako bi se alat zvao  
2. Koje parametre bi prihvaćao  
3. Koji izlaz bi vraćao  
4. Kako bi model mogao koristiti taj alat za rješavanje korisničkih problema


---

## Što slijedi

Sljedeće: [Poglavlje 2: Sigurnost](../02-Security/README.md)

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**Odricanje od odgovornosti**:
Ovaj dokument preveden je korištenjem AI prevoditeljske usluge [Co-op Translator](https://github.com/Azure/co-op-translator). Iako težimo točnosti, molimo imajte na umu da automatski prijevodi mogu sadržavati pogreške ili netočnosti. Izvorni dokument na njegovom izvornom jeziku treba smatrati autoritativnim izvorom. Za kritične informacije preporučuje se angažiranje profesionalnog ljudskog prevoditelja. Nismo odgovorni za bilo kakve nesporazume ili pogrešne interpretacije koje proizlaze iz korištenja ovog prijevoda.
<!-- CO-OP TRANSLATOR DISCLAIMER END -->
# 👻 Ghost Sikkerhetsmodul
**PowerShell-basert Windows og Azure sikkerhetsherdingsverktøy**

> **Proaktiv sikkerhetsherding for Windows-endepunkter og Azure-miljøer.** Ghost tilbyr PowerShell-baserte herdingsfunksjoner som kan hjelpe med å redusere vanlige angrepsveier ved å deaktivere unødvendige tjenester og protokoller.

## ⚠️ Viktige advarsler

**TESTING PÅKREVD**: Test alltid Ghost i ikke-produksjonsmiljøer først. Deaktivering av tjenester kan påvirke legitime forretningsfunksjoner.

**INGEN GARANTIER**: Selv om Ghost retter seg mot vanlige angrepsveier, kan ingen sikkerhetsverktøy forhindre alle angrep. Dette er én komponent i en omfattende sikkerhetsstrategi.

**OPERASJONELL PÅVIRKNING**: Noen funksjoner kan påvirke systemfunksjonalitet. Gjennomgå hver innstilling nøye før distribusjon.

**PROFESJONELL VURDERING**: For produksjonsmiljøer, konsulter med sikkerhetseksperter for å sikre at innstillingene er i tråd med organisasjonens behov.

## 📊 Sikkerhetslandskapet

Ransomware-skade nådde **$57 milliarder i 2025**, med forskning som viser at mange vellykkede angrep utnytter grunnleggende Windows-tjenester og feilkonfigurasjoner. Vanlige angrepsveier inkluderer:

- **90% av ransomware-hendelser** involverer RDP-utnyttelse
- **SMBv1-sårbarheter** muliggjorde angrep som WannaCry og NotPetya
- **Dokumentmakroer** forblir en primær metode for malware-levering
- **USB-baserte angrep** fortsetter å målrette luftgap-nettverk
- **PowerShell-misbruk** har økt betydelig de siste årene

## 🛡️ Ghost sikkerhetsfunksjoner

Ghost tilbyr **16 Windows-herdingsfunksjoner** pluss **Azure sikkerhetsintegrasjon**:

### Windows Endpoint-herding

| Funksjon | Formål | Betraktninger |
|----------|---------|----------------|
| `Set-RDP` | Administrerer Remote Desktop-tilgang | Kan påvirke fjernadministrasjon |
| `Set-SMBv1` | Kontrollerer eldre SMB-protokoll | Nødvendig for svært gamle systemer |
| `Set-AutoRun` | Kontrollerer AutoPlay/AutoRun | Kan påvirke brukervennlighet |
| `Set-USBStorage` | Begrenser USB-lagringsenheter | Kan påvirke legitim USB-bruk |
| `Set-Macros` | Kontrollerer Office-makroutførelse | Kan påvirke makroaktiverte dokumenter |
| `Set-PSRemoting` | Administrerer PowerShell-fjernkontroll | Kan påvirke fjernadministrasjon |
| `Set-WinRM` | Kontrollerer Windows Remote Management | Kan påvirke fjernadministrasjon |
| `Set-LLMNR` | Administrerer navneoppløsningsprotokoll | Vanligvis trygt å deaktivere |
| `Set-NetBIOS` | Kontrollerer NetBIOS over TCP/IP | Kan påvirke eldre applikasjoner |
| `Set-AdminShares` | Administrerer administrative delinger | Kan påvirke fjerntilgang til filer |
| `Set-Telemetry` | Kontrollerer datainnsamling | Kan påvirke diagnostiske evner |
| `Set-GuestAccount` | Administrerer gjestkonto | Vanligvis trygt å deaktivere |
| `Set-ICMP` | Kontrollerer ping-responser | Kan påvirke nettverksdiagnostikk |
| `Set-RemoteAssistance` | Administrerer Remote Assistance | Kan påvirke helpdesk-operasjoner |
| `Set-NetworkDiscovery` | Kontrollerer nettverksoppdagelse | Kan påvirke nettverksblaing |
| `Set-Firewall` | Administrerer Windows Firewall | Kritisk for nettverkssikkerhet |

### Azure skysikkerhet

| Funksjon | Formål | Krav |
|----------|---------|--------------|
| `Set-AzureSecurityDefaults` | Aktiverer grunnleggende Azure AD-sikkerhet | Microsoft Graph-tillatelser |
| `Set-AzureConditionalAccess` | Konfigurerer tilgangspolicyer | Azure AD P1/P2-lisensiering |
| `Set-AzurePrivilegedUsers` | Reviderer privilegerte kontoer | Global Admin-tillatelser |

### Bedriftsdistribusjonsalternativer

| Metode | Brukstilfelle | Krav |
|--------|----------|--------------|
| **Direkte utførelse** | Testing, små miljøer | Lokale administratorrettigheter |
| **Group Policy** | Domenmiljøer | Domenadministrator, GP-administrasjon |
| **Microsoft Intune** | Skyforvaltede enheter | Intune-lisensiering, Graph API |

## 🚀 Rask start

### Sikkerhetsvurdering
```powershell
# Last inn Ghost-modul
IEX(Invoke-WebRequest 'https://raw.githubusercontent.com/jimrtyler/Ghost/main/Ghost.ps1')

# Sjekk gjeldende sikkerhetsstatus
Get-Ghost
```

### Grunnleggende herding (test først)
```powershell
# Essensiell herding - test i laboratoriemiljø først
Set-Ghost -SMBv1 -AutoRun -Macros

# Gjennomgå endringer
Get-Ghost
```

### Bedriftsdistribusjon
```powershell
# Group Policy-distribusjon (domenmiljøer)
Set-Ghost -SMBv1 -AutoRun -GroupPolicy

# Intune-distribusjon (skyforvaltede enheter)
Set-Ghost -SMBv1 -RDP -USBStorage -Intune
```

## 📋 Installasjonsmetoder

### Alternativ 1: Direkte nedlasting (testing)
```powershell
IEX(Invoke-WebRequest 'https://raw.githubusercontent.com/jimrtyler/Ghost/main/Ghost.ps1')
```

### Alternativ 2: Modulinstallasjon
```powershell
# Installer fra PowerShell Gallery (når tilgjengelig)
Install-Module Ghost -Scope CurrentUser
Import-Module Ghost
```

### Alternativ 3: Bedriftsdistribusjon
```powershell
# Kopier til nettverksplassering for Group Policy-distribusjon
# Konfigurer Intune PowerShell-skript for skydistribusjon
```

## 💼 Brukstilfelle-eksempler

### Liten bedrift
```powershell
# Grunnleggende beskyttelse med minimal påvirkning
Set-Ghost -SMBv1 -AutoRun -Macros -ICMP
```

### Helsevesenmiljø
```powershell
# HIPAA-fokusert herding
Set-Ghost -SMBv1 -RDP -USBStorage -AdminShares -Telemetry
```

### Finansielle tjenester
```powershell
# Høy sikkerhetskonfigurasjon
Set-Ghost -RDP -SMBv1 -AutoRun -USBStorage -Macros -PSRemoting -AdminShares
```

### Sky-først-organisasjon
```powershell
# Intune-administrert distribusjon
Connect-IntuneGhost -Interactive
Set-Ghost -SMBv1 -RDP -AutoRun -Macros -Intune
```

## 🔍 Funksjonsdetaljer

### Kjerneherdingsfunksjoner

#### Nettverkstjenester
- **RDP**: Blokkerer fjernskrivebordstilgang eller randomiserer port
- **SMBv1**: Deaktiverer eldre fildelingsprotokoll
- **ICMP**: Forhindrer ping-responser for rekognosering
- **LLMNR/NetBIOS**: Blokkerer eldre navneoppløsningsprotokoller

#### Applikasjonssikkerhet
- **Makroer**: Deaktiverer makroutførelse i Office-applikasjoner
- **AutoRun**: Forhindrer automatisk utførelse fra flyttbare medier

#### Fjernadministrasjon
- **PSRemoting**: Deaktiverer PowerShell-fjernsesjoner
- **WinRM**: Stopper Windows Remote Management
- **Remote Assistance**: Blokkerer fjerrassistanseforbindelser

#### Tilgangskontroll
- **Admin Shares**: Deaktiverer C$, ADMIN$-delinger
- **Guest Account**: Deaktiverer gjestkontotilgang
- **USB Storage**: Begrenser USB-enhetsbruk

### Azure-integrasjon
```powershell
# Koble til Azure-leietaker
Connect-AzureGhost -Interactive

# Aktiver sikkerhetsinnstillinger
Set-AzureSecurityDefaults -Enable

# Konfigurer betinget tilgang
Set-AzureConditionalAccess -BlockLegacyAuth -RequireMFA

# Revider privilegerte brukere
Set-AzurePrivilegedUsers -AuditOnly
```

### Intune-integrasjon (nytt i v2)
```powershell
# Koble til Intune
Connect-IntuneGhost -Interactive

# Distribuer via Intune-policyer
Set-IntuneGhost -Settings @{
    RDP = $true
    SMBv1 = $true
    USBStorage = $true
    Macros = $true
}
```

## ⚠️ Viktige betraktninger

### Testingskrav
- **Laboratoriemiljø**: Test alle innstillinger i isolert miljø først
- **Gradvis distribusjon**: Rull ut gradvis for å identifisere problemer
- **Tilbakerullingsplan**: Sørg for at du kan reversere endringer om nødvendig
- **Dokumentasjon**: Registrer hvilke innstillinger som fungerer for ditt miljø

### Potensiell påvirkning
- **Brukerproduktivitet**: Noen innstillinger kan påvirke daglige arbeidsflyter
- **Eldre applikasjoner**: Eldre systemer kan kreve spesifikke protokoller
- **Fjerntilgang**: Vurder påvirkning på legitim fjernadministrasjon
- **Forretningsprosesser**: Verifiser at innstillinger ikke bryter kritiske funksjoner

### Sikkerhetsbegrensninger
- **Dybdeforsvar**: Ghost er ett sikkerhetslag, ikke en komplett løsning
- **Kontinuerlig forvaltning**: Sikkerhet krever kontinuerlig overvåking og oppdateringer
- **Brukeropplæring**: Teknisk kontroll må pares med sikkerhetsbevissthet
- **Trussel-evolusjon**: Nye angrepmetoder kan omgå nåværende beskyttelse

## 🎯 Eksempler på angrepscenarier

Selv om Ghost retter seg mot vanlige angrepsveier, avhenger spesifikk forebygging av riktig implementering og testing:

### WannaCry-stil angrep
- **Reduksjon**: `Set-Ghost -SMBv1` deaktiverer sårbar protokoll
- **Betraktninger**: Sørg for at ingen eldre system krever SMBv1

### RDP-basert ransomware
- **Reduksjon**: `Set-Ghost -RDP` blokkerer fjernskrivebordstilgang
- **Betraktninger**: Kan kreve alternative fjerntilgangsmetoder

### Dokumentbasert malware
- **Reduksjon**: `Set-Ghost -Macros` deaktiverer makroutførelse
- **Betraktninger**: Kan påvirke legitime makroaktiverte dokumenter

### USB-leverte trusler
- **Reduksjon**: `Set-Ghost -USBStorage -AutoRun` begrenser USB-funksjonalitet
- **Betraktninger**: Kan påvirke legitim USB-enhetsbruk

## 🏢 Bedriftsfunksjoner

### Group Policy-støtte
```powershell
# Anvend innstillinger via Group Policy-register
Set-Ghost -SMBv1 -RDP -AutoRun -GroupPolicy

# Innstillinger gjelder domenevidt etter GP-oppdatering
gpupdate /force
```

### Microsoft Intune-integrasjon
```powershell
# Opprett Intune-policyer for Ghost-innstillinger
Set-IntuneGhost -Settings $GhostSettings -Interactive

# Policyer distribueres automatisk til forvaltede enheter
```

### Overholdelsesrapportering
```powershell
# Generer sikkerhetsvurderingsrapport
Get-Ghost | Export-Csv -Path "SecurityAudit-$(Get-Date -Format 'yyyy-MM-dd').csv"

# Azure sikkerhetsposturrapport
Get-AzureGhost | Out-File "AzureSecurityReport.txt"
```

## 📚 Beste praksis

### Før distribusjon
1. **Dokumenter nåværende tilstand**: Kjør `Get-Ghost` før endringer
2. **Test grundig**: Valider i ikke-produksjonsmiljø
3. **Planlegg tilbakerulling**: Vit hvordan du reverserer hver innstilling
4. **Interessentgjennomgang**: Sørg for at forretningsenheter godkjenner endringer

### Under distribusjon
1. **Gradvis tilnærming**: Distribuer til pilotgrupper først
2. **Overvåk påvirkning**: Se etter brukerklager eller systemproblemer
3. **Dokumenter problemer**: Registrer eventuelle problemer for fremtidig referanse
4. **Kommuniser endringer**: Informer brukere om sikkerhetsforbedringer

### Etter distribusjon
1. **Regelmessig vurdering**: Kjør `Get-Ghost` periodisk for å verifisere innstillinger
2. **Oppdater dokumentasjon**: Vedlikehold oppdaterte sikkerhetskonfigurasjoner
3. **Gjennomgå effektivitet**: Overvåk for sikkerhetshendelser
4. **Kontinuerlig forbedring**: Juster innstillinger basert på trussel-landskap

## 🔧 Feilsøking

### Vanlige problemer
- **Tillatelserfeil**: Sørg for forhøyet PowerShell-sesjon
- **Tjenesteavhengigheter**: Noen tjenester kan ha avhengigheter
- **Applikasjonskompatibilitet**: Test med forretningsapplikasjoner
- **Nettverksforbindelse**: Verifiser at fjerntilgang fortsatt fungerer

### Gjenopprettingsalternativer
```powershell
# Aktiver spesifikke tjenester på nytt om nødvendig
Set-RDP -Enable
Set-SMBv1 -Enable
Set-AutoRun -Enable
Set-Macros -Enable
```

## 👨‍💻 Om forfatteren

**Jim Tyler** - Microsoft MVP for PowerShell
- **YouTube**: [@PowerShellEngineer](https://youtube.com/@PowerShellEngineer) (10,000+ abonnenter)
- **Nyhetsbrev**: [PowerShell.News](https://powershell.news) - Ukentlig sikkerhetsintelligens
- **Forfatter**: "PowerShell for Systems Engineers"
- **Erfaring**: Tiår med PowerShell-automatisering og Windows-sikkerhet

## 📄 Lisens og ansvarsfraskrivelse

### MIT-lisens
Ghost leveres under MIT-lisensen for gratis bruk, modifikasjon og distribusjon.

### Sikkerhetsansvarsfraskrivelse
- **Ingen garanti**: Ghost leveres "som den er" uten garanti av noe slag
- **Testing påkrevd**: Test alltid i ikke-produksjonsmiljøer først
- **Profesjonell veiledning**: Konsulter med sikkerhetseksperter for produksjonsdistribusjoner
- **Operasjonell påvirkning**: Forfatterne er ikke ansvarlige for operative forstyrrelser
- **Omfattende sikkerhet**: Ghost er en komponent i en komplett sikkerhetsstrategi

### Støtte
- **GitHub Issues**: [Rapporter feil eller be om funksjoner](https://github.com/jimrtyler/Ghost/issues)
- **Dokumentasjon**: Bruk `Get-Help <function> -Full` for detaljert hjelp
- **Samfunn**: PowerShell og sikkerhetsssamfunnsforum

---

**🔒 Styrk sikkerhetsstatus med Ghost - men test alltid først.**

```powershell
# Start med vurdering, ikke antakelser
Get-Ghost
```

**⭐ Gi denne repositoriet en stjerne hvis Ghost hjelper med å forbedre sikkerhetsstatus!**
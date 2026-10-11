# Økonomi

Privat økonomiverktøy for Peder og Viktoria. Én statisk side på GitHub Pages, ingen server, ingen avhengigheter.

All data ligger i `data.json`, kryptert med AES-256-GCM. Nøkkelen lages fra passordet (PBKDF2-SHA256, 600 000 runder). Filen er offentlig i repoet, men uten passordet er den bare tilfeldige tegn. `index.html` inneholder ingen tall, navn eller kontoer.

## Førstegangsoppsett

1. **Fjern den gamle, ukrypterte dataen fra GitHub.** Den gamle `data.json` ligger i klartekst i git-historikken, og repoet er offentlig. Å slette filen er ikke nok. Enkleste løsning:
   - GitHub → repoet → Settings → helt nederst: *Delete this repository*.
   - Lag et nytt, tomt repo med samme navn: `PederMyhrer.github.io`.
   - Last opp **bare** `index.html` og `README.md`. Pages slår seg på automatisk for dette repo-navnet (sjekk Settings → Pages, kilde `main`).
2. **Slett det gamle tokenet** under GitHub → Settings → Developer settings → Personal access tokens.
3. **Lag et nytt fine-grained token:**
   - Repository access: *Only select repositories* → `PederMyhrer.github.io`
   - Permissions → Repository → *Contents: Read and write*. Ingenting annet.
4. Åpne siden. Velg passord, velg `startdata-oktober.json` som startdata og lim inn tokenet. Siden lager en kryptert `data.json` i repoet.
5. Slett `startdata-oktober.json` fra maskinen etterpå (den er ukryptert). Last heller ned en kryptert kopi fra Innstillinger.
6. Viktoria åpner samme side og skriver passordet. For å kunne lagre fra hennes telefon: Innstillinger → Legg inn token.

Passordet kan ikke gjenopprettes. Bruk en lang setning, fire til fem tilfeldige ord, og skriv den ned et trygt sted.

## Slik er det tenkt brukt

**Kontoer** er de ekte kontoene i banken (nå én sparekonto). Legg gjerne til bolig som eiendel og lån som gjeld for å se hele nettoformuen.

**Sparemål** er konvolutter inne i en konto: Buffer, Bil, Barn, Investeringer osv. Summen av målene på en konto skal være lik saldoen. Det som ikke er fordelt vises tydelig, så hver krone har en jobb.

**Budsjett** er per måned og nullbasert: inntekter minus utgifter minus sparing skal bli 0. Sparelinjene peker på et sparemål, og det er her den månedlige sparingen bestemmes.

### Månedsrytme

1. Ny måned: Budsjett → › → *Lag budsjett ved å kopiere forrige*.
2. Juster beløpene (Rediger). Fordel det som er igjen til mål.
3. Overfør pengene i nettbanken og kryss av linjene.
4. *Avslutt måned*: sparingen bokføres på målene og kontoen, og formuen lagres i historikken.
5. Kontoer → *Oppdater saldoer* med tallene fra banken. Renter og avvik dukker opp som «ikke fordelt» og kan fordeles.

Når pengene brukes, for eksempel når bilen kjøpes: Sparemål → Bil → *Sett inn / ta ut* → negativt beløp, «penger ut av kontoen».

## Sikkerhet, kort fortalt

- Ingenting lagres ukryptert: ikke i repoet, ikke i nettleseren. Tokenet lagres også kryptert.
- Siden låser seg selv etter 15 minutter uten aktivitet (kan endres).
- Styrken avhenger av passordet. Et kort eller vanlig passord kan gjettes av den som laster ned filen.
- GitHub Pages kan vise en noen minutter gammel `data.json`. Med token hentes alltid ferskeste versjon fra GitHub direkte.
- Redigerer dere samtidig på to enheter, spør siden hvilken versjon som skal gjelde.

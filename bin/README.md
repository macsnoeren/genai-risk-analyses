# Cyberwijzer Risicoanalyse Agent

Automatische risicoanalyse-generator voor cybersecurity-thema's in het onderwijs.

## Installatie

```bash
pip install -r requirements.txt
export ANTHROPIC_API_KEY='sk-ant-...'
```

## Gebruik

### Stap 1: Genereer de risicoanalyse (JSON)

```bash
# Basis
python agent.py "Versiebeheer met Git"

# Met optionele uitleg van het thema
python agent.py "Docker containers" --uitleg "Docker is een containerplatform dat..."

# Met aangepaste output en meer searches
python agent.py "API Security" --output rapport_api.json --max-searches 20
```

### Stap 2: Genereer het Word-rapport

```bash
python rapport.py risicoanalyse_versiebeheer_met_git.json

# Met aangepaste output
python rapport.py rapport.json --output mijn_rapport.docx
```

## Architectuur

```
agent.py        →  JSON (risicoanalyse)  →  rapport.py  →  .docx
                        ↑
               Anthropic API + Web Search
```

- **agent.py**: Stuurt een prompt naar Claude (Sonnet) met de web search tool ingeschakeld. De agent zoekt zelf bronnen, verifieert bevindingen met minimaal 2 bronnen, en levert een gestructureerd JSON-object op.
- **rapport.py**: Leest het JSON-bestand en genereert een professioneel Word-document in de Cyberwijzer-stijl met voorpagina, risicomatrix, maatregelen en basisvaardigheden.

## JSON-structuur

Zie `risicoanalyse_schema_voorbeeld.json` voor een compleet voorbeeld. De hoofdsecties zijn:

| Sectie | Inhoud |
|--------|--------|
| `metadata` | Titel, auteur, datum, versie |
| `beschrijving_thema` | Inleiding, toepassingen, conclusie |
| `onderzoek` | Deelonderwerpen met bevindingen en bronnen |
| `consequenties_en_voorbeelden` | Echte incidenten |
| `risicos` | Risicomatrix met kans/impact/score |
| `maatregelen` | Technisch, proces, organisatorisch |
| `basisvaardigheden` | Bewustzijn, vaardigheden, gedrag |
| `samenvatting` | Kernrisico's, kernmaatregelen, kerninzicht |
| `bronnen` | Referentielijst |

## Kosten

Een enkele risicoanalyse kost circa $0.50–$2.00 aan API-kosten (afhankelijk van het aantal web searches en de complexiteit van het thema).

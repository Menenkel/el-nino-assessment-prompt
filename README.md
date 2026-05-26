# el-nino-assessment-prompt
A structured LLM prompt for generating decision-grade El Niño regional impact assessments

# El Niño Regional Assessment Prompt

A structured prompt for large language models (LLMs) that generates
decision-grade El Niño impact assessments for any region in the world —
in plain language, fully sourced, with interactive HTML charts.

Built for humanitarian planners, development finance teams, and government
decision-makers who need climate risk intelligence fast, without a
meteorology degree.

---

## What it produces

A ten-section regional brief covering:

1. **Current El Niño status** — plain-language forecast with confidence indicators
2. **Regional signal** — drought, wetter-than-normal, or mixed, with confidence level
3. **Sector impacts** — agriculture, food security, water, health, disaster financing
4. **Historical El Niño impacts** — documented past events with sources and years
5. **Anticipatory action window** — decision deadline and what must happen before it
6. **Watch items** — what to monitor and where
7. **Interactive HTML charts** — maize/harvest trends, seasonal calendar overlap,
   sortable event history, sector risk matrix
8. **Reliability check** — built-in audit of sources, unsourced claims, and weakest findings
9. **Verify before acting** — checklist of primary sources to confirm before acting
10. **Numbered source list** — every source with organisation, date, and URL

All key findings carry inline confidence labels (`[HIGH]` / `[MEDIUM]` / `[LOW]`)
based on source agreement, historical consistency, and forecast uncertainty.

---

## How to use it

### 1. Open the prompt file
The full prompt is in [`PROMPT.md`](./PROMPT.md).

### 2. Change two lines
At the top of the `# TASK` section:

```
Produce a regional El Niño impact assessment for: [INSERT REGION OR COUNTRY].
Optionally specify a sector focus: [agriculture / food security / water / health /
disaster risk financing — or "all"].
```

Replace `[INSERT REGION OR COUNTRY]` with your target (e.g. `Ethiopia`,
`Southern Africa`, `the Philippines`).
Replace the sector focus with whichever sectors matter, or leave as `all`.

**That's it.** The prompt handles the rest.

### 3. Run it in a model with web search enabled
The prompt instructs the model to fetch live forecasts from primary sources
rather than rely on training data — ENSO status changes monthly, so current
retrieval is essential. Use a model with web search access (e.g. Claude,
ChatGPT with search, Gemini). Results from models without web access will
be structurally valid but may contain stale forecast figures.

### 4. Verify before acting
The brief itself tells you what to verify. Always complete Section 9
(Verify Before Acting) before sharing or acting on the output.

---

## Key design principles

**Plain language is mandatory.** Every technical term must be explained
in-line the first time it appears. No undefined acronyms. The prompt
explicitly rejects meteorological jargon.

**No unsourced claims.** Every factual statement must trace to a named,
dated source. If a fact cannot be verified, the model is instructed to
say so explicitly — never to estimate or infer silently.

**Live data, not training data.** The prompt names eight primary sources
and instructs the model to retrieve the most recent issuance (within 60 days)
before writing. Historical figures are clearly separated from current forecasts.

**Built-in self-audit.** Section 8 (Reliability Check) forces the model to
flag its own weakest claims, unsourced statements, and what facts would most
change the assessment. Section 9 gives the reader a primary-source checklist.
Together these make the output's limitations visible rather than hidden.

**Confidence indicators on key findings.** Every actionable claim carries
an inline `[HIGH]`, `[MEDIUM]`, or `[LOW]` label based on three factors:
number of independent sources agreeing, consistency of the historical record,
and whether the spring predictability barrier applies.

---

## Primary sources referenced by the prompt

| Source | What it provides | URL |
|---|---|---|
| NOAA CPC ENSO Diagnostic Discussion | Official monthly ENSO forecast | [cpc.ncep.noaa.gov](https://cpc.ncep.noaa.gov/products/analysis_monitoring/enso_advisory/ensodisc.shtml) |
| IRI/Columbia ENSO forecast & impacts viewer | Model plume + historical regional impacts | [iri.columbia.edu](https://iri.columbia.edu/our-expertise/climate/enso) |
| WMO Global Seasonal Climate Update | Multi-agency global seasonal outlook | [public.wmo.int](https://public.wmo.int/en/resources/publications/global-seasonal-climate-update) |
| ECMWF Seasonal System 5 | Rainfall/temperature anomaly maps | [charts.ecmwf.int](https://charts.ecmwf.int/products/seasonal_system5_standard_rain) |
| FEWS NET | Food security outlooks, seasonal calendars | [fews.net](https://fews.net) |
| GEOGLAM Crop Monitor | Crop conditions and early warning | [cropmonitor.org](https://cropmonitor.org) |
| FAO GIEWS | Crop calendars and country alerts | [fao.org/giews](https://www.fao.org/giews/en/) |

---

## Known limitations

- **Strength uncertainty is real.** The prompt correctly labels El Niño
  strength forecasts as `[LOW]` confidence because no strength category
  typically exceeds ~37% probability. Do not build operational plans around
  a specific strength scenario.

- **Model self-audit has limits.** The Reliability Check in Section 8 flags
  missing citations and obvious hedging — but cannot catch confident factual
  errors. A model that retrieved a wrong figure from a real source will not
  flag it. The Section 9 checklist and a regional specialist review remain
  essential for decision-grade use.

- **Web search quality varies.** The prompt instructs the model to search
  for live data, but search results depend on the model and session. Always
  check source dates in Section 10 — if the NOAA or IRI issuance cited is
  older than 60 days, re-run or verify manually.

- **1997/98 is a standing reminder.** The strongest El Niño on record
  produced only minor impacts in Zimbabwe. Pacific signal strength does not
  guarantee local damage. Local vulnerability, timing of dry spells, and
  pre-existing food security conditions modify outcomes significantly.

---

## Sample output

A full example run for Zimbabwe (Southern Africa, all sectors, May 2026)
is available in [`examples/zimbabwe_may2026.html`](./examples/zimbabwe_may2026.html).
It includes all four charts and the complete ten-section brief.

---

## Version history

| Version | Date | Changes |
|---|---|---|
| v1.0 | May 2026 | Initial release — all sectors, interactive HTML charts, confidence indicators, reliability check |

---

## Contributing

Suggestions welcome via Issues. Particularly useful contributions:
- Validation of regional signal accuracy against IRI historical composites
- Additional example runs for other regions
- Adaptation for La Niña (opposite signal in most regions)
- Translation into French, Spanish, or Portuguese for broader accessibility

---

## License

Released under the [MIT License](./LICENSE).
Free to use, modify, and distribute.

---

*Built for decision-grade use, not demonstration. Verify before acting.*

# Streaming Catalogue Knowledge Graph

**CSE4007 Semantic Web – Option 2: From Case Description to Turtle – Case 2C: Streaming Catalogue and Rights**

An RDF knowledge graph and small RDFS vocabulary for a fictional streaming service. It models films, a series and its episodes, contributors and their roles, genres, language versions, regional licences and availability periods. Built in Protégé, stored and queried in GraphDB.

## Files

| File | Description |
|---|---|
| `streaming_catalogue_final.ttl` | Vocabulary (classes, properties, domains, ranges, comments) and instance data in Turtle – 252 triples |
| `queries.rq` | Eight SPARQL queries (competency questions, inference check, validation) with expected results |
| `report.pdf` | Report: problem, competency questions, modelling decisions, results and limitations |
| `screenshots/` | Protégé and GraphDB screenshots of the model, query results and visual graph |

## Tools
- [Protégé](https://protege.stanford.edu/) 5.6.9 – building the vocabulary and individuals
- [GraphDB Free](https://graphdb.ontotext.com/) 11.5.1 – storing the graph, RDFS inference, SPARQL queries and visualisation

## Open in Protégé

1. Open Protégé.
2. **File → Open** → select `streaming_catalogue_final.ttl`.
3. Browse the **Classes**, **Object properties**, **Data properties** and **Individuals** tabs.
   **View → Render by label (rdfs:label)** shows readable names.

## Validate

1. **Syntax:** the file opens in Protégé without errors, and GraphDB imports it with no parse errors.
2. **Consistency:** in Protégé, **Reasoner → HermiT → Start reasoner**. No inconsistency is reported and no class appears in red.
3. **Data checks:** after importing into GraphDB, run Q1 (expected triple count) and Q8 (no availability period outside its licence period, 0 rows expected).

## Reproduce in GraphDB

1. Start GraphDB and open `http://localhost:7200` in a browser.
2. **Setup → Repositories → Create new repository → GraphDB Repository**.
   - Repository ID: `streaming_catalogue`
   - Ruleset: **RDFS (Optimized)** (required for the inference results)
   - Click **Create**.
3. Select `streaming_catalogue` from the repository dropdown (top right).
4. **Import → User data → Upload RDF files** → select `streaming_catalogue_final.ttl` → **Import**.
   - Target graph: **The default graph**. Base IRI can be left blank.
5. Open the **SPARQL** tab and run each query from `queries.rq` (copy the PREFIX lines with each query).
   The **Include inferred** toggle (`>>` icon) switches between explicit and inferred results.
6. **Explore → Visual graph** → search `Riverline` and expand nodes to see the subgraph.

## Expected results

| Query | Competency question / purpose | Expected result |
|---|---|---|
| Q1 | Triple count | 252 (inferred OFF), 376 (inferred ON) |
| Q2 | CQ1 – Who contributed to a work, and in what role? | 5 rows; Maya Sen is Actor on Riverline and Director on City Loop |
| Q3 | CQ2 – Which titles are available today, and where? | City Loop and Last Signal (Singapore); Riverline excluded as expired |
| Q4 | CQ3 – Which episodes belong to a series, in order? | City Loop Episodes 1–3 with durations PT45M, PT48M, PT50M |
| Q5 | CQ6 – Which resources are creative works? | 0 rows (inferred OFF), 6 rows (inferred ON) via `rdfs:subClassOf` |
| Q6 | CQ4 – Which language versions does a title have? | Riverline: English, Hindi; Last Signal: English, Malayalam; City Loop: English |
| Q7 | CQ5 – Which licence covers a title, where and when? | Riverline: India 2024–2025; Last Signal and City Loop: Singapore 2026–2027 |
| Q8 | Validation – availability outside its licence period | 0 rows |

## Acknowledgements

- Protégé (Stanford University) and GraphDB (Ontotext) were used to build, validate and query the model.
- Claude (Anthropic) and ChatGPT (OpenAI) were used for discussion of modelling options, troubleshooting Protégé and GraphDB, checking the triple count, and suggesting SPARQL queries. The modelling, implementation and report are my own work. Details are in the report.

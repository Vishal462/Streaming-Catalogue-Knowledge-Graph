# Streaming Catalogue Knowledge Graph

An RDF knowledge graph and small RDFS vocabulary for a fictional streaming service. It models films, a series and its episodes, contributors and their roles, genres, language versions, regional licences and availability periods. Built in Protégé, stored and queried in GraphDB.

## Files

| File | Description |
|---|---|
| `streaming_catalogue_final.ttl` | The ontology and data (vocabulary + individuals) in Turtle |
| `queries.rq` | The five SPARQL queries used in the report, with expected results |
| `report.pdf` | Report explaining the modelling decisions, implementation and results |
| `screenshots/` | Screenshots of GraphDB setup, query results and the visual graph |
| `README.md` | This file |

## Tools

- [Protégé](https://protege.stanford.edu/) [5.6.9] – building the vocabulary and individuals
- [GraphDB Free](https://graphdb.ontotext.com/) [11.5.1] – storing the graph, RDFS inference, SPARQL queries and visualisation

## Open in Protégé

1. Open Protégé.
2. **File → Open** → select `streaming_catalogue_final.ttl`.
3. Browse the **Classes**, **Object properties**, **Data properties** and **Individuals** tabs.\
   **View → Render by label (rdfs:label)** shows readable names.

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
6. Optional: **Explore → Visual graph** → search `Riverline` and expand nodes to see the subgraph.

## Expected results

| Query | What it shows | Expected result |
|---|---|---|
| Q1 | Triple count | 220 (inferred OFF), 342 (inferred ON) |
| Q2 | Person–role–work credits | 5 rows; Maya Sen is Actor on Riverline and Director on City Loop |
| Q3 | Titles available today | City Loop and Last Signal (Singapore); Riverline excluded as expired |
| Q4 | City Loop episodes | E1–E3 with durations PT45M, PT48M, PT50M |
| Q5 | RDFS subclass inference | 0 rows (inferred OFF), 6 rows (inferred ON) |

## Acknowledgements

- Protégé (Stanford University) and GraphDB (Ontotext) were used to build and query the model.
- Claude (Anthropic) and ChatGPT (OpenAI) was used for discussion of modelling options, troubleshooting Protégé and GraphDB, checking the triple count, and suggesting SPARQL queries. The modelling, implementation and report are my own work. Details are in the report.

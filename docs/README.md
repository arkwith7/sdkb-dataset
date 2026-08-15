# SDKB documentation index

Start here. The repository root [`README.md`](../README.md) tells you what SDKB *is* and how to
build it; this directory tells you what it *means*, where every number came from, and what it
does not do.

> 🇰🇷 이 색인은 영문입니다. 개별 문서는 한국어·영어가 섞여 있으며, 각 항목에 언어를 표시했습니다.

---

## Reading paths

**"I want to understand the ontology and possibly reuse it."**
→ [`ontology_guide.md`](ontology_guide.md) — module map, modelling decisions and their costs,
naming rules, three extension recipes, the release gate, the competency-question suite.
New to RDF/OWL, or new to semiconductors? Take the matching glossary first:
[`glossary_ontology.md`](glossary_ontology.md) (how knowledge is represented — with the five
defects this repo shipped by getting each concept wrong) ·
[`glossary_semiconductor.md`](glossary_semiconductor.md) (what is being represented).
Then run `make owl convert validate` and `make cq` on an empty checkout; nothing there needs
credentials.

**"I want to judge whether the data is fit for my purpose."**
→ [`datasheet.md`](datasheet.md) (Gebru-style, whole knowledge base) →
[`dataset_rejected_patents_card.md`](dataset_rejected_patents_card.md) (the patent layer, its
licence position, and its limits) → the *"What is empty, and how to fill it"* table in the root
README.

<!-- 공개본에서 뺀다: runbook · 점검 · references 는 공개본에 없다 -->
---

## Normative documents — the ones that constrain the data

| Document | Lang | What it fixes |
|---|---|---|
| [`datasheet.md`](datasheet.md) | EN | Motivation, composition, collection, uses, distribution, maintenance for the whole KB. §8 lists the publication-integrity constraints any paper using this data must respect. |
| [`dataset_rejected_patents_card.md`](dataset_rejected_patents_card.md) | KO/EN | The SIRP rejected-patent layer: provenance, schema, statistics, **§6 licence and redistribution**, §7 limits. |
| [`ontology_guide.md`](ontology_guide.md) | EN | Vocabulary, IRI policy, modelling decisions, extension procedure, validation gate. |
| [`glossary_ontology.md`](glossary_ontology.md) | KO (EN summary) | RDF / OWL / SHACL / SKOS terms as SDKB uses them, each paired with a real defect it caused here and the rule adopted after. |
| [`glossary_semiconductor.md`](glossary_semiconductor.md) | KO (EN summary) | The semiconductor domain the ontology models — processes, devices, patent lifecycle, classification, industry structure, export control — and where the model deliberately stops. |
| [`deidentification_protocol.md`](deidentification_protocol.md) | KO | How the expert profiles were generated and de-identified. 105 of 110 are programmatically generated; 5 are perturbed derivatives with originals never ingested. |

### Writing a document that must **not** ship publicly

Put `<!-- sdkb:private -->` on the **first line**, alone. `make public-release` then leaves the
file out of the public tree, and `make check-public` fails if it is there anyway. The marker is
recognised on the first line only — a document that *discusses* the token (this one, for
instance) is not affected.

Do not rely on writing "CONFIDENTIAL" in the text. That was tried and measured: the word matches
seven tracked files here and **all seven are ordinary documents**. A checker that cannot tell a
document containing secrets from a document discussing them gets ignored.

## Data documents — where the numbers come from

| Document | Lang | Contents |
|---|---|---|
| [`semiconductor_industry_rejected_patents_schema.md`](semiconductor_industry_rejected_patents_schema.md) | KO/EN | Field-by-field schema of the rejected-patent JSONL, including which KIPRIS API tag each field came from. |
| [`kipris_reject_dataset_source_mapping.md`](kipris_reject_dataset_source_mapping.md) | KO/EN | Source-field → dataset-field crosswalk. Read this before trusting any date column. |
| [`semiconductor_ontology_provenance_research.md`](semiconductor_ontology_provenance_research.md) | EN | Survey of the upstream ontologies and why each was adopted, referenced, or declined. |

<!-- 공개본에서 뺀다: 평가 기록과 문헌 노트는 개발 과정이라 공개본에서 뺀다 -->
## Architecture and alignment

[`project/`](project/) holds the documents that explain *why the artifact is shaped this way*:

| Document | Contents |
|---|---|
| [`project/architecture_amendment_sdkb_centric.md`](project/architecture_amendment_sdkb_centric.md) | Why external ontologies are referenced via SKOS rather than imported. The ontology itself cites this file via `rdfs:seeAlso`. |

<!-- 공개본에서 뺀다: 판정 근거 문서가 공개본에 없다 -->

---

## Two facts that trip up every first-time reader

1. **SIRP is 1,000 patents.** Older documents say 773 — that was the initial cohort snapshot, and
   the ground-truth pairs are frozen at it. Both numbers are correct in their own sentence; never
   substitute one for the other.

2. **The two ground-truth tracks are not the same thing and neither is human-expert annotation.**
   The 7,500 prior-art pairs are *examiner-grounded* (objective KIPO examiner citations). The
   7,800 three-rater ratings are *algorithmically simulated*. Describing either as expert
   annotation is a misrepresentation — see `datasheet.md` §8 #2.

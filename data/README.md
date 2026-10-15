# Data

Full export of the MongoDB collections behind Stiftungsfinder, as JSON Lines
(one document per line, MongoDB Extended JSON, sorted by `_id`). Exported on 2026-10-15.

| File | Source collection | Documents | Contents |
|------|-------------------|-----------|----------|
| `foundations-de.jsonl` | `henophilia.foundations-de` | 30,652 | German foundations: name, contact details, portrait text and foundation purpose (`purpose`) |
| `project-descriptions.jsonl` | `henophilia.project-descriptions` | 20 | Anonymous project descriptions entered by users of the app |
| `europe-programmes.jsonl` | `europeprogrammes.programmes` | 569 | EU funding programmes: name, description, objectives, URL, country |
| `foundations-nl.jsonl` | `fondseninnederland.foundations` | 362 | Dutch foundations: name, description, link, address, socials |

The app reads `foundations-de` and `project-descriptions` from the `henophilia`
database. The embeddings for the foundation purposes live in Pinecone and are not
part of this export.

## Restore

```sh
mongoimport --uri "$MONGODB_URI" --db henophilia --collection foundations-de --file data/foundations-de.jsonl
mongoimport --uri "$MONGODB_URI" --db henophilia --collection project-descriptions --file data/project-descriptions.jsonl
mongoimport --uri "$MONGODB_URI" --db europeprogrammes --collection programmes --file data/europe-programmes.jsonl
mongoimport --uri "$MONGODB_URI" --db fondseninnederland --collection foundations --file data/foundations-nl.jsonl
```

---
name: pandit
description: "Read records of the Pandit database (panditproject.org) of South Asian intellectual history: fetch a record as JSON, follow its links, show field titles, cite the record's address."
---

# Pandit Project: reading records with an AI engine

Pandit (https://panditproject.org) is a scholarly database of South Asian intellectual history: people, works, manuscripts, places and institutions. Everything below is public, anonymous and read-only. Use `GET` requests only. No login, no API key, no cookies.

Send an honest `User-Agent` that names your tool, and keep the request rate low (a few requests per second at most).

## 1. Fetch one record

```
GET https://panditproject.org/node/<id>?_format=json
```

The JSON holds the record's fields. Field keys are machine IDs such as `field_coll_catalog`. To learn what each ID means, use the field map (section 3).

Content types: `work`, `person`, `place`, `manuscript`, `institution`, `extract`, `print`, `collection`, `state`.

## 2. Follow references and paragraphs

- **Reference to another record** (`target_type` is `node`): the entry carries a `target_id`. Fetch `https://panditproject.org/node/<target_id>?_format=json`. (The `url` key in the entry is a relative link of the form `/entity/<id>/<type>`; use `/node/<target_id>` instead.)
- **Paragraph fields** (nested records such as `field_coll_print_authors` or `field_coll_catalog`): each entry carries a `target_id`. Fetch it with:

```
GET https://panditproject.org/entity/paragraph/<target_id>?_format=json
```

  A paragraph can hold references to other records; follow them the same way.
- A record or paragraph you cannot read (HTTP 403 or 404) is not public. Do not try to work around it.

## 3. Field map

```
GET https://panditproject.org/api/field-map
```

Returns JSON:

```
{
  "content_types":   { "<bundle>": { "label": "...", "fields": { "<field_id>": "<title>" } } },
  "paragraph_types": { "<bundle>": { "label": "...", "fields": { "<field_id>": "<title>" } } }
}
```

Use the record's `type` to pick the bundle under `content_types`, and a paragraph's `type` for `paragraph_types`. Show the scholar the title, not the machine ID. The map is cached; fetch it once per session.

## 4. Cite

Every statement you take from a record must name its Pandit URL, `https://panditproject.org/node/<id>` (without `?_format=json`), so the scholar can open the record. For facts held in a paragraph, cite the parent record's URL. Say when a field is empty rather than guessing.

## Not covered here

Search is not part of this file. The endpoints above never change data.

# Pandit skills

Skills that teach an AI assistant to read the [Pandit](https://panditproject.org)
database: people, works, manuscripts, places and institutions of South Asian
intellectual history.

A skill is a short instruction file. It tells the assistant how Pandit's records
are built and how to fetch them, so a scholar can ask questions in plain language
and get answers taken from Pandit, with a link to each record used.

## What the skill does

- Fetches a single Pandit record as structured data (JSON).
- Follows the links from one record to the related ones, for example from a work
  to its author or from a manuscript to its institution.
- Reads the nested parts of a record, such as the authors listed in a print.
- Translates Pandit's internal field names into their readable titles, using
  Pandit's field map.
- Cites the Pandit address of every record it uses.

The skill only reads. It never changes a record and needs no user account.

## Status

Phase 1: reading one record and the records linked to it.
Searching Pandit through the skill is planned for the next phase.

## How to use

1. Download the skill from this repository: the folder [`pandit`](pandit), which holds
   the file [`SKILL.md`](pandit/SKILL.md).
2. Add it to your AI assistant as a skill, or as custom instructions if your
   assistant has no skills feature.
3. Ask about a record by its Pandit address or its number, for example:
   "Summarize https://panditproject.org/entity/12345/person and list the works
   linked to it."

## Accuracy

An AI assistant can make mistakes. Check every answer against the record on
Pandit, using the links the assistant gives.

## Contact

Questions and problems: open an issue in this repository.

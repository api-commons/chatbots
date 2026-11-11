# Chatbots and Conversational AI

The common chatbot-platform vocabulary -- the bots, the conversations they hold, the messages in them and the intents they are trained on -- distilled from the APIs that already exist. Part of [Schema Commons](https://github.com/api-commons/schema-commons),
published by the [API Commons](https://apicommons.org).

Built from the providers tagged Chatbots, Chatbot, Conversational AI, Chat, Virtual Assistants, Live Chat in [APIs.io](https://apis.io) that
publish their own OpenAPI. Only harvested contracts count -- nothing API Evangelist
generated. Every number below is a count of providers.

## What the market already agrees on

<!-- commons:summary -->
| Concept | Expose it | Readable schema | Core properties (share) | Collection named |
| --- | ---: | ---: | --- | --- |
| bot | 16 | 14 | id 79%, name 64% | bots 9, assistants 5, bot 2, chatbot 1 |
| conversation | 62 | 57 | id 68% | conversations 40, chat 9, conversation 7, threads 7 |
| conversation_message | 30 | 23 | id 87%, content 78%, created_at 78%, role 70% | messages 30, message 2 |
| intent | 7 | 7 | name 71%, description 57%, id 57%, training_phrases 57% | intents 6, intent 1 |

Cohort: 147 providers with harvested OpenAPI, 69 crosswalks. Of the providers exposing a bot: 75% create, 81% list, 56% fetch, 50% update, 62% delete. Generated 2026-11-11 by build.py.
<!-- /commons:summary -->

Shares are of the providers with a readable resource schema for that concept. The
extended tier and the long tail of every concept are in [profile.yml](profile.yml).

## What the measurement shows

- The message is the shared shape: conversation messages agree on id, content, created_at and role, the same four fields an LLM chat turn carries, whether the platform is a support chatbot or an assistant.
- Conversations agree only on id; created_at reaches 42% and status 40%, because a conversation is a thread at one platform, a session at another and a ticket-like case at a third.
- Intents agree on name, description, id and training_phrases at the platforms that still train on them; LLM-first platforms replace intents with instructions on the bot.

## Artifacts

- [openapi.yml](openapi.yml) -- OpenAPI 3.1 of the shared operations. No one serves it; it
  is the shape to map to. Lints clean against the
  [naming ruleset](https://github.com/api-commons/schema-commons/blob/main/ruleset/schema-commons-naming.yaml).
- [schema/](schema) -- JSON Schema 2020-12 per concept; each property carries
  `x-commons-tier`, `x-commons-share`, `x-commons-providers` and the spellings seen.
- [crosswalk/](crosswalk) -- one per provider, common name -> their name, with the harvested
  spec and operations each mapping was read from.
- [adopters.yml](adopters.yml) -- who exposes which concept, linked to their APIs.io page.
- [concepts.yml](concepts.yml) -- the only hand-written input: concepts, path segments and
  their qualifiers, aliases, reviewed exclusions, merged duplicates, and the decisions below.
- [census/](census) -- the cohort and the raw census the profile is built from.

## Decisions

These are calls, not measurements, recorded so they can be revisited as the method matures.

- The message is conversation_message, because messaging owns message; role is kept as the canonical name for the sender's kind (user, bot, agent).

## Rebuild

```bash
../schema-commons/scripts/run.sh .
```

## License

Artifacts CC BY-NC-SA 4.0 ([LICENSE](LICENSE)); code Apache 2.0 ([LICENSE-CODE](LICENSE-CODE)).

Concept Explorer App
=====
an implementation of the Concept Graph Custom NIP (still in draft format)
-----

This is a client that enables a user to manage individual decentralized lists, structured lists, object oriented lists, and concepts. Management of the Concept Graph will be added later.

## Prerequisite Custom NIPs:
- [Graphical Organization of Decentralized List Items Custom NIP](https://nostrhub.io/naddr1qvzqqqrcvypzpef89h53f0fsza2ugwdc3e54nfpun5nxfqclpy79r6w8nxsk5yp0qyt8wumn8ghj7un9d3shjtnwdaehgu3wvfskueqqxfnhyctsdp5kxctv94hhyempde5h5ct5d9hkutt0vckkgetrv4h8gunpd35h5ety94kxjum5945hgetdwv0pgvsy)
- (more)

## dependencies

- Orly (??) or Brainstorm (???)
- neo4j
- SQL (?)
- JSON Schema.org: ajv ("another json-schema validator") or some similar driver
- visjs or some other visualization tool (or just neo4j ??)

# Storage

SQL and neo4j

### Data Download 

Download should happen automatically. But the settings page will also have a button to redownload all relevant data:

- all kind (3)9998, (3)9999, 7 from `aDlistRelays`
- logged-in user's 10040 from `aTrustedAssertionPreferenceRelays`, `aPopularRelays`, and `aOutboxRelays`
- logged-in user's 30382 from relay indicated in 10040

ALl data will go into SQL and into neo4j.

### SQL schema

A table of events:
- event id
- kind
- author
- tags
- content
- timestamp

### neo4j schema: all relationships will be downloaded from `aDlistRelays` using the filter:

```json
{
    "kinds": [9999, 39999],
    "#z": ["<naddr for relationships>"]
}
```

node types: 
- nostr: `NostrEvent`, `NostrUser`
- canonical Brainstorm Knowledge Graph: `ListHeader`, `ListItem`, `Superset`, `Set`, `JSONSchema`

properties: `kind`, `pubkey`

Any given neo4j node can be multiple node types. Example: Each "canonical" Brainstorm KG node will _also_ be a `NostrEvent` node type.

relationship types: 
- nostr: `AUTHORS`
- all canonical Brainstorm Knowledge Graph relationship types as listed below

properties: `wot_score` and `recognized_by_wot` will be properties of each "canonical" brainstorm knowledge graph node type and relation

# Pages

## Settings Page

The Settings page allows the user to manage items that are necessary for the app's function. Each item will be associated with either an event id or an naddr.

### Structural List headers

These are a list of kind 9998 and 39998 events that are integral to the formation of a Concept. These are also referred to as the "canonical" Brainstorm Knowledge Graph node types.

| list header | event id or naddr |
| --- | --- |
| relationships | 39998:e5272de914bd301755c439b88e6959a43c9d2664831f093c51e9c799a16a102f: |
| relationship types | 39998:e5272de914bd301755c439b88e6959a43c9d2664831f093c51e9c799a16a102f:826fa669-b494-46bd-9326-97b894c70d8b |
| node types | 39998:e5272de914bd301755c439b88e6959a43c9d2664831f093c51e9c799a16a102f: |
| sets | 39998:e5272de914bd301755c439b88e6959a43c9d2664831f093c51e9c799a16a102f: |
| supersets | 39998:e5272de914bd301755c439b88e6959a43c9d2664831f093c51e9c799a16a102f: |
| JSON schemas | 39998:e5272de914bd301755c439b88e6959a43c9d2664831f093c51e9c799a16a102f: |
| properties | 39998:e5272de914bd301755c439b88e6959a43c9d2664831f093c51e9c799a16a102f: |

### Relationship types

These are the "canonical" Knowledge Graph relationship types:

| relationship type | uuid |
| --- | --- |
| CLASS_THREAD_INITIATION | 39999:e5272de914bd301755c439b88e6959a43c9d2664831f093c51e9c799a16a102f:24bc3eb6-fd75-4679-a3d7-d0b1a2a62be8 |
| CLASS_THREAD_PROPAGATION | 39999:e5272de914bd301755c439b88e6959a43c9d2664831f093c51e9c799a16a102f:e65edc7b-5f33-436a-a7b5-c8092da85d18 |
| CLASS_THREAD_TERMINATION | 39999:e5272de914bd301755c439b88e6959a43c9d2664831f093c51e9c799a16a102f:cad330c4-be50-4fa0-8178-0982078b908a |
| IS_A_PROPERTY_OF | 39999:e5272de914bd301755c439b88e6959a43c9d2664831f093c51e9c799a16a102f:9a74ffbd-33c6-456a-a5a9-9711d504e81d |
| IS_THE_JSON_SCHEMA_FOR | 39999:e5272de914bd301755c439b88e6959a43c9d2664831f093c51e9c799a16a102f:86ac71be-eab8-4b15-bb17-313b8378d2e5 |
| ENUMERATES | 39999:e5272de914bd301755c439b88e6959a43c9d2664831f093c51e9c799a16a102f:d0b4f08e-df4a-4131-a75c-e5bd056e4d78 |

For each item, the user will have the ability to replace the default naddr with an naddr of the user's choosing. For each item, there will also be a button to restore default naddr.

### Relays

| name | relays |
| --- | --- |
| `aDlistRelays` | `wss://dcosl.brainstorm.world` |
| `aTrustedAssertionPreferenceRelays` | `wss://nip85.nostr.band`, `wss://nip85.brainstorm.world` |
| `aPopularRelays` | `wss://relay.damus.io`, `wss://relay.primal.net`, `wss://relay.nostr.band` |
| aOutbox | `null` |

For `aDlistRelays` and `aTrustedAssertionPreferenceRelays`, the user will have the ability to replace the dafault relays with relays of the user's choosing. There will also be a "restore defaults" for each of these options.

`aOutbox` should be redownloaded automatically. But there should also be a button to redownload on demand.

## Lists

`<baseUrl>/lists`

This will be a page that shows ALL DECENTRALIZED LIST HEADERS in the form of a table.

Every kind 9998 or 39998 event will be obtained, using the following filter:

```json
{
    "kinds": [9999, 39999]
}
```

For each list, there will be a _list header UUID_ which is ether an event id (for kind 9998) or naddr (for kind 39998).

The table of list headers will have these columns:
- name (plural) of the list header
- UUID
- list type: Simple DList, Structured List, Object Oriented List, Concept
- GrapeRank score of the list header (rank of list header author plus rank of author of each kind 7 + reactions minus rank of author of each kind 7 - reaction)
- link to its page (see below)

### List Types

We can use neo4j cypher queries to answer the following questions:

Question 1: Does list header have an associated list Superset node connected by a CLASS_THREAD_INITIATION relationship?

`MATCH p = (n:ListHeader {uuid:<uuid>})-[:CLASS_THREAD_INITIATION]->(s:Superset) RETURN p`

Question 2: Does list header have an associated Property node connected by a IS_A_PROPERTY_OF relationship?

`MATCH p = (n:ListHeader {uuid:<uuid>})<-[:IS_A_PROPERTY_OF]-(p:Property) RETURN p`

| Q1/Q2 | list type |
| --- | --- |
| N/N | simple |
| Y/N | Structured |
| N/Y | Object Oriented |
| Y/Y | Concept |

## Simple or Structured List: Table of List Items

`<baseUrl>/list/items?list_header_uuid=<list_header_uuid>`

This will be a page that shows information regarding a SINGLE structured list. 

This page will contain a list of each list item, in the form of a table. To obtain the list of items, use this filter:

Obtain from nostr (not preferred -- will probably deprecate):

```json
{
    "kinds": [9999, 39999],
    "#z": [<z-tag of the list header>]
}
```

or obtain from local storage (preferred):

```
MATCH (n:ListHeader {uuid:<uuid>})-[:CLASS_THREAD_INITIATION]->(s:Superset)
OPTIONAL MATCH (s)-[:CLASS_THREAD_PROPAGATION (between 0 and infinity)]->(sub:Set)-[:CLASS_THREAD_TERMINATION]->(i:ListItem {z:"<list_header_uuid>"})
RETURN ...
```

## Structured List: Tree Structure Graph

`<baseUrl>/list/structured?uuid=<list_header_uuid>`

This will be a page that shows a SINGLE structured list.

Data will be obtained from neo4j using the cypher query:

```
MATCH (n:ListHeader {uuid:<uuid>})-[:CLASS_THREAD_INITIATION]->(s:Superset)
OPTIONAL MATCH (s)-[:CLASS_THREAD_PROPAGATION (between 0 and infinity)]->(sub:Set)-[:CLASS_THREAD_TERMINATION]->(i:ListItem {z:"<list_header_uuid>"})
RETURN ...
```

Then show results of query graphically. 

## Object Oriented List

`<baseUrl>/list/object-oriented?uuid=<list_header_uuid>`



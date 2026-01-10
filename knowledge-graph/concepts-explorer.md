Concept Explorer App
=====
an implementation of the Concept Graph Custom NIP (still in draft format)
-----

This is a client that enables a user to manage individual decentralized lists, structured lists, object oriented lists, and concepts. Management of the Concept Graph will be added later.

## Prerequisite Custom NIPs:
- [Graphical Organization of Decentralized List Items Custom NIP](https://nostrhub.io/naddr1qvzqqqrcvypzpef89h53f0fsza2ugwdc3e54nfpun5nxfqclpy79r6w8nxsk5yp0qyt8wumn8ghj7un9d3shjtnwdaehgu3wvfskueqqxfnhyctsdp5kxctv94hhyempde5h5ct5d9hkutt0vckkgetrv4h8gunpd35h5ety94kxjum5945hgetdwv0pgvsy)
- 
# Pages

## Settings Page

The Settings page allows the user to manage items that are necessary for the app's function. Each item will be associated with either an event id or an naddr.

### Structural List headers

These are a list of kind 9998 and 39998 events that are integral to the formation of a Concept.

| list header | event id or naddr |
| --- | --- |
| relationships | 39998:e5272de914bd301755c439b88e6959a43c9d2664831f093c51e9c799a16a102f: |
| relationship types | 39998:e5272de914bd301755c439b88e6959a43c9d2664831f093c51e9c799a16a102f: |
| node types | 39998:e5272de914bd301755c439b88e6959a43c9d2664831f093c51e9c799a16a102f: |
| sets | 39998:e5272de914bd301755c439b88e6959a43c9d2664831f093c51e9c799a16a102f: |
| supersets | 39998:e5272de914bd301755c439b88e6959a43c9d2664831f093c51e9c799a16a102f: |
| JSON schemas | 39998:e5272de914bd301755c439b88e6959a43c9d2664831f093c51e9c799a16a102f: |
| properties | 39998:e5272de914bd301755c439b88e6959a43c9d2664831f093c51e9c799a16a102f: |

### Relationship types

| relationship type | event id or naddr |
| --- | --- |
| CLASS_THREAD_INITIATION | 39999:e5272de914bd301755c439b88e6959a43c9d2664831f093c51e9c799a16a102f:24bc3eb6-fd75-4679-a3d7-d0b1a2a62be8 |
| CLASS_THREAD_PROPAGATION | 39999:e5272de914bd301755c439b88e6959a43c9d2664831f093c51e9c799a16a102f:e65edc7b-5f33-436a-a7b5-c8092da85d18 |
| CLASS_THREAD_TERMINATION | 39999:e5272de914bd301755c439b88e6959a43c9d2664831f093c51e9c799a16a102f:cad330c4-be50-4fa0-8178-0982078b908a |

For each item, the user will have the ability to replace the default naddr with an naddr of the user's choosing. For each item, there will also be a button to restore default naddr.

### Relays

| name | relays |
| --- | --- |
| aDlistRelays | `wss://dcosl.brainstorm.world` |

## Structured Lists

This will be a page that shows ALL DECENTRALIZED LIST HEADERS in the form of a table.

Every kind 9998 or 39998 event will be obtained, using the following filter:

```json
{
    "kinds": [9999, 39999]
}
```

For each list, there will be a _list header UUID_ which is ether an event id (for kind 9998) or naddr (for kind 39998).

Each item on the table will have 3 columns:
- name (plural) of the list header
- UUID
- list type: DList, Structured, etc
- link to its page

## Structured List: List Items

This will be a page that shows information regarding a SINGLE structured list.

This page will contain a list of each list item, in the form of a table. To obtain the list of items, use this filter:

```json
{
    "kinds": [9999, 39999],
    "#z": [<z-tag of the list header>]
}
```

## Structured List: Tree Structure

This will be a page that shows a SINGLE structured list: the tree, in the form of 

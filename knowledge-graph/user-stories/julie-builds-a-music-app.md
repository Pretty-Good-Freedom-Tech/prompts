Julie Builds a Music App
=====

Julie builds an app called EPOCH Music. Musicians can upload their songs and assign each song into one or more genres, of which there are about 30 or 40, hardcoded by Julie.

She wants to empower users to find music. Of course, they can search by genre. But what if a user is looking for something that does not fit a well-defined genre? She decides to enable users to create *bounties* for songs, albums, and/or musicians based on a description that can be as detailed as desired. The user will decide, for example, to place a 5000-satoshi bounty for Songs That Employ Tree Imagery (I know someone who has a PhD in this). 

The first step in building any app is to make a list of lists.

Following the Decentralized List Custom NIP, Julie makes three kind 9998 List Headers:

- Song Bounties, event_id_a
- Artist Bounties, event_id_b
- Album Bounties, event_id_c

In her app, Julie vibe codes a new section called Musical Bounties. Users can Create a New Bounty, View Existing Bounties, and Claim a Bounty.

### Create a New Bounty

Bob is writing his PhD thesis on the use of trees in 18th century French Literature, gets bored, and decides to place a bounty on French Pop Songs That Employ Tree Imagery. To do this, he issues a kind 9999 event with z-tag pointing to event_id_a (above). The kind 9999 event has event id: `event_id_for_tree_songs`. He deposits 5000 sats, held in escrow by EPOCH Music, and selects options that each bounty will be 500 sats, max two bounties per pubkey, and will expire after 24 hours.  

### View Existing Bounties

Charlie goes to this page and scrolls existing bounties. He only sees bounties that are unclaimed and — most importantly — bounties that are claimable by Charlie. Charlie sees Bob’s bounty shows up on this page because Bob’s Trusted Assertion gives Charlie a rank score above 25. (Future: replace rank with other metrics, like Musical Taste.) It just so happens that Charlie has the perfect song in mind!! So he clicks a button and is taken to the Claim a Bounty page.

### Claim a Bounty

Charlie claims a bounty by publishing a kind 9999 event with a z-tag that points to `event_id_for_tree_songs`. 

## Future Improvements

Somewhere, ideally in EPOCH Music but it could also be elsewhere, users can react to bounties with kind 7 + and - reactions. Any user who submits songs to bounties which get lots of upvotes using this system will gain reputation for being great at musical recommendations. Conversely, a bad reputation for downvotes. This data can be gathered (elsewhere) and processed by GrapeRank into a score that indicates whether this user is trusted by your community to categorize music. These scores will be published by Brainstorm alongside `rank` with a descriptive name, like `musical_recommender_repuration_score` A future version of EPOCH Music will give users the option to pre-approve bounties based on this score rather than the rank score. To do this, EPOCH Music will have a settings page that reads your kind 10040 event and allows you to select whatever scores are found in that. It will not be necessary for EPOCH Music to have any preconceived notion or knowledge of `musical_recommender_repuration_score`.

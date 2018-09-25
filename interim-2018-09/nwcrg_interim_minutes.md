---
title: "NWCRG Sept. 25th 2018 Interim Meeting Minutes"
author: "Marie-Jose and Vincent"
geometry: "left=2cm,right=2cm,top=2cm,bottom=2cm"
numbersections: true
---

--------------------------------------------------------------------------------------

**Participants (alpha. order):**

- Cedric Adjih

- Josu Bilbao

- Steve Blumenthal

- Kerim Fouli

- Pablo Garrido

- Hirah Malik

- Marie-Jose Montpetit

- Dave Oran

- Vincent Roca

- Mihail Zverev

--------------------------------------------------------------------------------------

**All slides** are available at [https://github.com/irtf-nwcrg/rg-materials/tree/master/interim-2018-09]


# New work items for the group

## IETF103 Hackathon (20') (Vincent)

See slides.

CA: Volunteers to help in various aspects (e.g., base code, especially if it's Gardinet LibLC, organisation, etc.) but is engaged in another hackathon project for IETF103.

MJM, concerning the possibility to support in-network recoding: yes, it's nice to have, but the details on how this should be done should be left aside.

TODO (chairs): send an email to the list to clarify several aspects (e.g., licence and base code).


## FEC and NC performance evaluation (20') (Vincent)

See slides.

TODO MJM: ask XXX if they can provide channel loss models for 5G.


## Facilitating FEC and Network Coding adoption (40')

### FEC and NC for dummies (Vincent)

See slides.

MJM: do not focus too much on type of traffic to justify the use of block vs. sliding window codes, but rather on the application needs.

DO: Say also that there's no simple answer. Do we have enough packets to code over?

DO: It's dangerous to mention Shannon capacity as there are situations where sending over the capacity may help. Do not overly simplify things.

CA: simple hints on coding are useful (e.g., Wikipedia introduction to Reed-Solomon codes is too complex). Otherwise I'm lost with some aspects such as relationships between FEC and congestion control (what are the design issues rather than the solutions?).

MJM: it could be useful to have a table with existing FEC codes with pointers.

Globally this initiative is recognized as useful. This is not a tutorial on FEC/NC (insist on this) but rather a few ideas for background information.

TODO (chairs): continue on the list.


### FEC/NC and Congestion Control (Marie-Jose)

Goal is to explain why FEC/NC can be CC friendly. An I-D that explains why would be appreciated.

We need to find a leader on this topic (MJM does not believe to be the most appropriate person).
There are connections too with ICCRG.

TODO (MJM): go to the list for see if someone is interested in leading this work.


## Additional topics (10') (Marie-Jose)

AI and VR are good targets for FEC/NC. Those topics should be discussed.

TODO (MJM): send a message on the list and get ready to have a structured presentation during IETF103.


# Progress on existing I-Ds (10' or more depending on authors)

[https://datatracker.ietf.org/rg/nwcrg/documents/]

- (RG-Item I-D) NC for CCN/NDN: requirements and challenges

- (RG-Item I-D) NC and satellites

- RLNC I-D (expired): 
KF: there will probably have a new I-D version for IETF103 although it is not guaranteed. If there's one, there will be a presentation by KF ou Janus (probably remotely) during IETF103.

- Generic FEC API for sliding window codes.

VR: hopefully the I-D will benefit from the hackathon work.

- FEC for QUIC (the two I-Ds)

VR (on behalf of authors): no progress made so far since IETF102, not sure how far we can go before next meeting.

- New I-D to be submitted for IETF103: BATS code.


# About our NWCRG group

## A Github repo for the group (20') (Vincent)

(see slides)

[https://github.com/irtf-nwcrg/]
Seems very positive (at least from the chairs' viewpoint) so far.


## NWCRG milestones update (10')

[https://datatracker.ietf.org/rg/nwcrg/about/] (bottom of page).    

TODO (chairs): start discussion on the list and update them before or during IETF103.


## Something else?

# Wrapup and actions for IETF 103, Bangkok (10') (Chairs)

We'll meet during IET 103: [http://ietf.org/how/meetings/103/].
Physical or remote participation is important.

---------------------------------------------------------

# IETF 104 NWCRG Meeting minutes

Thursday, March 28, 2019, Afternoon session I, 13:50-15:50, Berlin-Brussels

* [Datatracker](https://datatracker.ietf.org/rg/nwcrg/) 
* [Github](https://github.com/irtf-nwcrg/rg-materials/)



### 00- Welcome, administrative and general matters
(Chairs) (10')

### 01- Hackathon feedback (Vincent Roca)

Sliding Window FEC codec project (SWiF Codec) and relationships with draft-roca-nwcrg-generic-fec-api.

Goals:    
 - design reference open-source codec, RLC-like, later RLNC;    
 - facilitate testing and adoption;    
 - debug the generic API (draft-roca-nwcrg-generic-fec-api).    
Progress:    
 - encoder almost done, test in progress, python wrapper in progress, started work on decoder;    
 - 4 problems in API fixed, 5 open problems remain.    
The hackathon will continue in Montreal.
The ultimate goal is to be able to show API is codec-indepedent by supporting at least 2 codecs in the hackathon.

No questions


### 02- "Quick status on Network coding and satellites I-D" (Nicolas Kuhn)
(draft-irtf-nwcrg-network-coding-satellites)

Feedback from NWC RG and DTN WG, assessed comments from Lloyd Wood.
New version spun based on this.
Looking to move to RGLC. Chairs proposed doing this after confirmation on the list.

No questions


### 03- "Quick status on Network Coding for Content-Centric Networking / Named Data Networking: Requirements and Challenges" (Kazuhisha Matsuzono)
(draft-irtf-nwcrg-nwc-ccn-reqs)    

Goal of draft is articulate challenges/requirements and encourage research directions.
Actual coding and protocol would be in new drafts.
Updates:    
 - added a backward compatibility section;     
 - added a section on security and privacy.     
Got some more comments, plan to address them, respin the draft, then try to get RG last call.

Commen (DaveO with ICNRG Chair hat on): give ICNRG a chance to review the next version, then we’ll have advice about readiness for NWCRG Last Call.


### 04- "RLNC Background and Practical Considerations / RLNC Based Symbol Representation" (Kerim Fouli and Muriel Medard, remote)
[draft-heide-nwcrg-rlnc-background and draft-heide-nwcrg-rlnc]

Separated background and symbol representation into different drafts.
New section in background arguing that symbol representation is an important target for standardization.
The only technical change to concrete symbol representation is to lay it out in 32-bit units.

Comments (Salvatore and DaveO) - in process of addressing them and will respond the draft
three aspects of security to address: data hiding, byzantine or pollution attacks, detection and corrections, verification

Q (Vincent): on slide 5, mentioned dynamic number of coefficients and symbols, with 4-bit field you’re are limited.    
A (Kerim): thought there was a large field and small field - will go back and check

A (Muriel): if using as a seed, lots of choices

Comment(Vincent): need to tradeoff flexibility with detailed and efficient symbol representation.    
A (Kerim): night have different symbol representations for different applications. (Muriel) already done different representations in the past

Q (Vincent): put all of them in one document or not? What’s the view for evolution?    
A (Kerim): not necessarily, might have different ones for different applications. Topic for further discussion. Having one to bash on is useful to act as a baseline and is concrete.
Comment (Vincent): Agree

Q (Vincent): plan to have seed flexibility?    
A (Kerim): have that part in the negotiation not the actual symbol representation (Muriel) goal of  draft is to have a baseline concrete representation


### 05- "Adding Forward Erasure Correction to QUIC" (François Michel)
[ArXiV preprint](https://arxiv.org/pdf/1809.04822.pdf)

FEC was originally in QUIC spec, but was removed to get closure on QUIC v1.0
did 2 initial implementations (google-QUIC and IETF-QUIC)
Uses a format that differs from current NWCRG direction - will need to be rethought
Protect stream chunks of fixed size E
-   no signaling needed to announce source symbols
-   no control overhead - only protect the user data
-   QUIC naturally handles padding so don’t need fixed source symbol size
-   and protect more than STREAM data
Packet-based approach as alternative:
-   Need explicit signaling to identify source symbols in coding window
-   increased overhead - use similar approach to the one in FECFRAME
-   Propose to explicitly signal that a packets has been recovered - use a dedicated frame fo this - looks like an ACK frame

Q/Comment (Nicolas) Looked at recovered frame. may be able to handle recovery and congestion widow with one mechanism.

    Check slides for performance experiments and results
    Also looked at how QUIC+FEC competes with plain QUIC

Q (Morten): how do you know whether to just protect the end. Does QUIC know this? 

A: Fin bit marks the end of the stream

Q (Morten): how does this interact with HTTP. Only when you close socket you protect last piece of data?

A: use separate streams (e.g. one per file/object. If pipelining can’t detect this.

Q (Morten): what’s the current thinking

A: seems to be use one file/object per store

Q (Morten): do you see advantage to integrate FEC into transport, as opposed to inserting above the datagram layer?

A: depends on whether the application depends on shape of the traffic, if so may be better to do application rather than transept FEC

Q (.CJ Juhn): what was RTT used in the experiment, separate results for different RTT?

A: did lots of experiments with different RTTs between 100-700ms. Not separated out in display of results

Comment(Vincent): Is there a single best approach? Conclusion is to experiment for now

Comment(DaveO): don’t bake it too much until QUIC groups decides on how they will do multi-path

Comment(Spencer Dawkins): experiments here might inform QUIC how to do multi-path.


### 06- "Coding for low latency" (Morten V. Pedersen) 

Video conferencing, AR/VR, Telesurgery, Cooperative driving: these need not just low latency but high reliability too
Advocates trading bandwidth for latency via coding in order to have sufficient reliability. 
Lots of IETF groups talk on and on about latency but don’t think coding…

Q (Vincent): did you contact the authors of the cited drafts (which have expired)?

A: yes, doing that


### 07- "About RLC/TinyMT32 standardisation at TSVWG: a quick feedback" (Vincent Roca)

we first missed the PRNG issue (Park Miller Linear Congruential PRNG is broken!)
for copyright and other reasons, need the code maintainers to write the specification 
specifying a PRNG for generating coding coefficients is complex. C specification raises interoperability issue - no spec separate from the code
sometimes rather subtle (negative value representation not standardized). Compiler may generate different results due to optimizer.
Decided to go with TinyMT32 PRNG (Tiny Mersenne Twister)
have table of first 50 values to check
Still needed: scaler to 4 or 8 bit subspace. Do that in FEC scheme, not in PRNG.
Good news: almost finished - reviewed by IESG.

Q (Morten): did you benchmark the time needed to seed the PRNG?

A: yes, should be considered - way it’s used in NC you need a large number of short sequences, so seeding is important.

Q (Morten): is this mandatory, recommended, or what?

A: not mandatory except for the RLC FEC scheme which mandates it


### IETF 105, July 2019

Next NWCRG meeting will be in Montreal, and don’t forget the Hackathon!



# IETF 104 NWCRG Meeting minutes


## nwcrg@ietf104-hackathon: Sliding Window FEC (SWiF) codec project

Saturday and Sunday, March 23-24th, 2019.    
[Hackathon wiki](https://trac.ietf.org/trac/ietf/meeting/wiki/104hackathon)    
[Github swifc repo](https://github.com/irtf-nwcrg/swif-codec)


## nwcrg meeting@ietf104

Thursday, March 28, 2019, Afternoon session I, 13:50-15:50, Berlin-Brussels     
[Meeting materials](https://github.com/irtf-nwcrg/rg-materials/tree/master/ietf104-2019-03)     
[Meetecho record](https://play.conf.meetecho.com/Playout/?session=IETF104-NWCRG-20190328-1350)


### 00- Welcome, administrative and general matters
(Chairs) 

### 01- Sliding Window FEC (SWiF) codec hackathon project feedback (Vincent Roca)

A first goal of the Hackathon project is to design reference open-source codecs (RLC-like first, later RLNC) in order to facilitate adoption.
Another goal is to improve the generic API I-D (draft-roca-nwcrg-generic-fec-api).    

Progress made on the SWiF codec:    
 - encoder almost done, test in progress, python wrapper in progress, started work on decoder;    
 - 4 problems in API fixed, 5 open problems remaining.    
The hackathon will continue in Montreal (finish decoder?). Then we'll continue with RLNC support (Singapore?).

No questions.


### 02- "Quick status on Network coding and satellites I-D" (Nicolas Kuhn)
(draft-irtf-nwcrg-network-coding-satellites)

Feedback from NWC RG and DTN WG, assessed comments from Lloyd Wood.
New version spun based on this.

Comment (Chairs): Looking to move to RGLC. Chairs proposed doing this after confirmation on the list.

No questions.


### 03- "Quick status on Network Coding for Content-Centric Networking / Named Data Networking: Requirements and Challenges" (Kazuhisha Matsuzono)
(draft-irtf-nwcrg-nwc-ccn-reqs)    

Goal of draft is to articulate challenges/requirements and encourage research directions.
Actual coding and protocol proposed solutions would be in new drafts.
Updates:    
 - added a backward compatibility section;     
 - added a section on security and privacy.     
Got some more comments, plan to address them, respin the draft, then try to get RG last call.

Comment (DaveO with ICNRG Chair hat on): give ICNRG a chance to review the next version, then we’ll have advice about readiness for NWCRG Last Call.


### 04- "RLNC Background and Practical Considerations / RLNC Based Symbol Representation" (Kerim Fouli and Muriel Medard, remote)
(draft-heide-nwcrg-rlnc-background and draft-heide-nwcrg-rlnc)

Separated background and symbol representation into two different drafts.
Latest comments (Salvatore and DaveO) will be addressed in next version.

Q (Vincent): On slide 5, you mention a dynamic number of coefficients/symbols but with a 4-bit field you’re are rather limited.    
A (Kerim): We thought there was a large field and small field. I will go back and check.    
A (Muriel): If using as a seed, it's different, you have more choices.    

Comment (Vincent): Need to tradeoff flexibility with detailed and efficient symbol representation. It's a difficult exercise that needs to be discussed on the list.     
A (Kerim): We might have different symbol representations for different classes of applications.     
A (Muriel): We already had different representations in different implementations in the past.     

Q (Vincent): Do you intent to include more representations in this document? What’s the view for evolution?    
A (Kerim): Not necessarily, might have different documents for different applications and different representations.
	Topic for further discussion. Having one to bash on is useful to act as a baseline and is concrete.    
Comment (Vincent): Agree.

Q (Vincent): Plan to have PRNG (pseudo-random number generator) flexibility?    
A (Muriel): Goal of  draft is to have a baseline concrete representation. It's a narrow but concrete and useful contribution.    


### 05- "Adding Forward Erasure Correction to QUIC" (François Michel)
[ArXiV preprint](https://arxiv.org/pdf/1809.04822.pdf)

FEC was originally in QUIC specifications, but was removed.
We did an independent FEC implementation, with a totally different design than the current NWCRG direction.
Instead of fixed size source symbols, we work at QUIC packet payload level and protect the transported frames, regardless of their nature.
This packet-based approach:
 - solves the last symbol issue of NWCRG FEC for QUIC approach;
 - protects any number of STREAM data flows transparently;
 - but modifies any source packet and increases the packet size which in turn can create issues.
Note that QUIC naturally handles padding so we don't need fixed source symbol size any more.
We propose to explicitly signal that a packet has been recovered, using a dedicated RECOVERED frame that looks like an ACK frame but does not trigger any retransmission.
Check slides for performance experiments and results. We also looked at how QUIC+FEC competes with plain QUIC. Results are already interesting.

Q (Nicolas): Have you considered sending an ECN signal? May be able to handle recovery and congestion window with one mechanism.
A: Yes, agree. We can discuss on having a new frame or not.

Q (Morten): How do you know whether to just protect the end. Does QUIC know the size of the file being sent? 
A: A FIN bit marks the end of the stream. When we see this bit, we add redundancy.
We do the same when all streams are blocked by application, we send redundancy.

Q (Morten): how does this interact with HTTP when pipelining several files in the same connection?
	Is it only at the end, when you close socket you protect last piece of data?
A: Either you use separate streams, one per file, and in that case you know when we are reaching the end of a file.
	Or there is a single stream where all files are concatenated one behind another, and in that case we can't detect the end of file.

Q (Morten): Do you know what’s the current thinking on this?    
A: It seems the idea is to use only one file (or correlated files) per stream, and uncorrelated files in different streams.

Q (Morten): do you see advantage to integrate FEC into transport, as opposed to inserting above the datagram layer in the application?    
A: If the application knows the features of its traffic, it may be better to do FEC within the application rather than at transport.
	But doing that at transport level also simplifies the application design.
	There are use-cases for both approaches.

Q (CJ Juhn): What was the RTT used in the experiment? Do you have separate results for different RTT?
A: We did lots of experiments with different RTTs between 100-700ms. They are not all displayed here.

Q (Nicolas): What QUIC implementation did you use?
A: We used two, QUIC-Go and now picoquic.

Comment (Vincent): There are different design goals and properties. We already discussed with François and goal is now to experiments both types of solutions.
	We will update our two I-Ds to include support to both approaches.

Comment (DaveO): don't bake it too much until QUIC groups decides on how they will do multi-path.

Comment (Spencer Dawkins): Strongly agree with DaveO with the exception that experiments here might inform QUIC how to do multi-path.


### 06- "Coding for low latency" (Morten V. Pedersen) 

Video conferencing, AR/VR, Telesurgery, Cooperative driving: these need not just low latency but high reliability too.
Advocates trading bandwidth for latency via coding in order to have sufficient reliability. 
Lots of IETF groups talk on and on about latency but don't think coding...

Q (Vincent): Did you contact the authors of the cited drafts (which have expired)?    
A: Yes, we're doing that.


### 07- "About RLC/TinyMT32 standardisation at TSVWG: a quick feedback" (Vincent Roca)

We first missed the Pseudo-Random Number Generator (PRNG) issue -- we've long relied on Park Miller Linear Congruential PRNG which is broken for this usage.
Then we moved to TinyMT32, but for copyright/licence reasons, we had the code maintainers to co-author a specific I-D on the topic.
Specifying a PRNG from its C code also raises interoperability/deterministic behaviour issues, sometimes rather subtle (negative value representation is not standardized in C).

Q (Morten): Did you benchmark the time needed to seed the PRNG?    
A: Yes, we did it and it's important -- using a PRNG to produce coding coefficients means that you need a large number of short sequences (rather than a single very long sequence). We did not identify any issue here.

Q (Morten): is this PRNG mandatory to use, recommended, or what?    
A: It's only mandatory to use for the RLC FEC scheme which relies on it.


### IETF 105, July 2019

Next NWCRG meeting will be in Montreal, and don't forget the Hackathon!



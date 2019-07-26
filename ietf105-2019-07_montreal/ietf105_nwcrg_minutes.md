# IETF 105 NWCRG Meeting minutes


## nwcrg@ietf105-hackathon: Sliding Window FEC (SWiF) codec project

Saturday and Sunday, July 20-21, 2018, starting at 9:00

* [Hackathon wiki](https://trac.ietf.org/trac/ietf/meeting/wiki/105hackathon)    
* [Github swif-codec repo](https://github.com/irtf-nwcrg/swif-codec)    


## 2- nwcrg meeting@ietf105

Friday, July 26, 2019, Morning session I, 10:00-12:00


#### 00- Welcome, administrative and general matters
(Chairs)    
NB: FECFRAME-ext/RLC/TinyMT32 standardisation @ TSVWG: three documents entered RFC Editor Queue.

C (Dave Oran, ICNRG chair hat): The base protocol stacks for CCN are published for RFC. 
We have a stable base to do the binding with network coding. 
We should change the RFC version in the documents. 


#### 01- Hackathon feedback: Sliding Window FEC codec project (SWiF Codec)
(Vincent Roca)    

The goal is to design a reference and open source free codec for sliding window schemes. 
Another goal is to challenge the generic FEC API. 
Achievements of the hackathon are changing the licence, the encoder
is almost done and the decoder is in progress. The demo C-language application 
is almost done and the python wrapper is in progress. 
As expected the generic API was challenged and some corrections have 
been identified. 
A goal is to go for re-encoding starting from IETF107 hackaton.

Q (Carsten Bormann): How would you characterize the performance? Is it a proof of concept?    
A: Yes, goal is to have a POC.
Q (Carsten): What level of performance are you expecting?    
A: Lots of improvements could be envisioned. The objective is to have something functional and open source.
If anybody further improves the codec raw performance and releases the source code, that would be great, but it's not our goal.


#### 02- "Status Network coding and satellites I-D"
(Nicolas Kuhn)     
(draft-irtf-nwcrg-network-coding-satellites)

RGLC process: comments from John Border and Lloyd Wood and Vincent Roca.
See the updates on the slides and the draft
 
Q (Dave Oran): in or above network layer (above means no re-encoding in the router)?    
A: both - and the document is clear about it - no layer 2 coding.
 
Q (Stew Card): what are the “C” is the architecture picture?   
A: this is where we could put the coding.
 
C (Vincent): Since you sent your email to the list after updating the I-D, no comment on the two open issues has been received on the list. Please make it clear that you want to close the issues and send it on the list. 
Then address the comments recently received from Stuart Card and we'll start a new RGLC.


#### 03- "Update of the Coding for QUIC document"
(Vincent Roca)     
(draft-swett-nwcrg-coding-for-quic)

Q (Dave Oran): Do you have senses whether one scheme is more relevant for multipath or not?    
A: Have to look more carefully, but the new per-packet solution is probably more suited.    
Q (Dave Oran): Based on your current coding, you may want to adapt the level of coding depending on the feedbacks in RECOVERED frames received from the client. Have you considered it?   
A: RECOVERED frames might be used to piggyback information to the server and help the server to adapt the coding scheme. This was not the rationale but could be doable.    

Q (Stuart Card): Be cautious about not protecting ACK - it may have negative implications.        
A it is something we discussed between us, it seemed to be meaningful, but we can change it if needed.        
Q (Dave Oran) Seems oriented towards systematic codes.    
A: We can avoid sending sources packets, it is not a big deal. It's pretty flexible.    
Q (Dave Oran): I do not need to consider repair packets in some implementations.
A: (MJM) it is a systematic code because FEC helps providing reliability, and it is more an evolution of existing QUIC.    
Q (Dave Oran): Just consider non systematic codes in case.   
Q (Brandon Williams): I do not have a clear indication whether this approach works with the API document.    
A: These are separated documents for separate aspects - there may not be much dependency between the two.    
Q (Brandon): Some QUIC orientations may impact the API document - just consider it.    
Q (John Border): There is a non systematic code that could be relevant for satellite use case.    
Adapting the coding to , e.g., rain fades could be relevant.    
A: It can be done with sliding window schemes. We want the design to be flexible.    
Q (Stuart Card): compatible with Hybrid-ARQ type I and type II?   
A: Trying to assess the difference between the two versions of HARQ.    
A: the constraints is related to the sliding window scheme that may not have the packets in the buffers to retransmit already sent packets.    

Q (Dave Oran): The N bit seems redundant with S bit, no?     
A: Adding the N in the first chunk only is optional at the moment. We need to go deeper in that.    
A: In any case we need to clarify many details before going to the QUIC WG.


#### 04- "Coding for QUIC Reference Implementation"
(François Michel - remote)     

Q (Vincent Roca): How any implementations do you currently have?    
A 3 versions at the moment.    
Q (Vincent Roca): Which ones are you going to keep?    
A We plan to go on with QUIC-GO and SIGCOMM versions


#### 05- "Another FEC for QUIC Implementation"
(Mihail Zverev, Ikerlan - remote)     

Q (MJM): We do not know which QUIC+FEC is best. Merging the solutions may not be a good idea. When we started to work with Google, we were going to let operators use the coding solution they want. I do not think there is a way to efficiently merge the FEC solutions. 

Q (MJM): The fact that you are coding after the encryption, repair packets can be seen on the wire. How would you consider security issues?    
A: Dealt with QUIC - you may not see whether the packets are repair packets or not. But we need to further look at that.    

Q (Nicolas Kuhn): You may want to consider RTT of 500 ms, 20 Mbps (download) and 5 Mbps (upload) for the SATCOM access.    
    
Q (Michael Welzl): Relationships between your solution and congestion control. You are not changing the congestion control within QUIC. Do you assume losses do not play a role?     
A: We report the losses.    
Q (Michael): Will have to check the details in the paper.     
Q (Brandon Williams) The characteristics you want from the network and the need of the application may not be accessible with encrypted traffic.     
A We can see what packets are reliable or not. This implementation is embedded into QUIC, so we can see the priorities.     
Q (Brandon): Can you selectively apply FEC between different streams?    
A At the moment, no, FEC is applied to all traffics.
Q (Brandon): Do you plan to work on adapting the FEC when needed?     
A: This is not what we look at the moment.     
Q (Brandon): It is gonna be important. It will come up in the discussions for FEC in QUIC.     

Q (MJM): There's lots of work on interaction between CC and coding. At the moment, you correct all the losses and the CC does not know the nature of the losses. This is particularly important in congested network where congestion losses would be recovered with the proposal. If you get into complicated architectures with various segments characteristics, things would be more complicated. 


#### 06- "Links with other Groups and Initiatives (COINRG, ICNRG, LOOPS)"
(Marie-Jose Montpetit)    

Q (Carsten Bormann): This is not hop-by-hop it is meant to be used on path segments.    
A: Yes, I was meanig path segments.    
Q (Carsten): FEC is only one option, retransmission is another. The main point is "don't look, don't touch", we do not care about the protocol that is used.     
A: There is a QUIC based solution that can be looked at.     
Q (Carsten): In LOOPS, we do not look at the host.     
A: There is collaboration going-on. NWCRG ended up as being a research group because IETF was not ready. But the group focuses on real world deployment. 
The type of work described in LOOPS is already being deployed and exploits FEC. I am talking about collaboration between a research group and a (potential) group.     
Q (Carsten): There is something that can be standardized in LOOPS.



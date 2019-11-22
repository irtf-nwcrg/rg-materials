# IETF 106 NWCRG Meeting Agenda (v3)

* [Datatracker](https://datatracker.ietf.org/rg/nwcrg/) 
* [Github](https://github.com/irtf-nwcrg/rg-materials/)


## 1- nwcrg@ietf106-hackathon (Saturday and Sunday, Nov. 16-17, 2019)

* [Hackathon wiki](https://trac.ietf.org/trac/ietf/meeting/wiki/106hackathon)    
* [Github swif-codec repo](https://github.com/irtf-nwcrg/swif-codec)    


## 2- nwcrg meeting@ietf106 (Thursday, Nov. 21, 2019, Afternoon session I)
Notes taken by Nicolas K., Cedric A. and Oumaima A. Thanks to them.

#### 00- Welcome, administrative and general matters (Chairs) 

##### Situation of the "NC for CCN/NDN: requirements and challenges" I-D    
Not presented today.    
Vincent Roca (VR):  Dave, you mentioned at ietf104 that it would be fine to first have a discussion at ICNRG first before coming back to RGLC. Did the ICNRG group made any progress?
Dave Oran (DO): You are on the spot - I have got not feedback on ICNRG on the document. 
Vincent Roca (VR): Let us know when you think a RGLC is possible.
DO: We gave ICNRG one month, and maybe move on no matter. Of course, I need confirmation from my co-chairs.

##### Situation of the RLNC I-Ds: what's next?    

Not presented today.    
The authors asked the chairs to ask for feedback from the group. 
VR: A question for the group is whether we should adopt I-Ds as research group document? It would make sense for me.   
Marie-José Montpetit (MJM): I support Vincent. A goal of the group was also to have a document for existing solutions (BATS, RLC, RLNC, Tetrys, etc.)i,     
Emmanuel Lochin (EL): regarding TETRYS document, Jonathan D. added some text recently and the authors do not think there is much more needed.   
MJM: You should publish that updated version so that the group can adopt it.    
EL: Is there interest for the group for the document?    
MJM: This is in the charter, yes. 


##### News from the FECFRAME-ext/RLC/TinyMT32 standardisation (TSVWG)

Vincent(Slides): Just waiting for final approval, the documents are ready


#### 01- Sliding Window FEC (SWiF) codec hackathon feedback (Vincent Roca) 

Vincent thanks Oumaima and Cedric who both made many contributions to the codec since previous IETF.
MJM emphasized that the hackthon is really a great opportunity to see what other people are doing in the other groups, because ther rest of the week we are all scattered together

### Updates of existing works:    

#### 02- Update of the "Coding techniques for satellite systems" I-D (Nicolas Kuhn)
(draft-irtf-nwcrg-network-coding-satellites)    

All the comments from LLyod and VR have been answered (see details in github I-D repository for Lloyd comments).
Some satellite vocabulary (satellite "payload" and "FECFRAME" in the satellite context) may create confusion at IETF and these terms have been removed.
Authors think the document is ready for another round of Last Call.    

VR: There are still editorials issues, volunteers are welcome. Anyway MJM and VR will read it again. VR, as document sheperd, will take care of this.


#### 03- Update of the deployment of BATS code (Raymond W. Yeung)
[https://datatracker.ietf.org/doc/draft-yang-nwcrg-bats/]    

Raymond (RY) presents updates on the current use-case (smart lampposts) for BATS codes.

EL: (slide 8) We know that TCP is collapsing in such use cases. Do you use TCP?
RY: We use UDP.
EL: There is no feedback and no fairness. If you share multiple flows, what happens? 
RY: In our experiments, we have only one flow.
EL: So do you use congestion control or something like this?
RY: There is only one link in the network, and it links lamppost with each other. 
EL: Is it within the application protocol (if is there an application protocol), or is it added to UDP? 
RY: Let's take it offline. 
VR: What is your target with this I-D?
RY: We would like to have a standard describing BATS.
VR: This is a research group, so it will not be an IETF standard but it can be published as an informational or experimental RFC. 
DO: Are there any IPR disclosure in terms of rights?
VR: We know from the beginning that there are IPRs with BATS solution, RY has always been very clear on this.
DO: What are the people rights when they use it for IRTF work (i.e., the licencing conditions)?
Colin Perkins (CP): the important question is: has an IPR disclosure been made at IETF? If not, you have to make one first (see: [https://datatracker.ietf.org/ipr/]).
MJM: Having a list of existing FEC solutions is one goal of the group - that is what people outside the group ask for.
Provide the IPR disclosure, then we'll continue and ask for document adoption.


#### 04- Update of the "RLC FEC Scheme for QUIC" I-D (Vincent Roca)
(draft-roca-nwcrg-rlc-fec-scheme-for-quic)     

VR presents (without chair hat).

Carsten: Do you have an intuition about the choice of E (i.e., the symbol size)?
VR: (slide 8) the E value is the symbool size value, it is something important in practice.
Having a large E while incoming source packets are all small leads to producing large repair symbols which adds overhead.
A smaller E value is preferable, in particular for variable size incoming packets.
However a too small E value increases the number of variables in the underlying linear system. hence more processing overhead.
There is a balance to find which is use-case dependent and I dont have any definite answer.

EL: Are you piggybacking the repair symbols at the end of the packet?
VR: Repair symbols are transported in REPAIR frames. They are sent in dedicated packets.
QUIC original packet are not modified (except for the addition of a SOURCE-FPI frame.
Emile Stephan (ES): Do you plan to write an extension to QUIC? 
VR: Our objective is to be in position to convince the QUIC WG that FEC can be useful to QUIC. Doing work in NWCRG enables to make progress on the design and to continue research on benefits it brings to QUIC.
We are also waiting for QUIC v1 to be done, then we will decide what is feasible.
MJM: the same Louvain team has a modular QUIC implementation that enables dynamic extensions to the protocol (see their SIGCOMM'19 paper). That could be another approach. 
ES: Why is this specific to QUIC?
VR: The signaling and the QUIC packet to source symbol mapping are specific for QUIC. The rest is common to RLC specification.
ES: It would be more general with UDP.
MJM: QUIC is not UDP.
VR: With FECFRAME (see soon to be published RFC 8680), you can apply FEC to UDP flows.
Carsten: [about LOOPS] We have something very similar, but the details of course are different.
VR: you just design FECFRAME to apply it to the usecase. Not a single FEC scheme for every use case. 
EL: Adding FEC to QUIC is different than adding FEC to UDP. On the repair format, is it optionnal? Is there a specific header for the repair frame? Is the header different whether I use optionnal symbol fields or not? 
VR: The repair header is specified in this I-D, and is the first part of the REPAIR frame. It is then followed by one or more repair symbols.
EL: Is it expected to work half-duplex and full-duplex? 
VR: There is no issue in doing both I think.
ES: Do you need to have the session key to add coding?
VR: No, everything happens before encryption. 


### New works:    

#### 05- "Coding and congestion control in transport" I-D (Nicolas Kuhn)
[https://datatracker.ietf.org/doc/html/draft-kuhn-coding-congestion-transport]    


Michael Welzl: the point is the sender is informed about the packet losses [...] ~what if the sender may not care about the all information ~~~ The sender may also not have accurate information and the client may not know exactly what to report (eg losing 5/10 packet, recovering 2/10).
NK: if you are using a new type of frame in quic you can do that - in general, it depends on the protocol carrying the data. 
Carsten: recovered may not necessary mean lost but just delayed. 
Dave: fine, but you miss the opposite case, what do you send if the sender ignores a recover packet? There is another dimension on the impact of the coding rate 
Spencer: thank you for the draft, you are at -00 and you have already lots of interests. You may want to consider scalable congestion controls and the history in the IETF on the reaction to ECN signals. 
MJM: this document has been in the charter of the RG from the beginning and this is an important document. 
EL: good point - I want to point out there is a contradiction between erasure coding, and doing congestion control - at the end - How we are going to manage both?
VR:  the goal of the document is not to manage all the problems, the goal is the bring some lights in this domain.
Carsten: why do you want to do congestion control? the pbvious answer is you want to protect the network. But you maybe want to have TCP-fairdness also, so maybe you should be clear about waht your objective here.
NK:  My objective is to manage congestion control while integrating FEC in QUIC end-to-end. The tunnels are out of the scope of the document, so we need TCP Fairness. 
Casrten: I may add an objective here, that is getting a review from the IESG,
Dave O: this is an RG; looking at the coding, 
  would be really be nice to put in the document, to guide the researchers to give some guidance, on what points need to be confirmed. because lots of of people could spend lots of time on the wrong idea
MJM: in the sake of time - cuting the line - suggesting that congestion control becomes an important items, bring back the research group item - 
MJM: nobody disagree

#### 06- Getting and Exchanging Decoding State Information (Cedric Adjih)


VR: we need to see what need to be done for the IPR that FEC codes may add to this. 

    Let s let them as implementation specific matters

    We will talk about it. 


### Relationship with other groups:

#### 07- About LOOPS (Local Optimizations on Path Segments) (Carsten Bormann)
(https://datatracker.ietf.org/doc/draft-welzl-loops-gen-info)     


Carsten: Who has been in the LOOPS side meeting?:
Half of the people in the room (approx 10/20) has attend to recent LOOPS meetings. 


DaveO: - is reordering one of the things you are not doing?Carsten: we may do reordering
Dave: Is it a requirement to take incoming disorder packets and reorder them in the tunnel?
Carsten: We do not know yet. 
MJM: with or without chair hat . How can we collaborate?
Carsten: we look at products from the research group. based on specific assumptions, we will have questions. 
MJM: we indeed have strong opinions on the different FEC. 
Carsten: I guess the WG asks specific questions - that may end up being a research question. 
EL: there are many research issues here. With tunnels, you may aggregate flows and the protection may be per-flow or on the aggregate - this may end up provocating head-of-line blocking. 

    I do not have the answer for that. You may have different sizes of flow and you have different coding schemes for the different flows. If the repaired packets belong to multiple flows, you may 

    end up having head of line blocking. 

Carsten: we will have issues in identifying the different flows and may not encounter this issue. Can you send the results on the list?
EL: sure.
MJM: if you do that, copy both (nwcrg+loops) lists. 
Collin: you list a bunch of FEC schemes with different characteristics. When we worked on video, we started with a simple scheme and went into more complexity. Do you expect the same thing? You may 

    end up having different FEC solutions for different use-case.

Carsten: we may want to dynamically change the FEC scheme that is used. 
MJM: you may want to add a specific signaling to detail the code that you want to use. 
Collin: You may also have ACK mechanisms that report different things depending on the FEC mechanism that is used. 
MJM: you may want the same type of interaction as T2TRG and CORE. 


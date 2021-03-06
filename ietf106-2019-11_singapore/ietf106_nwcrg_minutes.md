# IETF 106 NWCRG Meeting Minutes (v1)

* [Datatracker](https://datatracker.ietf.org/rg/nwcrg/) 
* [Github](https://github.com/irtf-nwcrg/rg-materials/)


## 1- nwcrg@ietf106-hackathon (Saturday and Sunday, Nov. 16-17, 2019)

* [Hackathon wiki](https://trac.ietf.org/trac/ietf/meeting/wiki/106hackathon)    
* [Github swif-codec repo](https://github.com/irtf-nwcrg/swif-codec)    


## 2- nwcrg meeting@ietf106 (Thursday, Nov. 21, 2019, Afternoon session I)
Notes taken by Nicolas K., Cedric A. and Oumaima A. Thanks to all of them!

#### 00- Welcome, administrative and general matters (Chairs) 

##### Situation of the "NC for CCN/NDN: requirements and challenges" I-D    
Not presented today.    
Vincent Roca (VR):  Dave, you mentioned at ietf104 that it would be fine to first have a discussion at ICNRG before coming back to RGLC. Did the ICNRG group make any progress?    
Dave Oran (DO): You are putting me on the spot - I have got no feedback on ICNRG on the document.     
Vincent Roca (VR): Let us know when you think a RGLC is possible.    
DO: We gave ICNRG one month, and maybe move on no matter. Of course, I need confirmation from my co-chairs.    

##### Situation of the RLNC I-Ds: what's next?    

Not presented today.    
The authors asked the chairs to ask for feedback from the group.     
VR: A question for the group is whether we should adopt I-Ds as research group document? It would make sense for me.       
Marie-José Montpetit (MJM): I support Vincent. A goal of the group was also to have a document for existing solutions (BATS, RLC, RLNC, Tetrys, etc.).     
Emmanuel Lochin (EL): regarding TETRYS document, Jonathan (Detchart) added some text recently and the authors do not think there is much more needed.    
MJM: You should publish that updated version so that the group can adopt it.    
EL: Is there interest for the group for the document?    
MJM: This is in the charter, yes.     


##### News from the FECFRAME-ext/RLC/TinyMT32 standardisation (TSVWG)

VR (Slides): Just waiting for final approval, the documents are ready.


#### 01- Sliding Window FEC (SWiF) codec hackathon feedback (Vincent Roca) 

VR thanks Oumaima and Cedric who both made major contributions to the codec since previous IETF.
MJM emphasized that the hackthon is really a great opportunity to see what other people are doing in the other groups, because the rest of the week we are all scattered in many groups.

### Updates of existing works:    

#### 02- Update of the "Coding techniques for satellite systems" I-D (Nicolas Kuhn)
[https://datatracker.ietf.org/doc/draft-irtf-nwcrg-network-coding-satellites]     

All the comments from Lloyd Wood and Vincent Roca have been answered (see details in github I-D repository for Lloyd’s comments).
Some satellite vocabulary (satellite "payload" and "FECFRAME" in the satellite context) may create confusion at IETF and these terms have been removed.
Authors think the document is ready for another round of Last Call.    

VR: There are still editorials issues, volunteers are welcome. Anyway MJM and VR will read it again. VR, as document shepherd, will take care of this.


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
DO: What are the property rights when they use it for IRTF work (i.e., the licensing conditions)?    
Colin Perkins (CP): the important question is: has an IPR disclosure been made at IETF? If not, you have to make one first (see: [https://datatracker.ietf.org/ipr/]).    
MJM: Having a list of existing FEC solutions is one goal of the group - that is what people outside the group ask for. Provide the IPR disclosure, then we'll continue and ask for document adoption.    


#### 04- Update of the "RLC FEC Scheme for QUIC" I-D (Vincent Roca)
[https://datatracker.ietf.org/doc/draft-roca-nwcrg-rlc-fec-scheme-for-quic]    

VR presents (without chair hat).    

Carsten Bormann (CB): Do you have an intuition about the choice of E (i.e., the symbol size)?    
VR: (slide 8) the E value is the symbol size value, it is something important in practice. Having a large E while incoming source packets are all small leads to producing large repair symbols which adds overhead. A smaller E value is preferable, in particular for variable size incoming packets. However, a too small E value increases the number of variables in the underlying linear system. Hence more processing overhead. There is a balance to find which is use-case dependent and I don’t have any definite answer.    
EL: Are you piggybacking the repair symbols at the end of the packet?    
VR: Repair symbols are transported in REPAIR frames. They are sent in dedicated packets. QUIC original packet are not modified (except for the addition of a SOURCE-FPI frame).    
Emile Stephan (ES): Do you plan to write an extension to QUIC?     
VR: Our objective is to be in position to convince the QUIC WG that FEC can be useful to QUIC. Doing work in NWCRG enables to make progress on the design and to continue research on benefits it brings to QUIC. We are also waiting for QUIC v1 to be done, then we will decide what is feasible.    
MJM: the same Louvain team has a modular QUIC implementation that enables dynamic extensions to the protocol (see their SIGCOMM'19 paper). That could be another approach.     
ES: Why is this specific to QUIC?    
VR: The signaling and the QUIC packet to source symbol mapping are specific for QUIC. The rest is common to RLC specification.    
ES: It would be more general with UDP.    
MJM: QUIC is not UDP.    
VR: With FECFRAME (see soon to be published RFC 8680), you can apply FEC to UDP flows.    
CB: [about LOOPS] We have something very similar, but the details of course are different.    
VR: you just design FECFRAME to apply it to the use case. Not a single FEC scheme for every use case.     
EL: Adding FEC to QUIC is different than adding FEC to UDP. On the repair format, is it optional? Is there a specific header for the repair frame? Is the header different whether I use optional symbol fields or not?     
VR: The repair header is specified in this I-D, and is the first part of the REPAIR frame. It is then followed by one or more repair symbols.    
EL: Is it expected to work half-duplex and full-duplex?     
VR: There is no issue in doing both I think.    
ES: Do you need to have the session key to add coding?    
VR: No, everything happens before encryption.     


### New works:    

#### 05- "Coding and congestion control in transport" I-D (Nicolas Kuhn)
[https://datatracker.ietf.org/doc/html/draft-kuhn-coding-congestion-transport]    


Michael Welzl (MW): About the statement that the receiver MUST inform the sender about recovered packets. Do you always want to inform you were able to recover a packet? It's an unreliable data transfer so you don't really need to inform the sender about recovered packets.    
NK: The smart things are at the sender because the sender knows more, in particular if it's unreliable.    
MW: I understand but I think it may be too much. If it's unreliable I don't care about retransmitting.     
NK: Okay, but it's all about a signal used to convey the information to the sender and let the sender adapt. You could also use a SACK to inform about what has been lost. With a new type of frame in QUIC, you could do that.    
For the moment it's just a basic statement on who knows what, and who indicates what to whom.    
CB: "Recovered" may not necessarily mean the packet has been lost, it may just be delayed.    
NK: If we want to go further in this document, this is the kind of things we need to put warnings on.    
DO: Fine, but you miss the opposite case: how many repair packets are you sending that turn out to be useless? It's a matter of measuring the usefulness of repair traffic. It gives an extra degree of freedom as you may want to play at the congestion control level or at the coding rate level.    
NK: Good point, that's the kind of topic we need to gather in the document. There are several corner cases that are very important. This point is about how you add coding inside congestion control. With this claim, we want to be generic.    
Spencer Dawkins (SD): Thank you for starting this work, you are at -00 and you have already lots of interests. This is good sign and I know people who need it.    
MW: I don't understand intuition. I think it does not make sense to do something half reasonable.    
NK: We need something in-between. We need to discuss this type of situation and find consensus in the group if possible.    
SD: We discussed in many RFC congestion control. I encourage you to include scalable congestion control and the IETF history on the reaction to ECN signals.     
EL: Good point. I want to point out there is an antagonism between using erasure coding (temptation to add redundancy if there are losses) and congestion control (it reduces transmission rate in case of losses). How we are going to manage both? That's what we want to discuss.    
VR: The goal of the document is not to solve all the problems; the goal is to bring some light in this domain.    
CB: Why do you want to do congestion control? The obvious answer is you want to protect the network. But you may want to have TCP-fairness, so you need to be explicit about what your objectives are.    
NK: My objective is to have QUIC working on satellite links. We have issues in our network when we have losses. So, we need to manage congestion control while integrating FEC in QUIC, end-to-end. If we don't manage to find simple solutions here, FEC won't be deployed in QUIC because many people don't like it.    
CB: There's perhaps a 3rd motivation, getting by the IESG. Do you want to be fair or not?    
NK: The tunnels are out of the scope of the document, so we need TCP Fairness.     
DO: this is an RG, looking at the coding. It would be really be nice to put in the document that one goal is to guide the researchers to give some guidance on what points need to be confirmed. Because lots of of people could spend lots of time on useless research for wrong ideas.    
MJM/VR: This subject has long been a key topic for our group, thank you very much for the initiative. Does anybody object in having this a RG Item document? (nobody disagrees). Confirm on list.     


#### 06- Getting and Exchanging Decoding State Information (Cedric Adjih)


VR: Thanks. This is in parts an implementation specific matter. We have a flexible parameter setter and getter that uses a type-length-value approach. It could be used to have this implementation specific extension without adding extra complexity to the core API. Let's discuss this offline.


### Relationship with other groups:

#### 07- About LOOPS (Local Optimizations on Path Segments) (Carsten Bormann)
[https://datatracker.ietf.org/doc/draft-welzl-loops-gen-info]     


CB: Who has been in the LOOPS side meeting? Half of the people in the room (approx 10/20) did.    
DO: Is reordering one of the things you are not doing?    
CB: We may do reordering.    
DO: Is it a requirement to take incoming disorder packets and reorder them in the tunnel?    
CB: We do not know yet.     
MJM: With or without chair hat, how can we collaborate?    
CB: We look at outputs from the research group, based on specific assumptions, and we will have questions.     
MJM: We indeed have strong opinions on the different FEC.     
CB: I guess the WG asks specific questions, that may end up being research questions.     
EL: There are many research issues here. With tunnels, you may aggregate flows and the protection may be per-flow or on the aggregate. I do not have the answer for that. You may have different types of flows and different coding schemes for them. You may end up having head of line blocking.     
CB: We will have issues in identifying the different flows and may not encounter this issue. Can you send the results to the list?    
EL: Sure.    
MJM: If you do that, copy both NWCRG/LOOPS lists.     
CP: You list a bunch of FEC schemes with different characteristics. When we worked on video, we started with a simple scheme and went into more complexity. Do you expect the same thing? You may end up having different FEC solutions for different use-cases.    
CB: We may want to dynamically change the FEC scheme that is used.     
MJM: Add a specific signaling to detail the code that you want to use.     
CP: You may also have ACK mechanisms that report different things depending on the FEC mechanism that is used.     
MJM: You may want the same type of interaction between NWCRG and LOOPS as between T2TRG and CORE.     


To conclude: NWCRG will met during ietf107, hackathon included.


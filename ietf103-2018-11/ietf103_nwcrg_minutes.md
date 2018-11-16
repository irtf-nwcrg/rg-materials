# IETF 103 NWCRG Meeting Minutes

__More information on the research group in the [datatracker](https://datatracker.ietf.org/rg/nwcrg/) and [Github](https://github.com/irtf-nwcrg/rg-materials/).__

First version of minutes taken by Nicolas Kuhn. Great thanks to you!

## nwcrg@ietf103-hackathon

Saturday and Sunday, November 3-4, 2018.    
[Hackathon wiki](https://trac.ietf.org/trac/ietf/meeting/wiki/103hackathon)    
[Github swifc repo](https://github.com/irtf-nwcrg/swif-codec)


## nwcrg meeting@ietf103

Monday, November 5, 2018, Morning session I, 9:00-11:00.         
[Meeting materials](https://github.com/irtf-nwcrg/rg-materials/tree/master/ietf103-2018-11)     
[Meetecho record](https://play.conf.meetecho.com/Playout/?session=IETF103-NWCRG-20181105-0900)

#### 00- Welcome, administrative and general matters (Chairs) 

The group moved from *just* doing codes from actually assessing its deployment in network system.
You may want to have a look at the GITHUB repository. 
Latests versions on the draft can be found there (even if they are not uploaded to the official datatracker). 


#### 01- "BATS Coding Scheme for Multi-hop Data Transport" (Raymond W. Yeung, remotely, Chinese Univ. of Honk Kong)
(draft-yang-nwcrg-bats-code-00)

Smart Lampposts are key infrastructure of smart cities (cameras and sensors). 
There are an estimated 70 millions of lampposts in next to be smart cities. 
There is a need for connecting these lampposts to the internet. 
The presentation went over the advantages and drawbacks of different accesses to do so:

  - optical fiber: pro (data rate, reliable), cons (price)
  - 4G: pro (easy deployment), cons (low bandwidth during rush hours)
  - multi hop hybrid solution with BATS

BATS coding solution that can deal with hundreds of hops and achieves low latency, high throughput
and a good compromise between 4G and optical fiber.

Other applications: wireless ad hoc networks, satellite networks, V2x, underwater, powerline, 5G.
Hong Kong Smart Lamppost Project is expected to use BATS code. 

Q (Rick Taylor - AIRBUS DEFENSE AND SPACE): Agree to the use case.
	The picture shows a single linear topology for the BATS codes, but in real life, you would have
	intersections and star topologies. How does your solution scale?    
A: You can radiate to more than one lamppost. 

Q (Rick Taylor - AIRBUS DEFENSE AND SPACE) : there is no congestion at that central nodes?     
A: you can always add more than one computer per lamppost. 

Q (Florin Baboescu - Broadcom) : What is the distance between lamppost?    
A: typically less than 50m but the physical layer can adapt to longer distances (e.g., with bigger antennas).

Q (Florin Baboescu - Broadcom): The capacity depends on the distance. With WiGig's band (in 60 GHz) that would matter. Have you looked at it?
A: We haven't done that yet but look close at this possibility.

Q (Florin Baboescu - Broadcom) : did you consider 5G technology (mostly on the backhaul)?     
A: at the moment now, we just have started looking into this.

Q (Florin Baboescu - Broadcom): Then how do you link this to 5G since release 16 of 5G is coming up and does not consider such cases.    
A: Because the application of NC has nothing to do with the physical layer, being implemented at the transport.

Q (Dave Oran - Independant Network Systems Research & Design): About the performance graph. Does that graph include or not hop by hop retransmissions at the lower layers?    
A: no it does not include retransmissions because real-time applications wouldn't be supported.

Q (Dave Oran - Independant Network Systems Research & Design): you should include additional results taking into account low layer retransmissions because the delay wouldn't be that large with such small distances. Also results showing the delay introduced by NC.
You seem to set up a best case comparison for NC: high loss with no hop by hop recovery. 
Of course it shows major improvements. It would be nice to show how it performs in other situations.
A: we have done some experiments but they are not shown. 

Q (Vincent Roca - INRIA): You have always been clear about IPR disclosure. I assume this I-D should be subject to an IPR-disclosure too.    
A: We'll do so, we didn't forgot.


#### 02- Hackathon feedback and Generic Sliding Window FEC API (Vincent Roca, Inria)

Sliding Window FEC codec project (SWiF Codec).
Objective of the hackathon: 

  - Design a reference and open-source, free SWiF codec (or set of codecs);
  - Challenge our generic API I-D;
  - (also) Test the FEC/NC for dummies document

Achievements: 

  - several fixes in the generic FEC API document
  - laid out github repository
  - major progress on the encoder 

However we are missing manpower. Please show up for next IETF.


__Concerning the draft-roca-nwcrg-generic-fec-api__

RG adoption ? 
The API I-D and SWiF codec hackathon project are supposed to evolve in parallel.

Q (Dave Oran - Independant Network Systems Research & Design): No issue in RG adoption, but need to
have workplan on how to have two different FEC codes.    
A: we focus on sliding window codes and it should be applicable to any sliding-window-coding scheme.
	During hackathon, RLC is our first target (especially given the limit manpower during hackathon),
	but (a certain variant of) RLNC is expected too.

Q (Rick Taylor - AIRBUS DEFENSE AND SPACE) : I agree with the aforementioned position. 
We may want to have two very different FEC codecs to challenge the generic API.     

A: we will go to the list to ask formal RG adoption. 


#### 03- "Quick status on Network coding and satellites I-D" (Nicolas Kuhn, CNES)
(draft-irtf-nwcrg-network-coding-satellites-00)

C (Vincent Roca): We may be close to the end for this document. Everbody is welcome to read.

Q/C (Rick Taylor - AIRBUS DEFENSE AND SPACE): Great DTN section.
	The DTN section should have references updated to IETF.
	DTN meeting on Thursday could bring some volunteers.    
A (Nicolas K.): will update the section and go to the DTN meeting.

C (Simon Pietro Romano, remotely): You might want to add a couple of references to ongoing ESA projects, like SHINE (NC to improve security of satellite-based CDNs).


#### 04- "Quick status on Network Coding for Content-Centric Networking / Named Data Networking: Requirements and Challenges" (Kazuhisa Matsuzono, NICT)
(draft-irtf-nwcrg-nwc-ccn-reqs-00)

Q (Vincent Roca): You have started implemented this. That's great. Do not hesitate to join hackathon.
A: We want to finalize a prototype of our NC for CCN/NDN proposal.

Q (Dave Oran - Independant Network Systems Research & Design - ICNRG hat on): We are about to 
release the draft on the CCN protocols. You should look at them to see if there should be changes 
in the packet format in ICNRG documents.    
A (Hitoshi Asaeda - NICT): we should not modify any CCN format in these almost done ICNRG documents now.
Packet extensions or modifications could be done later on and separately.


#### 05- "FEC and NC for dummies" (Vincent Roca, Inria)

Comment: dummies or newcommers?

Q (Rick Taylor - AIRBUS DEFENSE AND SPACE):
For idea 2, I would agree but think you should just speak about recovered and not repaired packets.
The word "repair" implies you are fixing broken packets which is not the case here.
A: we try to be consistent with the terminology RFC.
We will try to find something better that is also inline with the terminology document.

Q (Dave Oran - Independant Network Systems Research & Design): 
If you have lots of small objects that are independent and you're spraying them out on the network, a sliding window code is actually going to enforce certain types of ordering properties on the data and actually slow things down.
So we have to find another way to say this I think.
I suggest:
"If you have large data objects, you should go for block coding,"
"If you have streams of real-time data with time correlation, you should use sliding window."    
A: we agree that we need to add things about the size and the timing.

Q (Rick Taylor - AIRBUS DEFENSE AND SPACE): idea 7 does not show network improved networks. The improvement
is not clear. The Wi-Fi use case may not be a good one (WiFi multicast is particularly inefficient).

Q (Marie-Jose Montpetit - without chair hat): you should provide information of the losses patterns. Codes would 
have different performances in different cases. There are codes that are better with random losses while others
may be more robust in front of correlated losses (in bursts).
Many people have a very bad idea of how codes work with losses.
All FEC codes are not equivalent in front of various types of losses.

Q (Dave Oran - Independant Network Systems Research & Design) : if the reason you are having bursts of losses is linked
to some queue management, NC may not be a solution. 

C (Nicolas Kuhn - CNES): we may be able to provide satellite-based traces to the group. We need to confirm this.


#### 06- "FEC and NC performance evaluation" (Vincent Roca, Inria)

Q (Marie-Jose Montpetit - without chair hat): in the performance metrics slide (topic 2), you should mention residual losses. 
A: Yes, this is what is meant here, with real-time flow, we assess the required code rate to achieve a certain quality objective in terms of residual losses that can be tolerated with a given channel.

Q (Marie-Jose Montpetit - without chair hat): is it a loss profiles, i.e., measured, or loss model, i.e., generated using a theoretical model? I think we need both. 
A: yes, in this case (3GPP SA4 mobility), they are loss models, generated by taking account of the physical layer protection and propagation models.

Q (Nicolas Kuhn - CNES) : we should be aware on the OSI layer we are working at - otherwise this could lead to misleading conclusions. 
I'll try to be clear when we'll provide satellite traces on how it was provided.

Q (Marie-Jose Montpetit - without chair hat): in ns-3 and ns-2 simulations, there is no good code simulators.
We may want to go for a ns-2/ns-3 hackhaton for having codes and provide an organised ns2/3 repository of simulators. 
I suggest you add this to your slides.


#### 07- Milestones update (Chairs, all)
See [https://datatracker.ietf.org/rg/nwcrg/about/], bottom of page.

Milestones need to be udpated. Let's start discussing this here, we'll finish on the list.

Q: What are the plans for the NC and ICN draft?    
A (Kazuhisa Matsuzono): We still have to work on specific sections and will be back during the next IETF 104 in Prague.
We should be ready for WGLC at that moment.

Q (Dave Oran - Independant Network Systems Research & Design) (on the new milesones) There's a possible confusion in the wording with "computing in the network": how can NC help computing in the network and how to use computing in the network to implement NC.
A: yes, there are two things.

Q (Hitoshi Asaeda - NICT): NC with ICN as a solution is a new milestones (rather than from the requirements and challenges view point).
How can we express NC functions in an ICN wording? 
In this contexte collaborations with ICNRG could be envisioned.



#### 08- "In Network Computing Enablers for Extended Reality" (Marie-Jose Montpetit)

[draft-montpetit-coin-xr-01](https://tools.ietf.org/html/draft-montpetit-coin-xr-01)

Join the COIN side meeting on Friday morning.

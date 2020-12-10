# IETF 109 NWCRG Meeting Minutes

* [Datatracker](https://datatracker.ietf.org/rg/nwcrg/) 
* [Github](https://github.com/irtf-nwcrg/rg-materials/)
* [Meeting record](https://www.youtube.com/watch?v=rBGh7clvhUc)

## nwcrg online meeting

Online meeting on Tuesday November 17, 2020, 7:30-8:30 (UTC) Session II     
[Time Zone Conversion:](https://www.timeanddate.com/worldclock/fixedtime.html?iso=20201117T0730)

------------------

Participation will take place through Meetecho (please connect in advance):    
    - [Meetecho participant guide](https://www.ietf.org/how/meetings/109/session-participant-guide/)    
    - [links to Meetecho sessions](https://datatracker.ietf.org/meeting/109/agenda)

------------------

#### 00- Welcome, administrative and general matters
(Chairs) (10')

### Updates of existing works:    
#### 01- "BATS Coding Scheme for Multi-hop Data Transport" I-D
(Raymond Yeung) (10+5')     
(https://datatracker.ietf.org/doc/draft-yang-nwcrg-bats/)

Cancelled.


#### 02- "Coding and congestion control in transport" I-D
(Nicolas Kuhn) (10+5')     
(https://datatracker.ietf.org/doc/draft-irtf-nwcrg-coding-and-congestion/)    
Update of the document and new experimental results.

- MJM: it's important work as congestion control versus FEC always comes as a question. Do you know anybody doing research on it?     
- NK: we know LOOPS activity, we're in the process of adding a state of the art section in the document. We couln't do that for this meeting.     
- VR: it can be quite ambitious.     
- Morten V. Pedersen: it's important work. Could you clarify the situation where coding happens above the transport (e.g., above TCP that already corrects losses).     
- NK: we mean coding at application level. Right now we discuss all the possible cases. Sure it does not make sense if TCP is used underneath, and this is what we tried to explain.     
- Carsten Bormann: have you read this paper suggesting to replace the notion of fairness with the notion of "not doing harm". It is presented during the IRTF Open meeting ["Beyond Jain’s Fairness Index: Setting The Bar For the Deployment of Congestion Control Algorithms"](https://datatracker.ietf.org/meeting/109/materials/slides-109-irtfopen-beyond-jains-fairness-index-setting-the-bar-for-the-deployment-of-congestion-control-algorithms-00).     
- CB: I think the "FEC below transport" category should be called "FEC disconnected from transport". I think that most people realize that FEC has to send signals to the transport. So it's more a question of signaling between FEC and transport. If FEC and transport are integrated, this is implicit. But if you have different entities, as was the case with a Tetrys tunnel, then the interesting question is: how do you do this?  How do you actually send the signal? The only way that was found is through ECN marks. But to what extent can you actually minimize harm by doing so? Do you really have to completely emulate the situation where all losses indicate congestion or can you find some more intelligent ways? The FEC layer has more information about it than the congestion layer, and it would be nice to relay some of it to the congestion control, but they can only communicate using the language they understand. This is an area where interesting research questions are that I'd like to see in the document.      
- NK: For 1st part, I read paper and we should include it in the draft, but we are afraid to open the pandora box on fairness. We currently have lots of QoS mechanisms between users. It's something that needs to be discussed, and it's very policy oriented. The definition "not to harm others" is something we tried to map in this work. I would disagree however when you suggest to rename FEC below as FEC disconnected, because we mention all these situations where you can have signaling. And it's protocol specific. I would agree concerning the research question. Guarrantying QoE while keeping fairness to other flows is something we are currently covering, the definition of signals for the "FEC below transport" case may be not. 


### Additional presentations

#### 03- "Repair patterns for sliding window codes"
(Morten V. Pedersen) (10')

### Wrap-up, next steps
(Chairs, all) (5')

Chairs: We're short of time, let's continue on the mailing list.

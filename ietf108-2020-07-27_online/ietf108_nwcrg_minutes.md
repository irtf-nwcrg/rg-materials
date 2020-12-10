# IETF 108 NWCRG Meeting Minutes

* [Datatracker](https://datatracker.ietf.org/rg/nwcrg/) 
* [Github](https://github.com/irtf-nwcrg/rg-materials/)


## nwcrg online meeting

Online meeting on Monday Session II 13:00-13:50 (UTC).
[Time Zone Conversion:](https://www.timeanddate.com/worldclock/fixedtime.html?iso=20200727T13&p1=1440&am=50)


#### 00- Welcome, administrative and general matters
(Chairs) (10'+5')

#### 01- Feedback on hackathon 
(Vincent Roca) (5')

Small team and little progress over the week, but at least the source code is now here (encoder and decoder).
It's now essentially a matter of debuging.
We'll have a new hackathon during IETF 109.

### Updates of existing works:    

#### 02- "Coding and congestion control in transport" I-D
(Nicolas Kuhn) (5+5')     
(https://datatracker.ietf.org/doc/draft-irtf-nwcrg-coding-and-congestion/)

- VR: if the I-D remains a "discussion draft" as it is today, without trying to become a "recommendation draft", how far is it from a consolidated version? What amount of work remains to be done?    
- NK: Afraid to open a pandora box since we could add much more content, even as a discussion draft, but is it worth?    
- VR: We need to define the scope depending on the time we have.    
- Anurag (not sure): Usually FEC is part of the physical layer and involves sync between two ends. 1- Is there any kind of synchronisation mechanims either as part of transport or FEC signaling?  2 Usually the packets have some differential delay depending on network fluctuations. Are these aspects being considered?    
- NK: For the moment the two channels [FEC and CC] are considered different in order to be as generic as possible. We do not look at how signaling could be done because it depends on how the mechanismes are being used. I take the point. The synchronisation aspects must be defined or discussed.     
- Spencer Dawkins (SD): thank you for doing this important work. Regarding discussion vs. recommendation. Depends on     
- NK: for the moment we make general statements. Not sure to what extent we can make more specific requirements. To go further in recommendations we need to go further in the protocols in use.    
- SD: My suggestion would be to do two different drafts. Recommendation is for protocol designers. People in IETF often raise such issues. This is anyway an important draft.    
- François Michel (on chat): we could try to recommend to ignore losses when we know we are on a satellite link and losses are not caused by congestion.     
- NK: we agree.    

### Next steps
(Chairs, all) (20')

Summary:
Most of the milestones have been addressed or could be addressed (non finalized docs).
So the chairs would like to:
- adopt as RG-Items most of the remaining I-Ds that are still individual documents;
- publish them as informational RFCs;
- and close the NWCRG group, approximately within 1 year.
The authors of current drafts should be prepared to work on their drafts.
It concerns BATS and Tetrys teams for instance.
Regarding FEC for QUIC, the goal is to publish them within NWCRG, since the IETF QUIC group is well behind schedule and it's not realistic to expect these I-Ds to be moved there any time soon.
And as always: if you want your drafts to be reviewed, be ready to review that of others.

- SD: I've been talking with the LOOPS proponents to be sure they were consistent on their position, looked at the slides, etc. I hope there will be discussion around FEC on Friday LOOPS BOF.    
- MJM: I intend to participate to LOOPS.    
- Colin Perkins: both the Congestion Control and FEC for QUIC documents are pretty close to IETF work, we'll need to discuss on what is most appropriate. I'm happy to see the group has achieved his goals.    
- MJM: the Congestion Control could be pretty a standalone doc, the QUIC work, I agree is close to IETF document. But I'd be very careful not to overwhelm QUIC with Yet Another Document. Anyway we have time to discuss.    

- MJM: we'll see if it make sense to have a short interim before November to make sure documents have made progress.

--    

Total allocated time: 50'



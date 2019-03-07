# IETF 104 SWIF Codec Hackathon

Saturday and Sunday, March 3-4, 2018, starting at 8:30, Grand Ballroom

* [Hackathon wiki](https://trac.ietf.org/trac/ietf/meeting/wiki/104hackathon)    
* [Github swif-codec repo](https://github.com/irtf-nwcrg/swif-codec)    


## Expected participants

* Vincent
* Marie-Jose (Saturday)
* François
* Kazuhisha ???
* Cedric ???
* ???

## General topics to be discussed and agreed on

### Licencing considerations:
* Do all contributors agree to use a BSD licence?
* Do all the authors of existing code reused by the SWIF codec (Cedric/Vincent/...) agree to switch to a BSD licence?

### SWIF Codec project targets:
To be discussed:
* Focus on an RLC codec first (as per [RLC I-D](https://datatracker.ietf.org/doc/draft-ietf-tsvwg-rlc-fec-scheme/)), the RLNC codec will be addressed as a second step (it will share a lot of code anyway.
* Design the SWIF Codec + tiny C language server (encoding side)/client (decoding side) application.
* Add a Python wrapper to the SWIF Codec, then Python test and simulation applications.

### Strategy
* Work on encoder first, with an operational SWIF encoder + server application. Add unitary tests for the encoder.
* Then work on decoder and test the whole chain: server - client. Add unitary tests for the decoder and the whole chain.
* In parallel, work on Python wrapper and python applications.


## Tasks

### SWIF Codec, encoder:
* T1.01: glue between the generic API and RLC codec: the generic API is the one shared by all the SWIF codecs, an RLC flavor is needed as well as a link between the two ones.
* T1.02: work on GF(2^8) math library: reuse gardinet lib, understand how to use it, see if something is missing.
* T1.03: work on encoder_create()
* T1.04: work on encoder_release()
* T1.05: work on encoder_set_callback_functions()
* T1.06: work on swif_encoder_set/get_parameters()
* T1.07: work on swif_build_repair_symbol(): requires to generate the coding coefficients (see RLC I-D) and to computate of the linear combination.
* T1.08: work on encoder_reset_coding_window()
* T1.09: work on encoder_add_source_symbol_to_coding_window()
* T1.10: work on encoder_remove_source_symbol_from_coding_window()
* T1.11: work on encoder_get_coding_window_information()
* T1.12: work on encoder_set_coding_coefs_tab()
* T1.13: work on swif_encoder_generate_coding_coefs()
* T1.14: work on encoder_get_coding_coefs_tab()


### SWIF Codec, decoder:
* T2.01: work on new source or repair symbol reception
* T2.02: linear system decoding using the GF(2^8) math library: includes linear system representation (C structure), progressive decoding upon receiving repair symbols involving erased source symbol(s)
* T2.03: work on decoder_create()
* T2.04: work on decoder_release()
* T2.05: work on set_callback_functions()
* T2.06: work on decoder_set/get_parameters
* T2.07: work on decoder_decode_with_new_source_symbol(): relies on work done on task "linear system decoding"
* T2.08: work on decoder_decode_with_new_repair_symbol(): relies on work done on task "linear system decoding"
* T2.09: work on decoder_reset_coding_window()
* T2.10: work on decoder_add_source_symbol_to_coding_window()
* T2.11: work on decoder_remove_source_symbol_from_coding_window()
* T2.12: work on decoder_set_coding_coefs_tab()
* T2.13: work on decoder_generate_coding_coefs()

### SWIF Codec unitary test:
* T3.1: find a way to add unitary tests.
* T3.2: add as many unitary tests as possible for the encoder.
* T3.3: add as many unitary tests as possible for the decoder.
* T3.4: add as many unitary tests as possible for the server/client transmission.

### C-language server/client application:
* T4.1: work on server (i.e., the encoding/sending side): requires to design a trivial packet format (transmission of the FEC OTI can be static on the opposite), set up the UDP connection, design a simple rate control scheme (to avoid saturating the receiver), and use the generic API to create repair symbols. This work should enable to provide feedback on the Generic API I-D.
* T4.2: work on client (i.e., the decoding/receiving side): set up the UDP connection, use the generic API to manage source/repair symbols, to recover from erased source symbols. Test the whole transmission/reception chain. This work should enable to provide feedback on the Generic API I-D.


### Python wrapper:
* T5.X:


### Python test and simulation applications:
* T6.X:


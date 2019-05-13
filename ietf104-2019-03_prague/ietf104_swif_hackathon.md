# IETF 104 SWIF Codec Hackathon

Saturday and Sunday, March 3-4, 2018, starting at 9:00, Grand Ballroom

* [Hackathon wiki](https://trac.ietf.org/trac/ietf/meeting/wiki/104hackathon)    
* [Github swif-codec repo](https://github.com/irtf-nwcrg/swif-codec)    
* [Final recap presentation](https://github.com/irtf-nwcrg/rg-materials/blob/master/ietf104-2019-03/swif-codec-hackathon-presentation.pdf)


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

## Hackathon participants

* (CA) Cedric Adjih
* (OA) Oumaima Attia
* (FM) François Michel
* (MJM) Marie-Jose Montpetit
* (VR) Vincent Roca

## Tasks

### SWIF Codec, encoder:
* T1.01: (FM) glue between the generic API and RLC codec
* T1.02: (CA) work on GF(2^8) math library: reuse gardinet lib, understand how to use it, see if something is missing.
* T1.03: (OA) work on encoder_create()
* T1.04: (OA) work on encoder_release()
* T1.05: work on encoder_set_callback_functions()
* T1.06: work on swif_encoder_set/get_parameters()
* T1.07: (CA) work on swif_build_repair_symbol(): requires to generate the coding coefficients (see RLC I-D) and to computate of the linear combination.
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
* T4.1 (VR) : work on server (i.e., the encoding/sending side): requires to design a trivial packet format (transmission of the FEC OTI can be static on the opposite), set up the UDP connection, design a simple rate control scheme (to avoid saturating the receiver), and use the generic API to create repair symbols. This work should enable to provide feedback on the Generic API I-D.
* T4.2: work on client (i.e., the decoding/receiving side): set up the UDP connection, use the generic API to manage source/repair symbols, to recover from erased source symbols. Test the whole transmission/reception chain. This work should enable to provide feedback on the Generic API I-D.

### Python wrapper:
* T5.X: (MJM, CA)

### Python test and simulation applications:
* T6.X: (MJM, CA)


## Lessons learned, API I-D fixes and open points @ IETF104 hackathon

I-D/API fixes done:

* clarify that this SWIF-codec is not meant to be thread-safe.
* clarification for buffer init/free in function swif_build_repair_symbol().
* clarification (added examples) for the definition of codepoints
* typo (encoder instead of decoder) in swif_decoder_reset_coding_window (ptr to swif_decoder_t rather than swif_decoder);
* update to the generic control block structure (addition of pointers to the codec specific versions of the API functions).


I-D/API fixes that remain to be done:

* TODO: the esi_t is probably inappropriate. In certain situations, it may be a 64-bit long identifer, in other situations it may be an offet (e.g., see RLC for QUIC).
* TODO: do we really need the encoder_reset_coding_window()? This is clearly useful at the decoder (specify a brand new coding window), but we expect most encoders to manage their encoding window continuously, without needing to reset it altogether. A decision needs to be taken: keep it or remove it.
* TODO: build_repair() cannot be used when the buffer is allocated locally. Error in the API.
* TODO: during the end of session, at an encoder, should we call the callback each time we free a symbol or not? We need to clarify this.
* Added INVALID_ESI to the API. Needed during session startup (first symbol submission). Use another approach to avoid reserving an ESI value to the INVALID state?
* TODO: swif_encoder_get_coding_window_information() is not appropriate when there's non contiguous symbols (e.g., with re-coding use-cases). We need to decide what to do.

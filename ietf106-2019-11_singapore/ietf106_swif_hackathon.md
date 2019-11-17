# IETF 105 SWIF Codec Hackathon

Saturday and Sunday, November 16-17, 2019, starting at 9:00

* [Hackathon wiki](https://trac.ietf.org/trac/ietf/meeting/wiki/105hackathon)    
* [Github swif-codec repo](https://github.com/irtf-nwcrg/swif-codec)    
* Slack discussion forum (ask Vincent)
* [Final recap presentation](https://github.com/irtf-nwcrg/rg-materials/blob/master/ietf105-2019-07/swif-codec-hackathon-presentation.pdf)


## General topics to be discussed and agreed on

N/A

## Hackathon participants

* (CA) Cedric Adjih
* (OA) Oumaima Attia
* (VR) Vincent Roca


## Tasks (including completion status)

* Essentially integration of linear system decoding library (from Cedric A.).
* Continue simple_client.c testing application.

### SWIF Codec, encoder:

### SWIF Codec, decoder:

### SWIF Codec unitary test:
* T3.1: - DONE - find a way to add unitary tests.
* T3.2: - ON PROGRESS - add as many unitary tests as possible for the encoder.
* T3.3: add as many unitary tests as possible for the decoder.
* T3.4: add as many unitary tests as possible for the server/client transmission.

### C-language server/client application:
* T4.1 - DONE - work on server (i.e., the encoding/sending side): requires to design a trivial packet format (transmission of the FEC OTI can be static on the opposite), set up the UDP connection, design a simple rate control scheme (to avoid saturating the receiver), and use the generic API to create repair symbols.
* T4.2: - ALMOST DONE - work on client (i.e., the decoding/receiving side): set up the UDP connection, use the generic API to manage source/repair symbols, to recover from erased source symbols. Test the whole transmission/reception chain.

This work should enable to provide feedback to the Generic API I-D.

### Python wrapper:
* T5.1: - ON PROGRESS - (CA, OA)

### Python test and simulation applications:
* T6.1: (CA, OA)


## I-D/API updates and open problems

### I-D/API fixes done:

* error in decoded_source_symbol_callback) (): does not return anything, so change for void return type.

### Active I-D/API fixes that remain to be done:

* TODO: the esi_t is probably inappropriate. In certain situations, it may be a 64-bit long identifer. Could it be a variable length integer (a la QUIC)?
* TODO: do we really need the encoder_reset_coding_window()? This is clearly useful at the decoder (specify a brand new coding window), but we expect most encoders to manage their encoding window continuously, without needing to reset it altogether. A decision needs to be taken: keep it or remove it.
* TODO: during the end of session, at an encoder, should we call the callback each time we free a symbol or not? We need to clarify this.
* Added INVALID_ESI to the API. Needed during session startup (first symbol submission). Use another approach to avoid reserving an ESI value to the INVALID state?
* TODO: swif_encoder_get_coding_window_information() is not appropriate when there's non contiguous symbols (e.g., with re-coding use-cases). We need to decide what to do.

------

## Decisions taken, API and I-D fixes @ IETF105 hackathon

### Decisions

### I-D/API fixes done:

* build_repair() cannot be used when the buffer is allocated locally. Fixed the error in the API by using a double pointer.

------

## Decisions taken, API and I-D fixes @ IETF104 hackathon

### Decisions

### Licencing considerations:
* decision to use a BSD licence. Yes
* authors of existing code reused by the SWIF codec (Cedric/Vincent/...) agreed to switch to a BSD licence

### SWIF Codec project targets:
* Focus on an RLC codec first (as per [RLC I-D](https://datatracker.ietf.org/doc/draft-ietf-tsvwg-rlc-fec-scheme/)), the RLNC codec will be addressed as a second step (it will share a lot of code anyway).
* Design the SWIF Codec + tiny C language server (encoding side)/client (decoding side) application.
* Add a Python wrapper to the SWIF Codec, then Python test and simulation applications.

### Strategy
* Work on encoder first, with an operational SWIF encoder + server application. Add unitary tests for the encoder.
* Then work on decoder and test the whole chain: server - client. Add unitary tests for the decoder and the whole chain.
* In parallel, work on Python wrapper and python applications.

### I-D/API fixes done:

* clarify that this SWIF-codec is not meant to be thread-safe.
* clarification for buffer init/free in function swif_build_repair_symbol().
* clarification (added examples) for the definition of codepoints
* typo (encoder instead of decoder) in swif_decoder_reset_coding_window (ptr to swif_decoder_t rather than swif_decoder);
* update to the generic control block structure (addition of pointers to the codec specific versions of the API functions).



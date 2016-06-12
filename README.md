# WavAudioEncoder.js

## What is it?

WavAudioEncoder.js is a small JavaScript library that encodes audio data to Waveform Audio (.wav) on web browsers.

### Acknowledgement

Basic idea is taken from Recorderjs (<https://github.com/mattdiamond/Recorderjs>). API has been totally re-designed and simplified. Now it has been a lower layer part of [WebAudioRecorder.js](https://github.com/higuma/web-audio-recorder-js).

## Demo

<https://higuma.github.io/wav-audio-encoder-js/>

## Library files

`lib/` contains library files.

* `WavAudioEncoder.js`: JavaScript library (uncompressed)
* `WavAudioEncoder.min.js`: JavaScript library (minified)

### Using library

You can use it from both HTML and Web Worker.

* from HTML: `<script src="javascripts/WavAudioEncoder.js"></script>`
* from Worker: `importScripts("javascripts/WavAudioEncoder.js");`

## API

``` javascript
encoder = new WavAudioEncoder(sampleRate, numChannels)
```

Create an encoder object.

* Parameters
    * `samleRate`: sampling rate [Hz]
    * `numChannels`: number of audio channels
* Returns
    * encoder object

> In current implementation, bit width is fixed to 16 (2 bytes).

``` javascript
encoder.encode(buffers)
```

Encode audio buffers.

* Parameters
    * `buffers`: array of sample buffers (`[Float32Array, Float32Array ...]`)
* Returns
    * (none)

`buffers` must be an array of Float32Array audio data (range = [-1, 1]). Array length must be same as number of channels. It supports stream (incremental) processing. Sample buffers are processed to .wav fragment and appended to internal data.

``` javascript
blob = encoder.finish([mimeType])
```

Finish encoding and get Waveform Audio as a Blob.

* Parameters
    * `mimeType`(optional): MIME type (default = `"audio/wav"`)
* Returns
    * Blob object

After calling `.finish()`, all internal data is cleared. You must create a new encoder object to encode another audio data.

``` javascript
encoder.cancel()
```

* Parameters
    * (none)
* Returns
    * (none)

Cancel encoding and clear all internal data.

## License

MIT (see [LICENSE.txt](LICENSE.txt)).

import Meyda from 'meyda';

// Create analyzer
const analyzer = Meyda.createMeydaAnalyzer({
  audioContext: audioCtx,
  source: audioSourceNode,   // from MediaElement or MediaStream
  bufferSize: 512,
  featureExtractors: [
    'rms',
    'spectralCentroid',
    'spectralFlatness',
    'zcr',
    'mfcc'
  ],
  callback: (features) => {
    // features.rms
    // features.spectralCentroid
    // features.mfcc → array of 13 numbers
    // etc.
  }
});

analyzer.start();
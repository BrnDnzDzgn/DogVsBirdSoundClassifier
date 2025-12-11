
1) From Waveform to Spectral Shape: FFT (Fast Fourier Transform)
- A raw sound waveform is highly volatile, that is why FFT is essential for this classification task because spectrum provides a stable signature. For this purpose "librosa.stft()" (Short-Time Fourier Transform) is used.

- Time-domain waveforms converted to frequency-domain spectra.

- Spectral centroid (F1) and Spectral Roll-off (F2) are extracted from the magnitude spectrum. These are the stable features that don't change with volume or slight timing differences.

- extract_features_robust() function applies FFT to get spectogram S, then extracts spectral features.


2) Designing a Robust Feature Vector: The Spectral Descriptor
-  The raw frequency spectrum is too large for matching, for this reason we need a small, robust feature vector that is invariant to irrelevant changes like overall volume or amplitude. That is why 2 amplitude-invariant spectral features for bird/dog separation is proposed.

- Spectral Centroid (F1) - Measures where energy is concentrated
- Spectral Roll-off at 85% (F2) - Measures frequency spread

How this works?
- Birds have high centroid (~2000-8000 Hz), high roll-off
- Dogs have low centroid (~500-2000 Hz), low roll-off

3) Classification by Descriptor Matching
- The unknown sound is classified as belonging to the class with the smallest distance. For this purpose Euclidean distance to each class mean are computed.

- Euclidean distance is appropriate for this task because the feature space is low dimensional(2D) and derived from normalized spectral shaped


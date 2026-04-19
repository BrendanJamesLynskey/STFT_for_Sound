# STFT for Sound — Gabor, Allen &amp; Rabiner, Portnoff, the Phase Vocoder

An interactive, animated guide to the Short-Time Fourier Transform as it applies to
audio and music — from Gabor's 1946 time–frequency atoms through the Bell Labs phase
vocoder and Portnoff's filter-bank view, to modern mel-spectrogram neural networks.

**[→ View the Live Guide](https://brendanjameslynskey.github.io/STFT_for_Sound/)**

---

## What's Inside

Ten chapters walk through the history, mathematics, and audio applications of the
Short-Time Fourier Transform, with real-time interactive visualisations and audio
playback throughout.

### 1 · Origins — From Fourier to Gabor
Illustrated timeline: Fourier (1822), Schuster, Nyquist &amp; Shannon, Gabor's 1946
"logons" and uncertainty principle, Cooley &amp; Tukey's FFT, Flanagan &amp; Golden's
phase vocoder (1966), Portnoff's filter-bank formalism, Allen &amp; Rabiner's unified
framework (1977), Crochiere's WOLA, Griffin &amp; Lim, Dolson, Laroche &amp; Dolson,
through to mel-spectrograms and neural vocoders.

### 2 · The STFT — Definition and Intuition
Continuous and discrete formulations. Frame index, hop size, FFT size, bin spacing.
Interactive: slide a window across three different signals and watch the local
spectrum update in real time.

### 3 · Window Functions
The full window library — rectangular, triangular, Hann, Hamming, Blackman,
Blackman-Harris, Gaussian, Kaiser, Flat-top. Interactive comparison of time-domain
shape and frequency-domain magnitude (dB) with main-lobe width and peak sidelobe
level computed from the live FFT.

### 4 · Time–Frequency Resolution — the Uncertainty Principle
Gabor's theorem. Heisenberg-box visualisation that updates as you change window length
and hop. A three-panel spectrogram comparing the same signal at L=128, 512, and 2048
so you can *see* the short/long tradeoff.

### 5 · The Filter-Bank View (Portnoff)
Every STFT bin is a modulated bandpass filter. Interactive bin explorer showing the
impulse response and full bank frequency response as you vary $N$, $k$, and window
type.

### 6 · Perfect Reconstruction and COLA
The Constant-Overlap-Add condition. A live COLA checker — pick any window and hop,
watch whether the shifted sum is flat or rippled — and an STFT round-trip A/B audio
test that reports the reconstruction error in dB.

### 7 · The Phase Vocoder and Modifications
Full derivation of the phase-unwrap and synthesis-phase accumulation equations.
Interactive phase-vocoder time-stretch with adjustable factor and Laroche–Dolson
identity phase-locking toggle. Audio A/B.

### 8 · Spectrogram Inversion — Griffin–Lim
The classic 1984 iterative phase-reconstruction algorithm. Watch it converge across
iterations on a vowel, chord, or bell; error tracked in dB. Audio A/B against the
original.

### 9 · Applications to Sound
A full spectrogram builder for piano, bell, speech, drums, and chirps, with window /
length / overlap controls. Spectral-flux onset detection with live threshold slider.
Spectral subtraction for noise removal (Boll 1979) with α-over-sub and β-floor
controls. A mel-spectrogram view — exactly the frontend modern neural audio models
actually consume.

### 10 · Legacy and Continuing Impact
The STFT's downstream descendants (MDCT in MP3/AAC/Opus), its ubiquity in every DAW,
and its role as the default frontend for contemporary speech and music machine
learning. Full bibliography and cross-links to the companion
[Wavelets for Sound](https://github.com/BrendanJamesLynskey/Wavelets_for_Sound) and
[Constant-Q Transform for Sound](https://github.com/BrendanJamesLynskey/Constant_Q_Transform_for_Sound)
guides.

---

## Technical Details

* **Zero dependencies.** No npm, no bundler, no external libraries. All rendering uses
  the HTML Canvas API. Audio uses the Web Audio API. Math typesetting uses KaTeX
  via jsdelivr — the only third-party asset.
* **All maths computed in real time.** Every STFT, spectrogram, window response,
  COLA sum, COLA round-trip, phase-vocoder stretch, Griffin–Lim iteration, spectral
  flux, spectral subtraction, and mel-bank projection is calculated live in the
  browser with a hand-written radix-2 FFT.
* **Audio playback.** Every signal can be listened to via the Web Audio API —
  synthesised on demand, not pre-recorded.
* **Responsive.** Canvases scale with DPR for sharp rendering on Retina/HiDPI
  displays.
* **Single file.** Everything lives in `index.html`.

### What's computed where

| Visualisation | Algorithm | Notes |
|---|---|---|
| Sliding window + local spectrum | Hann-windowed DFT, 1024-point zero-padded | Draggable |
| Window library comparison | FFT of zero-padded window, log-magnitude | Computes main-lobe width and peak sidelobe |
| Heisenberg boxes | Direct ($\Delta t$, $\Delta f$) geometry | Parameterised by $L$ and $H$ |
| Chirp resolution tradeoff | Three parallel spectrograms at $L=128,512,2048$ | Hann window, $H=L/8$ |
| Filter-bank bin explorer | Impulse and frequency response of bin-$k$ modulated window | Real-valued plot |
| COLA checker | Direct sum of shifted windows | Reports interior ripple in dB |
| COLA round-trip A/B | Full STFT+iSTFT with normalisation | Plots $|x-\hat{x}|$ in dB |
| Phase-vocoder time-stretch | Princarg-based phase update + identity phase-lock | Audio A/B |
| Griffin–Lim | Alternating projection over iterations | Plots SC error vs iteration |
| Spectrogram builder | STFT with user-selected window and overlap | Hann/Hamming/Blackman/Rect |
| Onset detection | Spectral flux + peak-picking | Live threshold |
| Spectral subtraction | Noise-floor estimate + α-over-sub + β-floor | Audio A/B |
| Mel spectrogram | Triangular mel filterbank on STFT magnitude | 32/64/128 bands |
| Audio synthesis | Web Audio API buffer playback | All sounds generated algorithmically |

---

## Key References

1. Gabor, D. (1946). *Theory of Communication.* J. Inst. Electrical Engineers, 93(3), 429–457.
2. Cooley, J. W. &amp; Tukey, J. W. (1965). *An Algorithm for the Machine Calculation of Complex Fourier Series.* Math. Comp., 19(90), 297–301.
3. Flanagan, J. L. &amp; Golden, R. M. (1966). *Phase Vocoder.* Bell System Technical Journal, 45(9), 1493–1509.
4. Portnoff, M. R. (1980). *Time-Frequency Representation of Digital Signals and Systems Based on Short-Time Fourier Analysis.* IEEE Trans. ASSP, 28(1), 55–69.
5. Allen, J. B. &amp; Rabiner, L. R. (1977). *A Unified Approach to Short-Time Fourier Analysis and Synthesis.* Proc. IEEE, 65(11), 1558–1564.
6. Harris, F. J. (1978). *On the Use of Windows for Harmonic Analysis with the Discrete Fourier Transform.* Proc. IEEE, 66(1), 51–83.
7. Griffin, D. W. &amp; Lim, J. S. (1984). *Signal Estimation from Modified Short-Time Fourier Transform.* IEEE Trans. ASSP, 32(2), 236–243.
8. Dolson, M. (1986). *The Phase Vocoder: A Tutorial.* Computer Music Journal, 10(4), 14–27.
9. Laroche, J. &amp; Dolson, M. (1999). *Improved Phase Vocoder Time-Scale Modification of Audio.* IEEE Trans. SAP, 7(3), 323–332.
10. Boll, S. F. (1979). *Suppression of Acoustic Noise in Speech Using Spectral Subtraction.* IEEE Trans. ASSP, 27(2), 113–120.
11. McFee, B. et al. (2015). *librosa: Audio and Music Signal Analysis in Python.* Proc. SciPy 2015.

---

## Related Guides

* [Wavelets for Sound](https://github.com/BrendanJamesLynskey/Wavelets_for_Sound) — Kronland-Martinet, Grossmann &amp; Morlet — adaptive time–frequency resolution.
* [Constant-Q Transform for Sound](https://github.com/BrendanJamesLynskey/Constant_Q_Transform_for_Sound) — Brown &amp; Puckette's log-frequency spectrum.

---

## License

MIT — use it however you like. Attribution appreciated but not required.

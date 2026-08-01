# Fourier Transform Explained

The **Fourier Transform (FT)** is a mathematical tool that converts a signal from the **time domain** into the **frequency domain**.

In simple words, it tells us **what frequencies are present in a signal and how strong each frequency is**.

---



# Simple Analogy

Imagine you're listening to an **orchestra**.

When all the instruments play together, you hear one combined sound.

The **Fourier Transform** acts like a magical machine that separates the sound into:

- 🎻 Violin
- 🥁 Drums
- 🎺 Trumpet
- 🎹 Piano
- 🎸 Guitar

It tells you how much each instrument (frequency) contributes to the final sound.

---

# Example 1: Single Frequency

Suppose the signal is

$$
x(t) = \sin(2\pi \times 5t)
$$

This is a **5 Hz sine wave**.

### Time Domain

```
   / \      / \      / \
--/---\----/---\----/---\----
```

### Fourier Transform Output

```
Amplitude
   |
   |         *
   |         |
___|_________|______________ Frequency
           5 Hz
```

The Fourier Transform tells us:

> The signal contains only one frequency: **5 Hz**.

---

# Example 2: Multiple Frequencies

Suppose

$$
x(t)=\sin(2\pi\times5t)+0.5\sin(2\pi\times20t)
$$

Now the signal contains:

- 5 Hz
- 20 Hz

The Fourier Transform becomes

```
Amplitude
   |
1.0|      *
   |      |
0.5|                  *
   |                  |
___|______|___________|____________ Frequency
       5 Hz        20 Hz
```

This tells us:

- Strong 5 Hz frequency
- Smaller 20 Hz frequency

---

# Mathematical Formula

The Fourier Transform is defined as

$$
X(f)=\int_{-\infty}^{\infty}x(t)e^{-j2\pi ft}\,dt
$$

Where

- **x(t)** = Original signal
- **X(f)** = Frequency representation
- **f** = Frequency (Hz)
- **j** = √−1 (imaginary unit)

The term

$$
e^{-j2\pi ft}
$$

is a complex sine wave.

The Fourier Transform checks **how much of each frequency exists in the signal**.

---

# Inverse Fourier Transform

The original signal can be recovered using

$$
x(t)=\int_{-\infty}^{\infty}X(f)e^{j2\pi ft}\,df
$$

So,

- Fourier Transform → Time Domain ➜ Frequency Domain
- Inverse Fourier Transform → Frequency Domain ➜ Time Domain

---

# Why Sine and Cosine Waves?

Almost every real-world signal can be represented as a combination of many sine and cosine waves.

Each wave has:

- Frequency
- Amplitude
- Phase

The Fourier Transform finds these components.

---

# Why is Fourier Transform Useful?

Many real-world signals are mixtures of different frequencies.

Examples include:

- 🎵 Music
- 🎤 Speech
- 📡 Radio Signals
- 🌍 Earthquakes
- 🖼️ Images
- ❤️ ECG Signals
- 🧠 EEG Signals

The Fourier Transform helps us analyze these signals.

---

# Applications

The Fourier Transform is widely used in many fields.

### Audio Processing

- Noise removal
- Equalizers
- MP3 compression

### Image Processing

- JPEG compression
- Image filtering
- Edge detection

### Communication Systems

- Wi-Fi
- Bluetooth
- 4G / 5G
- Radio
- Television

### Medical Imaging

- MRI
- CT Scan
- Ultrasound

### Machine Learning

- Feature extraction
- Speech recognition
- Signal processing

### Engineering

- Vibration analysis
- Fault detection
- System analysis

---

In short,

> **Fourier Transform converts a signal from the time domain into the frequency domain, making it easier to analyze the frequencies that make up the signal.**

---

# Short-Time Fourier Transform (STFT) for Speech Recognition

## What is STFT?

**STFT (Short-Time Fourier Transform)** is a technique used to convert a speech signal into a form that a computer can understand more easily.

Instead of analyzing the **entire audio signal at once**, STFT analyzes **small pieces of audio one by one**. This allows us to see **how the frequencies change over time**, which is essential for speech recognition.

---

# Why Can't We Use a Normal Fourier Transform?

Imagine someone says:

> **"Hello"**

The sound changes continuously:

* Beginning → **"He"**
* Middle → **"ll"**
* End → **"o"**

A normal **Fourier Transform** analyzes the **entire audio signal** and tells us:

> "These frequencies exist."

However, it **does not tell us when** those frequencies occurred.

For speech recognition, **timing is very important** because every word changes over time.

---

# The Idea Behind STFT

Think of reading a book.

Instead of reading the entire book at once, you read **one page at a time**.

STFT works the same way.

```text
Whole Audio

|---------------------------------------------|

Split into Small Windows

|----|----|----|----|----|----|----|
```

Each window is usually **20–40 milliseconds** long.

---

# Step-by-Step Process

## Step 1: Input Speech

Suppose the user says:

```text
Hello
```

The microphone records it as a waveform.

```text
Amplitude

 ^
 |        /\      /\      /\
 |       /  \    /  \    /  \
 |______/____\__/____\__/____\____ Time
```

---

## Step 2: Divide the Audio into Small Windows

Instead of analyzing the entire waveform, STFT divides it into many overlapping frames.

```text
Window 1
|------|

Window 2
      |------|

Window 3
            |------|
```

### Why do the windows overlap?

Speech changes smoothly over time.

If there were no overlap, important information between two windows could be lost.

Typical values:

* **Window Size:** 25 ms
* **Hop Length:** 10 ms

```text
Frame 1
|-------------------------|

Frame 2
          |-------------------------|

Frame 3
                    |-------------------------|
```

---

## Step 3: Apply a Window Function

Before applying the Fourier Transform, each frame is multiplied by a **window function** (usually a **Hamming Window**).

Without a window:

```text
|████████████|
```

Sharp edges introduce unwanted frequency artifacts.

With a Hamming window:

```text
      /\
    /    \
  /        \
```

The edges become smooth, reducing **spectral leakage**.

---

## Step 4: Apply Fourier Transform

Now each small window is converted from the **time domain** into the **frequency domain**.

Example:

### Window 1

```text
Sound:
He
```

Fourier Transform:

```text
200 Hz
500 Hz
900 Hz
```

### Window 2

```text
ll
```

Result:

```text
250 Hz
700 Hz
1200 Hz
```

### Window 3

```text
o
```

Result:

```text
300 Hz
800 Hz
1400 Hz
```

Now we know **which frequencies were present during each small time interval**.

---

## Step 5: Combine All Windows

Instead of producing one frequency graph, STFT produces one graph for **every window**.

```text
Time →

Frame1   Frame2   Frame3   Frame4

Freq
 ^
 |
 | ####      ###      ##
 | ######    #####    ####
 | ###       ###      #####
 +---------------------------->
```

This final representation is called a **Spectrogram**.

---

# What is a Spectrogram?

A **spectrogram** is the output of STFT.

It is essentially an image showing how frequencies change over time.

```text
Frequency
^

4000 |       ██
3000 |     ████
2000 | ████████
1000 |██████████
      ------------------------> Time
```

### Axes

* **X-axis:** Time
* **Y-axis:** Frequency
* **Color/Brightness:** Energy (strength) of each frequency

This is why many speech recognition systems treat speech as an **image**.

---

# Why is STFT Useful for Speech Recognition?

Speech changes continuously.

```text
H   E   L   L   O
```

Each letter contains different frequency patterns.

STFT captures these frequency changes over time.

Instead of knowing only:

```text
Frequency
```

STFT gives us:

```text
Time + Frequency
```

This makes it much easier for machine learning models to recognize spoken words.

---

# Speech Recognition Pipeline

```text
Microphone
      │
      ▼
Audio Waveform
      │
      ▼
Split into Frames
      │
      ▼
Apply Hamming Window
      │
      ▼
STFT
      │
      ▼
Spectrogram
      │
      ▼
Mel Filter Banks
      │
      ▼
Log-Mel Spectrogram
      │
      ▼
Neural Network
(RNN / LSTM / GRU / CNN / Transformer)
      │
      ▼
Predicted Text
```

---

# Example

Suppose someone says:

```text
"Cat"
```

The waveform may look like:

```text
/\/\/\/\/\/\/\/\/\/\/\/\
```

After STFT:

| Time     | Dominant Frequencies |
| -------- | -------------------- |
| 0–25 ms  | 300 Hz, 900 Hz       |
| 10–35 ms | 350 Hz, 1100 Hz      |
| 20–45 ms | 500 Hz, 1500 Hz      |
| 30–55 ms | 700 Hz, 2200 Hz      |

The speech recognition model now understands **how the frequencies changed over time**, making it easier to identify the spoken word.

---


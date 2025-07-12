---

## 1. Recurrent Neural Networks (RNN):

### **What is RNN?**

* RNN is a type of neural network designed specifically to process sequences of data, like sentences, time-series data, audio, etc.
* The output from a previous step is fed into the current step, giving the network a form of memory.

### **How it works:**

* Each step shares the same weights and biases.
* It has a hidden state (`h`) to store previous information.

### **Mathematical Representation:**

$$
h_t = \text{tanh}(W_{hh}h_{t-1} + W_{xh}x_t + b_h)
$$

$$
y_t = W_{hy}h_t + b_y
$$

### **Simplified Diagram:**

```
Input(x₁) ──────→ RNN ────→ Output(y₁)
                   │
                   │
                 h₁(state)
                   │
                   ↓
Input(x₂) ──────→ RNN ────→ Output(y₂)
                   │
                   │
                 h₂(state)
                   │
                   ↓
Input(x₃) ──────→ RNN ────→ Output(y₃)
                   │
                   │
                  ...
```

---

## 🔴 **Problem with RNN (Vanishing Gradient):**

* RNNs struggle to learn from very long sequences due to the **vanishing gradient problem** (gradients becoming too small) or sometimes the exploding gradien(too large).

---

## 2. Long Short-Term Memory (LSTM):

### **What is LSTM?**

* A special type of RNN designed to handle long-term dependencies and mitigate vanishing gradient problems.
* It introduces gating mechanisms (`input gate`, `forget gate`, and `output gate`) to control information flow.

### **Structure:**

* **Forget Gate** (`fₜ`): Decides what information to discard.
* **Input Gate** (`iₜ`): Decides what new information to store.
* **Output Gate** (`oₜ`): Decides what output to generate.

### **Mathematical Representation:**

* **Forget Gate**:

$$
f_t = \sigma(W_f[h_{t-1}, x_t] + b_f)
$$

* **Input Gate**:

$$
i_t = \sigma(W_i[h_{t-1}, x_t] + b_i)
$$

* **Candidate memory cell**:

$$
\tilde{C}_t = \text{tanh}(W_C[h_{t-1}, x_t] + b_C)
$$

* **Cell State update**:

$$
C_t = f_t \odot C_{t-1} + i_t \odot \tilde{C}_t
$$

* **Output Gate**:

$$
o_t = \sigma(W_o[h_{t-1}, x_t] + b_o)
$$

* **Hidden State update**:

$$
h_t = o_t \odot \text{tanh}(C_t)
$$

### **Simplified Diagram:**

```
   Previous Cell State (Cₜ₋₁)
            │
            │
            ↓
(xₜ,hₜ₋₁)───→[Forget Gate]───→×─────┐
            │                       │
(xₜ,hₜ₋₁)───→[Input Gate]───→×───→(+)───→ Cₜ (Updated Cell State)
            │                │      │
            └───→[tanh]──────┘      │
                                    │
(xₜ,hₜ₋₁)───→[Output Gate]──────────┤
                                    ↓
                                 Output (hₜ)
```

---

## 3. Gated Recurrent Unit (GRU):

### **What is GRU?**

* A simpler variant of LSTM, with fewer gates, thus computationally more efficient.
* It combines the forget and input gates into a single **update gate** (`zₜ`) and has a **reset gate** (`rₜ`).

### **Structure:**

* **Update Gate (`zₜ`)**: Determines how much of past information to carry forward.
* **Reset Gate (`rₜ`)**: Controls how much of the past information to forget.

### **Mathematical Representation:**

* **Update Gate**:

$$
z_t = \sigma(W_z[h_{t-1}, x_t] + b_z)
$$

* **Reset Gate**:

$$
r_t = \sigma(W_r[h_{t-1}, x_t] + b_r)
$$

* **Candidate Hidden State**:

$$
\tilde{h}_t = \text{tanh}(W[r_t \odot h_{t-1}, x_t] + b)
$$

* **Hidden State update**:

$$
h_t = (1 - z_t) \odot h_{t-1} + z_t \odot \tilde{h}_t
$$

### **Simplified Diagram:**

```
hₜ₋₁ ────→[Reset Gate]───→×────→[tanh]───┐
 │                        ↑              │
 │                        │              │
 └─────→[Update Gate]─────┴─────────→(1 - zₜ)
                          │              │
                          ↓              │
                       (zₜ)──────────────(+)
                          │
xₜ────────────────────────┘
                          │
                          ↓
                        hₜ (New State)
```

---

## ⚡ **Comparison of RNN, LSTM, and GRU:**

| Factor                  | RNN      | LSTM                  | GRU              |
| ----------------------- | -------- | --------------------- | ---------------- |
| Gates                   | No gates | Input, forget, output | Update, reset    |
| Complexity              | Simple   | Complex               | Moderate         |
| Training Speed          | Faster   | Slower                | Faster than LSTM |
| Long-term dependency    | Poor     | Excellent             | Good             |
| Computational Resources | Low      | High                  | Moderate         |

---

## 🎯 **Summary of Usage:**

* **RNN**: Basic sequence learning, short sequences.
* **LSTM**: Effective for longer sequences and complex tasks, like language modeling and machine translation.
* **GRU**: Similar tasks as LSTM but faster and simpler, good balance between complexity and performance.

---
Here are clear, simple, and relatable **real-world examples** illustrated through diagrams for **RNN, LSTM, and GRU**, along with the generated examples:
---

## 🔷 **1. Recurrent Neural Network (RNN):**

### 🎯 **Real-world Example: Text Auto-completion**

* **Scenario:** Predict the next word when typing a message.
* **Example sentence:** "I am going to the \_\_\_".

### **Diagram:**

```
(User typing)         ┌───────┐        ┌───────┐       ┌───────┐      ┌─────────┐
 "I am going to" ────▶│  RNN  │───────▶│  RNN  │─────▶│  RNN  │────▶│ Predict │
                      └───────┘        └───────┘       └───────┘      └─────────┘
                          │                │               │               │
                        "the"            "park"         "movie"          "mall"
```

* **Generated Example:**

  ```
  Input: "I am going to the"
  Predicted output: "park"
  ```

---

## 🔷 **2. Long Short-Term Memory (LSTM):**

### 🎯 **Real-world Example: Sentiment Analysis on Reviews**

* **Scenario:** Understanding if a movie review is positive or negative.
* **Example Review:** "The movie was interesting at first, but later became boring."

### **Diagram:**

```
 Review Text ────────────────────────────────────────────┐
                                                         │
 ┌──────────┐    ┌──────────┐   ┌──────────┐  ┌──────────┐
 │  LSTM    │───▶│  LSTM    │──▶│  LSTM    │─▶│ LSTM     │
 └──────────┘    └──────────┘   └──────────┘  └──────────┘
      │               │              │             │
    "The"          "interesting"   "later"     "boring"
      │               │              │             │
      └───────────────┴──────────────┴─────────────┘
                           │
                 ┌───────────────────┐
                 │Sentiment Analysis │
                 └───────────────────┘
                           │
                  ┌────────┴────────┐
               Negative          Positive
```

* **Generated Example:**

  ```
  Input Review: "The movie was interesting at first, but later became boring."
  Predicted Sentiment: Negative
  ```

---

## 🔷 **3. Gated Recurrent Unit (GRU):**

### 🎯 **Real-world Example: Stock Price Prediction**

* **Scenario:** Predicting the next day's stock price based on past data.
* **Example:** Stock prices of XYZ Corp for three days.

### **Diagram:**

```
 Past Stock Prices ────────────────────────────────────────┐
                                                           │
 ┌───────────┐    ┌───────────┐     ┌───────────┐   ┌───────────────┐
 │   GRU     │───▶│   GRU     │───▶ │   GRU     │─▶ │ Prediction    │
 └───────────┘    └───────────┘     └───────────┘   └───────────────┘
      │                │                 │                  │
   "Day 1"          "Day 2"           "Day 3"        "Next Day Price"
      │                │                 │                  │
    $120              $123              $125               $127 ?
```

* **Generated Example:**

  ```
  Input Prices: [$120, $123, $125]
  Predicted Next Day Price: $127
  ```

---

## ⚡ **Comparison (Why use each one?):**

| Model | Example Application                       | Why use?                           |
| ----- | ----------------------------------------- | ---------------------------------- |
| RNN   | Text auto-completion                      | Simple, fast, short sequences      |
| LSTM  | Sentiment analysis, language translation  | Captures long-term context, memory |
| GRU   | Stock price prediction, forecasting tasks | Less complex than LSTM, efficient  |

---



# ⚡ AI-Based Power Dissipation Prediction and Optimization in VLSI Design

An AI-powered system to predict power dissipation in digital circuits at an early design stage—without running expensive EDA simulations.



## 🚀 Overview

Power estimation is a critical challenge in VLSI design. Traditional methods rely on tools like Synopsys or Cadence, which are slow and applied late in the design flow.

This project uses Machine Learning to predict power dissipation from design parameters early in the process, enabling faster decisions and optimization.



## 📊 Dataset

* Source: CircuitNet-N28 (28nm technology node)
* 10,242 samples from RISC-V CPU designs
* Each sample includes:

  * Clock frequency
  * Utilization
  * Macro count
  * PDN layers
  * Placement strategy
  * IR drop map (used as power proxy)



## 🤖 Model

* Random Forest Regressor (Primary Model)
* R² Score: ~0.70
* Predicts IR drop (proxy for power dissipation)



## 🖥️ Features

* Predict power dissipation from design parameters
* Identify power-hungry modules
* Visualize module-wise power distribution
* Get module-specific optimization suggestions
* Batch prediction using CSV upload



## 🧩 User Interface

### Input Modes

1. **Manual Input**

   * Enter circuit parameters directly
   * Instant prediction

2. **CSV Upload**

   * Upload multiple designs for batch prediction

### CSV Validation

* Detects missing/incorrect columns
* Shows clear error messages
* Suggests how to fix the file
* Provides downloadable CSV template
* Option to switch to manual input

### Output

* Power level (Low / Moderate / High)
* IR drop value
* Module-level power charts
* Optimization recommendations

### Report

* Download results as a **PDF report**



## 🛠️ How to Use

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/power-prediction-vlsi.git
cd power-prediction-vlsi
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

### 3. Run the Application

```bash
python app.py
```

### 4. Open in Browser

Go to:

```
http://localhost:5000
```

### 5. Use the System

* Choose **Manual Input** or **CSV Upload**
* Enter/upload parameters
* Click **Predict**
* View results and download report



## 📈 Key Insight

Power is strongly dependent on frequency:

P = αCV²f

Higher frequency ⇒ higher power consumption



## ⚠️ Limitations

* Uses IR drop as proxy (not direct power data)
* Limited to 28nm dataset



## 📚 Reference

* CircuitNet Dataset: [https://github.com/circuitnet/CircuitNet](https://github.com/circuitnet/CircuitNet)



## Website link:
https://circuitmindai.netlify.app/ 

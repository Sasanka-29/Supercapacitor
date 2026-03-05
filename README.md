# Supercapacitor Bank

**Sasanka Barman**  
**March 3, 2026**

## 1. Introduction

This document explores the possibility of using the **HSH1630-3R8457-R** supercapacitor bank with the **Shock360** module.

<!-- ![Figure 1: Block Diagram]("\image.png") -->

![Block Diagram](blockdiagram.png)

## 2. Requirements

### 2.1 Shock360 Module Power Supply (195 uF / 360 J)

- **Supply Voltage**: 21 V
- **Peak Current**: 5.6 A @ 3.6 s
- **Power Consumption**: 2 W

## 3. HSH1630-3R8457-R Hybrid Supercapacitor Specs

- Capacitance: **450 F**
- Maximum Rated Voltage: **3.8 V**
- Minimum Rated Voltage: **2.5 V**
- Maximum Discharge Current: **15 A**
- Maximum DC ESR: **0.06 Ω**

## 4. Bank Configuration: 7S1P

- Capacitors in Series: **7**
- Capacitors in Parallel: **1**

### 4.1 Bank Specs

- **Capacitance**: 450 ÷ 7 = **64.3 F**
- **Maximum Rated Voltage**: 3.8 × 7 = **26.6 V**
- **Minimum Rated Voltage**: 2.5 × 7 = **17.5 V**
- **Maximum DC ESR**: 7 × 0.06 = **0.42 Ω**

## 5. Energy Required per Shock

$$
E = \frac{1}{2} \times \left( \frac{C \times M_\text{parallel}}{N_\text{series}} \right) \times (V_\text{final}^2 - V_\text{initial}^2)
$$

- Energy stored = **0.5 × 64.3 × (26.6² − 17.5²) = 12,902.1 J**
- Total time (Charging 3.6 s + Operation): **15 s**
- DC-DC Converter Efficiency: **90 %**
- Energy required by module = **21 V × 5.6 A × 3.6 s + (15 − 3.6) s × 2 W = 446.1 J**
- Energy drained from capacitor = **446.1 ÷ 0.9 = 495.6 J**

## 6. Super Capacitor Voltage Calculations

### 6.1 DC-DC Buck-Boost Converter Specs (LTM8055)

- Minimum Input Voltage: **5.0 V**
- Boost Efficiency: **90 %**
- Output: **21 V / 5.6 A**
- Input Voltage (nominal): **22 V**
- Input Current: **(21 × 5.6) ÷ (22 × 0.9) = 5.9 A**

### 6.2 Minimum Super Capacitor Voltage

- Max voltage droop = 7.5 A × (0.42 Ω × 3) = **9.45 V**
- Minimum SC voltage = (5.0 + 9.45) + 50 % safety = **21.67 V**

### 6.3 Maximum Super Capacitor Voltage

$$
V_\text{max} = \sqrt{\frac{2 \times 495.6}{64.3}} + 21.67 = \mathbf{22.02\,V}
$$

## 7. Super Capacitor Charging Time

- Max charging current: **15 A**
- Min charging time = (64.3 × 21.95) ÷ 15 ≈ **94.1 s ≈ 1.56 min**
- Total operation cycle = 15 s + 92.8 s = **109.1 s ≈ 1.81 min**

## 8. Handcrank Timing

- Handcrank power ≈ **20 W**
- Handcrank voltage ≈ **28 V**
- Handcrank current ≈ **0.71 A**

**Time to reach minimum voltage (21.67 V) for 1 shock**  
→ **(64.3 × 21.67) ÷ 0.71 ≈ 1962.5 s**

**Full charge (0 → 26.6 V)** → **2408.9 s**

**Time for next shock (from 21.67 V)** → **495.6 J ÷ 20 W = 24.78 s**

## 9. Miscellaneous Calculations

### 9.1 Power & Energy Loss

- Power loss = **I²R = 5.92² × 0.42 = 12.24 W**
- Energy loss = **12.24 W × 3.6 s = 44.08 J**

### 9.2 Discharge Timeline (5.9 A load)

1. t = 0 s → Bank voltage = **26.6 V**
2. t = 0.001 s → Instant ESR droop = 5.9 × 0.42 = **2.47 V** → Output drops to **24.13 V**
3. t = 0.001–3.6 s → ΔV = 21.34 ÷ 64.3 = **0.33 V**
4. t = 3.6 s → Voltage = **23.8 V**
5. t = 3.601 s (load removed) → Voltage recovers to **26.27 V**

### 9.3 Leakage Calculation

Leakage current ≈ **70 µA**

| Days | Voltage Drop | Remaining Voltage |
| ---- | ------------ | ----------------- |
| 30   | 2.8 V        | 18.84 V           |
| 45   | 4.23 V       | 17.43 V           |

**Recommendation**: Charge the bank once every **4 weeks** up to **25.2 V** (3.6 V per capacitor) to keep it healthy and ready.

---

# **End of document**

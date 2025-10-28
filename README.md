📊 Hotel Booking Cancellation Insights — Data Analysis & Business Recommendations

Goal:
Analyze hotel booking behavior & identify key drivers of reservation cancellations to help hotels reduce revenue loss and improve booking strategy.

Tools Used: Python, Pandas, Seaborn, Matplotlib
Modeling Approach: Logistic regression (binary classification)
Business Focus: Revenue management & cancellation prevention

### 🔍 Key Questions
- What % of bookings get canceled?
- Does booking early increase cancellation risk?
- Does room price impact cancellations?
- Which booking channels cancel more?
- Do deposits and loyalty matter?

---

## 📊 Key Insights

### ✅ Key Insight #1: Overall Cancellation Rate ~27.7%
![Cancellation Rate](images/cancellation_rate.png)

Nearly **1 in 3 bookings are canceled**, creating major forecasting challenges.

---

### ✅ Key Insight #2: Longer Lead Time = Higher Cancellation
![Lead Time Boxplot](images/lead_time_boxplot.png)

Guests who book **far in advance** are more likely to cancel later.

---

### ✅ Key Insight #3: Higher Price Bookings Cancel More
![ADR Boxplot](images/adr_boxplot.png)

Price-sensitive customers cancel more — dynamic pricing strategy recommended.

---

### ✅ Key Insight #4: Channel Matters (OTA & Groups cancel more)
![Market Segment Cancellation](images/market_segment_cancellation.png)

| Segment | Cancellation Rate |
|---|---|
Groups | ~43% ❗  
Online TA | ~35% ⬆️  
Direct / Corporate | ~13-15% ✅  

---

### ✅ Key Insight #5: Deposit Policy Influences Cancellation
![Deposit Type Cancellation](images/deposit_type_cancellation.png)

| Deposit Type | Cancellation Rate |
|---|---|
No Deposit | ~25%  
Refundable | ~16%  
Non Refund | **~96%** 🤯  

---

### ✅ Key Insight #6: Repeat Guests Rarely Cancel
![Repeat Guest Cancellation](images/repeat_guest_cancellation.png)

Repeat guests cancel **~6% vs ~29%** for new guests → loyalty matters!

---

## 💡 Business Recommendations

| Strategy | Purpose |
|---|---|
Require deposit/pre-auth for OTA / groups | Reduce speculative bookings |
Prioritize loyalty guests | Stable revenue + lower cancellation |
Monitor far-future reservations | Reduce peak-date overbooking risk |
Dynamic pricing rules | Reduce price-driven cancellations |
Risk flag model | Prioritize follow-ups |

---

## 🧠 Tech Stack
- Python  
- Pandas, NumPy  
- Matplotlib, Seaborn  
- Jupyter Notebook

---

## 📁 Project Structure

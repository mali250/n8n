# 📦 Telegram Receipt Extractor — Tesseract + Llama (AI Powered)

This workflow allows users to send receipt images or plain text via Telegram.  
The bot automatically extracts receipt details, detects expenses, and sends back a clean, organized summary.

---

## 🚀 Features

### ✔️ Smart Input Detection  
- Detects if the user sent **image** or **text**  
- Routes the workflow accordingly  

### ✔️ OCR Using Tesseract  
- Extracts text from receipt images  
- Handles messy, wrinkled, or low-light receipts  

### ✔️ AI-Powered Receipt Understanding  
Uses **Llama via OpenRouter** to automatically understand:  
- Store name  
- Store location  
- Date & time  
- Items list with quantity, price, and totals  
- Payment method  
- Expense category  
- Grand total  

### ✔️ Clean Summary Message  
Outputs a beautifully formatted Telegram message summarizing all captured receipt details.

### ✔️ Error Handling  
- Detects missing or zero totals  
- Sends helpful error notifications  
- Prevents sending invalid expense summaries

---

## 🧠 Workflow Logic

1. **Telegram Trigger**  
   Receives messages from the user.

2. **Check for Image**  
   If the message contains a photo → OCR flow  
   If text → NLP flow.

3. **Download Image**  
   Fetches and downloads the photo file from Telegram.

4. **Tesseract OCR**  
   Extracts plain text from the image.

5. **AI Categorizer (Llama)**  
   Understands natural language receipts.  
   Categorizes and structures the data.

6. **Receipt Parser**  
   Converts AI output into strict JSON:  
   - store  
   - transaction  
   - items  
   - summary  

7. **Format Summary Message**  
   Creates a user-friendly Telegram message.

8. **Check Invalid Input**  
   Ensures total amount isn’t missing or zero.

9. **Send Summary / Error**  
   Returns results to the user.


## ⚙️ Technologies Used

- **n8n**
- **Telegram Bot API**
- **Tesseract.js OCR**
- **Llama (OpenRouter)**
- **JavaScript (Code node)**
- **JSON structured parsing**

---

## 🔧 Requirements

- Telegram Bot Token  
- OpenRouter API Key  
- n8n instance  
- Tesseract node installed  

---

## 👤 Author / Credits  
This workflow is adapted and enhanced for custom use by **Muazzam Ali**.  
Original creator attribution remains intact.

Need a customized version? DM me anytime 👍


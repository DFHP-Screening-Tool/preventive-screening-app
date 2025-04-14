# CAF Preventive Screening App

This is a web-based preventive screening tool designed for Canadian Armed Forces (CAF) healthcare providers. It helps determine appropriate preventive health screenings for asymptomatic, average-risk adults based on age and gender. The tool aligns with the most recent Canadian Task Force on Preventive Health Care (CTFPHC) and national specialty society guidelines as of April 2025.

## 🚀 Features

- Easy-to-use interface for inputting age and gender
- Dynamically generates tailored screening recommendations
- Categorized output: Universal, Female-Specific, Male-Specific
- Includes:
  - Strength of recommendation (✔, ➕, ➖, ✖, 🩺)
  - Screening test name
  - Suggested frequency
  - Link to guideline source

## 📊 Source

Recommendations are derived from:
- Canadian Task Force on Preventive Health Care (CTFPHC)
- Diabetes Canada
- Hypertension Canada
- Canadian Cardiovascular Society
- Canadian Urological Association
- Osteoporosis Canada

Compiled in: **"Updated Preventive Medicine Recommendations for the CAF – April 7, 2025"**

## 🧠 Symbols Legend

| Symbol | Meaning                             |
|--------|-------------------------------------|
| ✔      | Strong recommendation               |
| ➕      | Weak recommendation                 |
| ➖      | Weak recommendation against         |
| ✖      | Strong recommendation against       |
| 🩺      | Eligible for screening, discuss     |

## 🖥️ How to Use

1. Visit the [CAF Screening Tool](https://dfhp-screening-tool.github.io/preventive-screening-app/)
2. Enter patient’s **age** and **gender**
3. Click **"Get Recommendations"**
4. Review personalized screening guidance sorted by category

## 📁 Project Structure

```
preventive-screening-app/
├── index.html         # Main application logic & UI
├── pic-for-app.png    # Illustration (optional)
├── README.md          # Project documentation
```

## 📌 To Do

- Add support for high-risk population modifiers
- Improve mobile responsiveness
- Local storage or export of results
- French version (bilingual support)

## 🤝 Contributing

Suggestions and pull requests are welcome. Please ensure your updates align with evidence-based CAF guidelines.

## 📜 License

This tool is open source and free to use under the MIT License.

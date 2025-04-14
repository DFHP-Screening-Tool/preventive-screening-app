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
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>CAF Preventive Medicine</title>
  <link href="https://fonts.googleapis.com/css?family=Roboto:400,500,700&display=swap" rel="stylesheet">
  <style>
    body {
      font-family: 'Roboto', sans-serif;
      margin: 0;
      padding: 0;
      background-color: #f4f4f4;
      color: #333;
      line-height: 1.6;
    }
    header {
      background-color: #003366;
      padding: 15px 20px;
      text-align: center;
      color: white;
    }
    .container {
      max-width: 800px;
      margin: 30px auto;
      padding: 0 20px;
    }
    h1, h2 {
      color: #003366;
      text-align: center;
    }
    p.intro {
      text-align: center;
      font-size: 1.1rem;
      margin-bottom: 30px;
    }
    .my-image {
      display: block;
      margin: 20px auto;
      max-width: 100%;
      height: auto;
      border-radius: 8px;
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
    }
    form {
      background: #ffffff;
      padding: 20px;
      border-radius: 8px;
      box-shadow: 0 2px 6px rgba(0, 0, 0, 0.15);
      max-width: 400px;
      margin: 0 auto 30px;
    }
    form label, form input, form select, form button {
      display: block;
      width: 100%;
      margin-top: 15px;
      font-size: 1rem;
    }
    form input, form select {
      padding: 10px;
      border: 1px solid #ccc;
      border-radius: 4px;
    }
    form button {
      background-color: #005fa3;
      color: #ffffff;
      border: none;
      padding: 12px;
      border-radius: 4px;
      cursor: pointer;
      transition: background-color 0.3s ease;
    }
    form button:hover {
      background-color: #004c87;
    }
    #results {
      background: #ffffff;
      padding: 20px;
      border-radius: 8px;
      box-shadow: 0 2px 6px rgba(0, 0, 0, 0.15);
      max-width: 700px;
      margin: 0 auto 30px;
    }
    #results section {
      margin-bottom: 30px;
    }
    #results h3 {
      color: #005fa3;
      margin-bottom: 15px;
    }
    #results ul {
      list-style-type: none;
      padding: 0;
    }
    #results li {
      padding: 15px;
      border-bottom: 1px solid #e6e6e6;
    }
    #results li:last-child {
      border-bottom: none;
    }
    #results a {
      color: #005fa3;
    }
    #results a:hover {
      color: #003366;
      text-decoration: underline;
    }
  </style>
</head>
<body>
  <header>
    <h1>CAF Preventive Medicine</h1>
  </header>

  <div class="container">
    <img src="pic-for-app.png" alt="App Preview" class="my-image" />

    <p class="intro">
      This tool suggests evidence-based preventive screening recommendations for healthy adults. Enter the patient's age and gender to get tailored guidelines, including test types and screening intervals.
    </p>

    <form id="screeningForm">
      <label for="age">Patient Age:</label>
      <input type="number" id="age" name="age" min="18" required>

      <label for="gender">Patient Gender:</label>
      <select id="gender" name="gender" required>
        <option value="">Select Gender</option>
        <option value="female">Female</option>
        <option value="male">Male</option>
      </select>

      <button type="submit">Get Recommendations</button>
    </form>

    <div id="results"></div>
  </div>

  <script>
    const recommendationTextMap = {
      '✔': 'Strong recommendation',
      '➕': 'Weak recommendation',
      '➖': 'Weak recommendation against',
      '✖': 'Strong recommendation against',
      '🩺': 'Eligible for screening, discuss with provider'
    };

    const screeningData = {
      universal: [],
      female: [],
      male: []
    };

    // Placeholder: Insert complete screening data for universal, female, and male here
    // Format each entry as: { name, guideline, link, test, frequency, brackets: { 'age-range': symbol } }

    function getAgeBracket(age) {
      if (age >= 18 && age <= 20) return '18-20';
      if (age >= 21 && age <= 29) return '21-29';
      if (age >= 30 && age <= 39) return '30-39';
      if (age >= 40 && age <= 49) return '40-49';
      if (age >= 50 && age <= 59) return '50-59';
      if (age >= 60) return '60+';
      return null;
    }

    function getRecommendations(age, gender) {
      const ageBracket = getAgeBracket(age);
      const results = { universal: [], female: [], male: [] };

      ['universal'].forEach(category => {
        screeningData[category].forEach(rec => {
          const symbol = rec.brackets[ageBracket];
          if (symbol && recommendationTextMap[symbol]) {
            results[category].push({ ...rec, symbol, text: recommendationTextMap[symbol] });
          }
        });
      });

      if (gender === 'female') {
        screeningData.female.forEach(rec => {
          const symbol = rec.brackets[ageBracket];
          if (symbol && recommendationTextMap[symbol]) {
            results.female.push({ ...rec, symbol, text: recommendationTextMap[symbol] });
          }
        });
      }

      if (gender === 'male') {
        screeningData.male.forEach(rec => {
          const symbol = rec.brackets[ageBracket];
          if (symbol && recommendationTextMap[symbol]) {
            results.male.push({ ...rec, symbol, text: recommendationTextMap[symbol] });
          }
        });
      }

      return results;
    }

    document.getElementById('screeningForm').addEventListener('submit', function(event) {
      event.preventDefault();
      const age = parseInt(document.getElementById('age').value, 10);
      const gender = document.getElementById('gender').value;
      const results = getRecommendations(age, gender);
      const resultsDiv = document.getElementById('results');

      resultsDiv.innerHTML = '<h2>Screening Recommendations</h2>';

      const renderCategory = (label, items) => {
        if (items.length === 0) return '';
        const ul = document.createElement('ul');
        items.forEach(rec => {
          const li = document.createElement('li');
          li.innerHTML = `
            <strong>${rec.name}</strong><br>
            <em>${rec.text}</em> (${rec.symbol})<br>
            <strong>Test:</strong> ${rec.test}<br>
            <strong>Frequency:</strong> ${rec.frequency}<br>
            <a href="${rec.link}" target="_blank">${rec.guideline}</a>
          `;
          ul.appendChild(li);
        });
        const section = document.createElement('section');
        section.innerHTML = `<h3>${label}</h3>`;
        section.appendChild(ul);
        return section;
      };

      ['universal', 'female', 'male'].forEach(cat => {
        const section = renderCategory(cat.charAt(0).toUpperCase() + cat.slice(1) + ' Screening', results[cat]);
        if (section) resultsDiv.appendChild(section);
      });
    });
  </script>
</body>
</html>



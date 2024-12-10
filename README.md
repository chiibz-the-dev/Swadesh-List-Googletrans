# Swadesh-List-Googletrans
This is a test repository to help people master the fundamental words of a new language that they are learning.

### README: Translating the Swadesh List to Bemba Using Python

---

#### **Program Overview**

This Python script automates the process of translating the Swadesh list of basic vocabulary from English into Bemba. The translations are saved in an Excel spreadsheet using the `openpyxl` library for handling Excel files and the `googletrans` library for translation. It is a practical solution for generating bilingual Swadesh lists.

---

#### **Features**

- Automates the translation of a predefined list of English words into Bemba.
- Saves the English terms and their Bemba translations in an Excel file.
- Handles all tasks programmatically to reduce manual effort.

---

#### **Prerequisites**

1. **Python Installation**:
   Ensure Python 3.x is installed on your system. You can download it from [python.org](https://www.python.org/).

2. **Required Libraries**:
   Install the following Python libraries:
   - `openpyxl`: For creating and managing Excel files.
   - `googletrans==4.0.0-rc1`: For accessing Google Translate services.
   
   Use the following commands to install them:
   ```bash
   pip install openpyxl
   pip install googletrans==4.0.0-rc1
   ```

3. **Internet Access**:
   The script requires an active internet connection to use the Google Translate API.

---

#### **How to Use**

1. **Set Up the Swadesh List**:
   The Swadesh list is hard-coded into the script as an array. If you wish to modify the list, simply edit the `swadesh_list` variable within the script.

2. **Run the Script**:
   Save the script as a `.py` file (e.g., `translate_swadesh.py`) and run it using:
   ```bash
   python translate_swadesh.py
   ```

3. **Output File**:
   The script generates an Excel file named `Swadesh_List_Bemba.xlsx` in the same directory. The file contains two columns:
   - Column 1: English words.
   - Column 2: Their translations in Bemba.

4. **File Location**:
   The path to the saved file is displayed in the console after the script completes.

---

#### **Script Description**

```python
import openpyxl
from googletrans import Translator

# Swadesh list in an array
swadesh_list = [
    "I", "you (singular)", "he", "we", "you (plural)", "they", "this", "that", "here", "there",
    # Add the rest of the words here...
]

# Initialize workbook and worksheet
wb = openpyxl.Workbook()
ws = wb.active
ws.title = "Swadesh List - Bemba"

# Write the English Swadesh list to the first column
for i, word in enumerate(swadesh_list, start=1):
    ws.cell(row=i, column=1, value=word)

# Initialize translator
translator = Translator()

# Translate words and write to the second column
for i, word in enumerate(swadesh_list, start=1):
    try:
        # Translate word from English to Bemba
        translation = translator.translate(word, src='en', dest='bem').text
        ws.cell(row=i, column=2, value=translation)
    except Exception as e:
        print(f"Error translating '{word}': {e}")
        ws.cell(row=i, column=2, value="Translation Error")

# Save the workbook
file_path = "Swadesh_List_Bemba.xlsx"
wb.save(file_path)
print(f"Translations saved in {file_path}")
```

---

#### **Error Handling**

- **Unsupported Language Error**:
   If `googletrans` cannot handle Bemba translations due to an invalid language code, consider:
   - Using an alternative API such as **DeepL** or **LibreTranslate**.
   - Hard-coding translations for unsupported words.

- **API Limitations**:
   Google Translate may restrict access if too many requests are sent in a short period. Introduce a delay between requests if necessary:
   ```python
   import time
   time.sleep(1)  # Pause for 1 second between requests
   ```

- **Network Issues**:
   Ensure stable internet connectivity to avoid translation failures.

---

#### **Future Improvements**

- **Dynamic Language Support**:
   Add an interface for selecting source and target languages dynamically.

- **Batch Processing**:
   Allow importing the Swadesh list from a file (e.g., CSV or text) for easier customization.

- **Alternative Translation Services**:
   Integrate additional APIs for languages not supported by `googletrans`.

---

#### **License**

This script is provided under an open license for educational and personal use. Ensure compliance with the terms of service of the translation API you use.

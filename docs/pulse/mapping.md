---
title: Mapping
parent: Brand Pulse
nav_order: 4
last_modified_date: 2025-01-23 12:00
---

Here’s a refined version with improved flow, clarity, and readability:  

---

# Mapping and Categorising Survey Questions

Over the years, the survey has undergone multiple iterations due to:  
- Changes in client requirements.  
- Addition of new languages.  
- Refinements to improve clarity.  
- Engineering issues on Focal Data’s side that led to formatting changes.  

As a result, we need a **dynamic approach** to mapping various survey questions—despite minor variations—to a **consistent column header** in the final dataset.  

To address this, two key files are used:  
- **`mapping.py`** – Handles standardisation and transformation logic.  
- **`questioncat.py`** – Manages question categorisation.  

Currently, this functionality is only implemented for **New Balance**, with sample files available in the `/new_balance` folder.  

---

## How the Script Processes Survey Questions

The script assumes a standard question format:  

**Format:**  
```  
{Question Number} {Question Text} | {Option}  
```  

**Example:**  
```  
Q14.1 You have indicated that you have purchased trainers from the below brands within the last 12 months. Was this your first ever purchase from that brand? | Nike  
```  

- **Question Number** (`Q14.1`) – Used as a reference but not essential for mapping.  
- **Question Text** (`You have indicated that you have purchased trainers…`) – Used to identify and map questions.  
- **Option** (`Nike`) – Separated into another column.  

---

## Mapping Components (`mapping.py`)

Several variables control how questions and responses are standardised:  

### **1. `RAW_QUESTION_SECTION`**  
Replaces the full raw question text. Useful when the question format **doesn’t** follow the standard structure.  

### **2. `STANDARDISE_QUESTION_SECTION`**  
Extracts the question text after the first whitespace and standardises it.  
- Mainly used for questions **without** response options.  
- Helps ensure consistency in wording across surveys.  

**Example:**  
```  
"Thinking about trainer brands, please list as many as you can remember:"  
→ "Spontaneous Awareness | New Balance"  
```  

### **3. `SURVEY_STANDARDISATION_DICT`**  
Maps question text to a **standardised question number** and a **database-friendly name**.  
- If question wording differs across regions (e.g., "trainers" in the UK vs. "sneakers" in the US), **multiple mappings may be needed**.  

**Example:**  
```  
"Have you bought at least one pair of trainers over the last 12 months?" → "a02-trainer_purchase"  
```  


### **4. `OPTION_STANDARDISATION`**  
Standardises response options to be **database-friendly** (used as column names in the final table).  

**Example:**  
```  
"New Balance" → "03_newbalance"  
```  
- Many options are replaced with numerical prefixes (`02`, `03`, etc.) to improve readability.  
- These values are mapped in the **mapping table**.  

### **5. `RESPONSE_MAP`**  
Maps responses in the **`response`** column based on how we want to visualise the data.  
- Enables grouping and categorisation.  

**Example (Grouping Sentiment Responses):**  
```  
"It’s a brand that I love" → 1  
"It’s a brand that I like" → 1  
"It’s a brand that I don’t like very much" → 0  
"It’s a brand that I don’t like at all" → 0  
```  

Here’s a refined version with improved structure, clarity, and readability:  

---

## **Question Categorisation**  

This module focuses on **filtering survey questions based on their purpose** and ensuring consistency in categorisation.  

### **Meta Table Questions**  

For the `meta` table, we filter and group specific questions:  

```python
META_Q: Final[List[str]] = [
    "a01",  # market
    "a02",  # trainer purchase
    "a03",  # age group
    "q01",  # age
    "a05",  # gender
    "q03",  # statements apply
    "q04",  # statements agree
    "q05",  # monthly activity (run, exercise)
    "s01",  # trainer use locations
    "q13",  # purchase new balance
    "q10",  # planning_purchase_3m
]
```  

These mappings are based on **`SURVEY_STANDARDISATION_DICT`**, ensuring that regardless of the **question number**, the question text is consistently assigned to a **singular identifier**.  

This approach enables:  
- **Easy filtering** – Ensuring questions are correctly grouped.  
- **Consistency** – Standardising questions across different survey versions.  

---

### **Score Remapping**  

Some questions require score transformations for analysis. An example is the **Cultural Scale**, where responses are remapped to a numerical scale:  

```python
CULTURAL_SCALE: Final[Dict[int, int]] = {
    0: -4,
    1: -3,
    2: -2,
    3: -1,
    4: 0,
    5: 0,
    6: 0,
    7: 1,
    8: 2,
    9: 3,
    10: 4,
}
```  

This transformation ensures that responses are interpreted correctly when visualising or analysing the data.  

---

### **Standardising Terms for Visualisation**  

To improve **dashboard readability** and ensure uniformity, certain terms are mapped to **standardised labels**:  

```python
WORD_ASSOCIATION_REPLACE: Final[Dict[str, str]] = {
    "Tops": "TSHIRTS AND TOPS",
    "Trainers/sneakers": "TRAINERS",
    "I tend to purchase items second-hand": "PURCHASE SECOND HAND",
    "I tend to purchase more formal trainers / clothes": "PURCHASE MORE FORMAL",
    "Hoodies": "HOODIES AND SWEATSHIRTS",
    "Accessories (e.g. hats, socks, headbands, bags)": "ACCESSORIES",
    "Any other high street retailer": "OTHER HIGH STREET RETAILER",
    "Bags": "ACCESSORIES",
    "Online marketplace (e.g. Asos.com)": "ONLINE MARKETPLACE",
    "New Balance is not popular among my friends/family": "NOT POPULAR AMONG FAMILY FRIENDS",
    "Sweatshirts": "HOODIES AND SWEATSHIRTS",
    "NewBalance.com": "NEW BALANCE WEB",
    "I have no need for new trainers / clothes": "I HAVE NO NEED",
    "T-shirts + tops": "TSHIRTS AND TOPS",
    "Soccer": "SOCCER",
    "Down jacket": "DOWN JACKET",
    "I have a preference for other brands": "PREFERENCE FOR OTHER BRANDS",
    "Sweatpants, leggings, tights or shorts": "SWEATPANTS AND LEGGINGS",
    "I have sustainability/environmental concerns about New Balance": "ENVIRONMENTAL CONCERNS",
    "Shorts": "SWEATPANTS AND LEGGINGS",
    "New Balance is too expensive": "TOO EXPENSIVE",
    "Outerwear (e.g. jackets, vests)": "OUTERWEAR",
    "Hoodies + sweatshirts": "HOODIES AND SWEATSHIRTS",
    "I haven’t had a good experience with New Balance in the past": "BAD PAST EXPERIENCE",
    "I've recently bought from New Balance": "MADE RECENT PURCHASE",
    "New Balance retail store": "NEW BALANCE RETAIL",
    "Sweatpants": "SWEATPANTS AND LEGGINGS",
    "Backpack": "ACCESSORIES",
    "None of the above": "NONE",
    "Other (please specify)": "OTHER",
}
```  

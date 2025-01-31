# Efficient Log Retrieval from a Large File  

## 📌 Problem Statement  
We need to extract logs efficiently from a **1TB log file** where logs are evenly distributed across dates. The solution must be optimized for **speed** and **memory usage**, ensuring that retrieving logs for a specific date is as fast as possible.  

---

## 🔍 **Approaches Considered**  

### 1️⃣ **Naive Approach (Line-by-Line Scan)**
**📌 Idea:**  
- Open the log file and scan every line.
- Check if the line starts with the required date.
- If yes, store it in an output file.  

**❌ Drawbacks:**  
- **O(N) time complexity** (where N is the number of lines).  
- Inefficient for a **1TB** file as it requires reading the entire file even if we only need a small portion.  
- **Memory inefficient** since it holds unnecessary logs in memory.  

---

### 2️⃣ **Indexing-Based Approach (Final Solution)**
**📌 Idea:**  
- Create an **index file** mapping **dates → byte positions** in the log file.  
- Use **binary search** to quickly locate the starting position for a given date.  
- Extract logs **without scanning unnecessary lines**.  

**✅ Advantages:**  
- **O(log N) lookup time** due to binary search.  
- Only reads **relevant logs**, improving efficiency.  
- **Minimal memory usage**, as we only store the index in RAM.  

---

## 🏆 **Final Solution Explanation**  
Our final solution follows **three main steps:**  

### **1️⃣ Index Creation**  
- We **scan the log file once** and store the **byte position** where each date begins.  
- This is stored in a separate `log_index.txt` file.  
- It ensures **fast lookups** in future queries.  

### **2️⃣ Fast Log Extraction**  
- We **load the index into memory**.  
- We perform a **binary search** to locate the starting position of the requested date.  
- We read logs **only for that date** and stop as soon as the date changes.  

### **3️⃣ Efficient Storage & Retrieval**  
- Extracted logs are saved in `output/output_YYYY-MM-DD.txt`.  
- If the index doesn’t exist, it's created automatically.  

---

## 🚀 **Performance Analysis**  
| Approach         | Time Complexity | Space Complexity | Scalability |
|-----------------|---------------|----------------|-------------|
| Naive Scan      | O(N)          | O(1)           | 🚨 Slow for large files |
| Indexed Lookup  | O(log N) + O(M) | O(log N) (index size) | ⚡ Fast & Efficient |

- **N = Total number of log entries**  
- **M = Number of log entries on the requested date**  

---

## 🛠 **How to Run the Script?**  
### **🔹 Step 1: Download the Log File**

###Project Structure
/log-extractor
│── src/
│   ├── extract_logs.py   # Main log extraction script
│── README.md             # Instructions & setup
│── DISCUSSION.md         # This file (Solution discussion)
│── test_logs.log         # Sample log file
│── log_index.txt         # Auto-generated index file
│── output/               # Extracted logs output folder

## 🔥 Why This Approach?  

✅ **Scalability**  
   - Designed to handle **1TB+ log files** efficiently without excessive disk reads.  

✅ **Optimized Retrieval**  
   - **Uses indexing & binary search** for fast lookups, reducing search time from **O(N) to O(log N)**.  
   - Reads only the relevant portion of the file instead of scanning the entire log.  

✅ **Minimal Memory Usage**  
   - Loads only the **index file** (a few MBs) into RAM, making it highly **memory efficient**.  
   - Doesn't store unnecessary logs in memory—everything is processed **line by line**.  

🚀 **With this approach, extracting logs for a specific date takes only a few seconds, even from a 1TB file!**  

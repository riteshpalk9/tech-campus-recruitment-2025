Discussion

Solutions Considered

1. Linear Search for Log Extraction

Initially, one approach considered was scanning the entire log file line by line to extract logs for a given date. This would work for small log files but would become highly inefficient for large files due to the high time complexity of O(n), where n is the number of lines in the log file.

2. Using an Index File with Binary Search

To optimize log retrieval, an index file mapping dates to byte positions in the log file was introduced. This allows for O(log n) lookup time using binary search, followed by O(m) time for reading logs sequentially from the determined byte position. This significantly improves performance for large log files.

3. Database Storage

Another approach was to store logs in a database and use SQL queries for efficient retrieval. While this would provide robust indexing and query capabilities, it introduces additional setup complexity and might not be ideal for quick, standalone log extraction.

Final Solution Summary

The final approach chosen was to create an index file and use binary search to quickly locate log entries for a given date. This method provides a balance between simplicity and efficiency, as it avoids the overhead of a full database setup while drastically improving search performance compared to linear scanning.

Advantages of this approach:

Efficient Log Retrieval: Binary search significantly reduces search time.

Scalability: Works well for large log files.

Simple Implementation: No need for additional dependencies like a database.

Steps to Run

Ensure Required Files Exist:

Place the log file (test_logs.log) in the working directory.

If an index file (log_index.txt) does not exist, it will be created automatically.

Run the Script:

python extract_logs.py YYYY-MM-DD

Replace YYYY-MM-DD with the desired date to extract logs for that day.

Check the Output Directory:

Extracted logs will be saved in the output/ directory as output_YYYY-MM-DD.txt.

If no logs exist for the given date, the script will notify the user.

Regenerate Index (If Needed):

If new logs are added and need to be indexed, delete log_index.txt and rerun the script to recreate the index.

This approach ensures quick and efficient log retrieval while keeping the implementation straightforward.


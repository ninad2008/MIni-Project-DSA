Hospital Management System (DSA Project)
A console-based Hospital Management System implemented in C++ that demonstrates core data structures and algorithms from a Data Structures & Algorithms (DSA) course. The program supports patient registration, searching, sorting, deletion with undo, appointment queueing, patient history tracking, priority grouping with an AVL tree, greedy bed assignment, and file I/O persistence.

Table of Contents
* Project overview
* Features
* Data structures & complexity
* Files
* Build & run
* Usage / Example session
* File format (patients.txt)
* Limitations
* Suggested improvements
* License

Project overview
This project is a small, self-contained console application that models basic hospital workflows while illustrating use of arrays, stack, queue, linked list, and AVL tree. Patients are stored in an array for quick indexing; an AVL tree groups patients by priority (Critical/Urgent/Routine) and maintains buckets (linked lists) of patients in each priority node. A linked list stores a history of added patients. Deleted patients are kept on a stack to support undo. An appointment queue models FIFO appointment handling.

1. Features
* Add new patient (auto-assigned ID).
* View all registered patients.
* Search patients:
  * Linear search by name (O(n)).
  * Binary search by ID (sorts copy then binary search, O(log n) after sort).
  * AVL search by priority (O(log n)).
* Sort patients:
  * Bubble sort by ID.
  * Merge sort by name.
  * Quick sort by priority (on a copy).
* Delete a patient (stores deleted patient on undo stack and removes from AVL).
* Undo last delete using a stack (LIFO).
* Appointment management (queue): book, call next, list appointments.
* Patient history using a linked list (most recent first).
* Priority grouping using an AVL tree; each AVL node contains a bucket (linked list) of patients sharing that priority.
* Greedy bed assignment: assign available beds to highest-priority patients first.
* Save/load patients to/from a text file (patients.txt).

2. Data structures & time complexity
* Array (patients): O(1) insert (amortized here with fixed max), O(n) traversal.
* Linked list (history): O(1) insert, O(n) traverse.
* Stack (undo): O(1) push/pop for undo deletes.
* Queue (appointmentQ): O(1) enqueue/dequeue for appointments.
* AVL tree (avlRoot): O(log n) insert/search; each node holds a bucket (linked list) of patients for that priority.
* Sorting/searching methods included: bubble (O(n^2)), merge (O(n log n)), quick (O(n log n) average), linear search (O(n)), binary search (O(log n) after sorting).

3. Big-O summary (selected):
* Add patient: O(1) (array insert) + O(log n) (AVL insert)
* AVL search: O(log n)
* Delete patient: O(n) (array shift) + O(log n) (AVL bucket removal)
* Undo delete: O(1) + O(log n) (AVL insert)
* Save/load file: O(n)

4. Files
* main.cpp — full source code (the provided C++ program).
* patients.txt — data file used for persistence (created/used by Save/Load).

5. Build & run
Prerequisites: A C++ compiler supporting C++11 or later (g++, clang++).

6. Compile:
* g++:
* g++ -std=c++11 -O2 -o hms main.cpp

7. Run:
./hms

8. On Windows (MinGW):
g++ -std=c++11 -O2 -o hms.exe main.cpp
hms.exe

9. Usage / Example session
Start program: it prints a menu.
Choose 1 to add a patient. Enter name, age, disease, and priority (1,2,3).
Choose 2 to view all patients.
Choose 3 to search (linear by name, binary by ID, or AVL by priority).
Choose 4 to sort (bubble/merge/quick).
Choose 5 to delete by ID — deleted patient is pushed to undo stack.
Choose 6 to undo the last delete (restores patient).
Choose 7 for appointment queue: book, call next, or view queue.
Choose 8 to view history (linked list of added patients).
Choose 9 to view priority grouping using the AVL tree (in-order: Critical->Urgent->Routine).
Choose 10 to run greedy bed assignment given number of beds.
Choose 11 to save/load patients to/from patients.txt.
Choose 0 to exit.

Example — add patient:
Add "Alice", age 30, disease "Fever", priority 3 → stored in array, history, and AVL bucket.
Example — delete and undo:
Delete patient ID 2 → patient pushed to undo stack and removed from AVL.
Undo delete → patient popped from undo stack and re-inserted.
File format (patients.txt)
Each patient is saved as five lines:
* id
* name
* age
* disease
* priority

Multiple patients are written sequentially. Loading expects the same format.

10. Limitations
* Fixed maximum number of patients: MAX_PATIENTS = 100.
* No concurrency / multi-user support.
* Minimal input validation (e.g., non-integer inputs can be handled, but some inputs rely on simple checks).
* AVL removal only removes from the bucket (linked list) for a priority but does not free or rebalance AVL nodes if a node’s bucket becomes empty; tree node removal and rebalancing are not implemented.
* Binary search sorts a local copy with bubble sort for simplicity; not optimized for large data.
* No unique constraint on patient name; searches by name require exact match (case-sensitive).
* No encryption or secure storage for files.
* Basic console UI only.

11. Suggested improvements
* Replace fixed-size arrays with std::vector for dynamic sizing.
* Implement AVL node deletion with full rebalancing when a priority bucket becomes empty.
* Improve input validation and error handling.
* Use case-insensitive and partial string matching for name search.
* Provide CSV or JSON file format for portability and easier parsing.
* Add persistent unique ID generation and avoid collisions.
* Add unit tests for core DSA operations.
* Improve sorting/searching to use STL algorithms (std::sort, std::binary_search).
* Add a better UI (ncurses or GUI) and/or REST API (using FastAPI/Crow/Boost.Beast) for multi-user access.


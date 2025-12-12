Adaptive Resource Allocation in Multiprogramming Systems

This project implements a real-time adaptive resource allocation system using Python,
designed to simulate how an operating system manages CPU and memory across multiple running programs.

The system launches actual child processes, monitors them using psutil, and dynamically adjusts
resources using:

Process priorities (nice values)

Pause / Resume via signals

Feedback-based adaptive decision engine

Real-time performance monitoring UI (PyQt6)

🚀 Features
🔹 1. Real Process Execution

Launch CPU-bound and Memory-bound jobs

Each job runs as a separate process

Assigned a PID and monitored in real-time

🔹 2. Monitoring System

Using psutil, the system tracks:

Per-process CPU usage

Per-process memory usage

Global system CPU percent

Global memory percent

Displayed live in the GUI every second.

🔹 3. Adaptive Allocation Engine

Heuristics:

Condition	Action
Memory usage > 80%	Pause highest-memory process
CPU usage < 40%	Resume paused process OR Boost priority
Multiple jobs competing	Prioritize CPU jobs

This prevents system overload and increases efficiency.

🔹 4. Desktop GUI (PyQt6)

The GUI provides:

Live system resource stats

Process table with CPU%, Memory MB, State, Priority

Buttons to start CPU and Memory jobs

Pause/Resume selected job

Real-time action log

🔹 5. Safe Windows Multiprocessing Support

Uses:

mp.set_start_method("spawn")


And a separate job_worker.py to avoid re-import loops, making the system fully stable on Windows.

🏛️ System Architecture
+------------------------------+
|        PyQt6 GUI             |
|  - Start Jobs                |
|  - Pause/Resume              |
|  - Display Metrics           |
+--------------+---------------+
               |
               v
+--------------+---------------+
|         Monitor Module       |
|  - Launch processes          |
|  - Collect CPU/MEM           |
|  - Track states              |
+--------------+---------------+
               |
               v
+--------------+---------------+
|   Adaptive Allocation Engine |
|  - Heuristic decisions       |
|  - Pause/Resume jobs         |
|  - Boost priority            |
+--------------+---------------+
               |
               v
+--------------+---------------+
|   Process Workers (Jobs)     |
|  - CPU job (infinite loop)   |
|  - MEM job (increasing list) |
+------------------------------+

📁 Project Structure
AdaptiveAllocator/
│
├── main.py
├── monitor.py
├── monitoring_job.py
├── allocator_engine.py
├── mainwindow_gui.py
└── job_worker.py

🛠️ Technologies Used
Component	Technology
GUI	PyQt6
Monitoring	psutil
Process Control	multiprocessing, subprocess
Priority Management	nice()
Pause/Resume	Windows process control (CREATE_NEW_PROCESS_GROUP)
OS	Windows (spawn mode), Linux-ready
🧪 How to Run

Install dependencies:

pip install psutil PyQt6


Run the project:

python main.py

📷 Demo (Expected Behavior)

CPU Job → CPU load increases

Memory Job → memory usage increases

Engine pauses jobs if memory exceeds 80%

Engine resumes jobs if CPU is idle

Priority of CPU jobs increases dynamically

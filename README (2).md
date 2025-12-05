# Intelligent CPU Scheduler Simulator (Python)

This project is a simple simulator that demonstrates how different CPU scheduling algorithms work in an Operating System. The goal of this project is to take user input for processes and then show how each scheduling algorithm executes them along with the waiting time and turnaround time.

The algorithms implemented in this project are:
- FCFS (First Come First Serve)
- SJF (Shortest Job First, Non-preemptive)
- Priority Scheduling (Non-preemptive)
- Round Robin Scheduling

The program also generates a Gantt Chart using matplotlib so that the execution flow can be visualized easily.

---

## Features of the Simulator

1. Takes input for:
   - Arrival Time
   - Burst Time
   - Priority (for Priority Scheduling)
   - Time Quantum (for Round Robin)

2. Shows detailed execution order based on the selected algorithm.

3. Displays:
   - Waiting Time for each process
   - Turnaround Time for each process
   - Average Waiting Time
   - Average Turnaround Time

4. Plots a Gantt Chart for better understanding of CPU scheduling.

---

## Technologies Used

- Python 3
- Matplotlib library
- Collections module (used for Round Robin queue)
- Basic input/output for user interaction

---

## How to Run the Program

1. Install matplotlib if not installed:
```
pip install matplotlib
```

2. Run the Python file:
```
python scheduler.py
```

3. Enter the number of processes and required details as asked by the program.

4. Choose any one of the four scheduling algorithms.

5. The program will show the calculated waiting times, turnaround times, averages, and the Gantt Chart.

---

## Example Output Format

Process    Waiting Time    Turnaround Time  
P1         0               5  
P2         4               7  
P3         6               10  

Average Waiting Time = 3.33  
Average Turnaround Time = 7.33  

---

## Purpose of the Project

This project has been created as a part of the Operating Systems course to better understand scheduling algorithms and how they impact CPU performance. The simulator helps visualize how the CPU behaves with different algorithms.

---

## Author
Tejesh Kadiyam  
B.Tech CSE

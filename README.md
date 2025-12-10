Intelligent CPU Scheduler Simulator (Python)

This project is a simple simulator that shows how different CPU scheduling algorithms work in an Operating System. The idea is to take user input for processes and then display how each scheduling algorithm executes those processes along with their waiting time and turnaround time.

The algorithms included in this project are:
- FCFS (First Come First Serve)
- SJF (Shortest Job First, Non-preemptive)
- Priority Scheduling (Non-preemptive)
- Round Robin Scheduling

A Gantt Chart is generated using matplotlib to help visualize how the CPU processes tasks over time.

Features of the Simulator

1. Accepts input for:
   - Arrival Time
   - Burst Time
   - Priority (for Priority Scheduling)
   - Time Quantum (for Round Robin)

2. Shows the sequence of process execution.

3. Displays:
   - Waiting Time
   - Turnaround Time
   - Average Waiting Time
   - Average Turnaround Time

4. Generates a Gantt Chart for better visualization.

Technologies Used

- Python 3
- Matplotlib library
- Collections module (used for Round Robin queue)
- Simple input/output for process handling

How to Run the Program

1. Install matplotlib:
pip install matplotlib

2. Run the program:
python scheduler.py

3. Enter the number of processes and fill in the required details.

4. Choose any one of the four scheduling algorithms.

5. The output will display the calculated times and show the Gantt Chart.

Example Output Format

Process    Waiting Time    Turnaround Time  
P1         0               5  
P2         4               7  
P3         6               10  

Average Waiting Time = 3.33  
Average Turnaround Time = 7.33  

## Purpose of the Project

This project was created as part of the Operating Systems course to understand scheduling algorithms better and to visualize how they perform in different situations.



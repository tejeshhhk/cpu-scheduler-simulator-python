# CPU Scheduler Simulator - Improved Readability Version (Commit 3)
# Small comments and spacing added to make the code easier to understand.

import matplotlib.pyplot as plt
from collections import deque

# Function to draw the Gantt Chart on screen
def plot_gantt_chart(schedule, title):
    fig, ax = plt.subplots(figsize=(10, 3))
    
    # Each item in schedule contains (start_time, end_time, process_name)
    for task in schedule:
        start, end, process = task
        ax.barh(1, end - start, left=start, edgecolor='black')
        ax.text((start + end) / 2, 1, process, ha='center', va='center', color='white')
    
    ax.set_title(title)
    ax.set_xlabel("Time")
    ax.set_yticks([])
    plt.show()


# --------------------------------
# FCFS Scheduling
# --------------------------------
def fcfs(processes):
    processes.sort(key=lambda x: x['arrival'])  # Sort based on arrival time
    time = 0
    schedule = []
    WT = []
    TT = []

    for p in processes:
        if time < p['arrival']:
            time = p['arrival']   # Wait until the process arrives
        
        start = time
        end = start + p['burst']

        schedule.append((start, end, p['name']))
        time = end

        WT.append(start - p['arrival'])
        TT.append(end - p['arrival'])

    return schedule, WT, TT


# --------------------------------
# SJF (Non-Preemptive)
# --------------------------------
def sjf(processes):
    processes = processes.copy()
    time = 0
    schedule = []
    WT = []
    TT = []

    while processes:
        available = [p for p in processes if p['arrival'] <= time]
        
        if not available:
            time += 1
            continue

        current = min(available, key=lambda x: x['burst'])
        
        start = time
        end = start + current['burst']
        schedule.append((start, end, current['name']))

        WT.append(start - current['arrival'])
        TT.append(end - current['arrival'])

        time = end
        processes.remove(current)

    return schedule, WT, TT


# --------------------------------
# Priority Scheduling (Non-Preemptive)
# --------------------------------
def priority_scheduling(processes):
    processes = processes.copy()
    time = 0
    schedule = []
    WT = []
    TT = []

    while processes:
        available = [p for p in processes if p['arrival'] <= time]

        if not available:
            time += 1
            continue

        current = min(available, key=lambda x: x['priority'])  # Lower number = higher priority

        start = time
        end = start + current['burst']
        schedule.append((start, end, current['name']))

        WT.append(start - current['arrival'])
        TT.append(end - current['arrival'])

        time = end
        processes.remove(current)

    return schedule, WT, TT


# --------------------------------
# Round Robin Scheduling
# --------------------------------
def round_robin(processes, quantum):
    queue = deque()
    time = 0
    schedule = []

    remaining = {p['name']: p['burst'] for p in processes}    # Track remaining burst
    WT = {p['name']: 0 for p in processes}
    last_exec = {p['name']: p['arrival'] for p in processes}

    processes.sort(key=lambda x: x['arrival'])
    index = 0

    while index < len(processes) or queue:

        # Add all processes that have arrived
        while index < len(processes) and processes[index]['arrival'] <= time:
            queue.append(processes[index])
            index += 1

        if not queue:
            time = processes[index]['arrival']
            continue

        current = queue.popleft()
        exec_time = min(quantum, remaining[current['name']])

        start = time
        end = start + exec_time

        schedule.append((start, end, current['name']))

        WT[current['name']] += start - last_exec[current['name']]
        remaining[current['name']] -= exec_time
        last_exec[current['name']] = end

        time = end

        if remaining[current['name']] > 0:
            queue.append(current)

    # Convert dicts to list format
    TT = [WT[name] + (0 if remaining[name] <= 0 else remaining[name]) for name in WT]

    return schedule, list(WT.values()), TT


# --------------------------------
# Main Program
# --------------------------------
print("\n--- Intelligent CPU Scheduler Simulator ---\n")

n = int(input("Enter number of processes: "))
processes = []

for i in range(n):
    name = f"P{i+1}"
    arrival = int(input(f"Arrival Time of {name}: "))
    burst = int(input(f"Burst Time of {name}: "))
    priority = int(input(f"Priority of {name}: "))

    processes.append({
        "name": name,
        "arrival": arrival,
        "burst": burst,
        "priority": priority
    })

print("\nChoose Scheduling Algorithm:")
print("1. FCFS")
print("2. SJF")
print("3. PRIORITY")
print("4. ROUND ROBIN")

choice = int(input("Enter choice: "))

if choice == 1:
    schedule, WT, TT = fcfs(processes)
    title = "FCFS Scheduling Gantt Chart"

elif choice == 2:
    schedule, WT, TT = sjf(processes)
    title = "SJF Scheduling Gantt Chart"

elif choice == 3:
    schedule, WT, TT = priority_scheduling(processes)
    title = "Priority Scheduling Gantt Chart"

elif choice == 4:
    quantum = int(input("Enter Time Quantum: "))
    schedule, WT, TT = round_robin(processes, quantum)
    title = "Round Robin Scheduling Gantt Chart"

else:
    print("Invalid choice!")
    exit()

print("\n--- OUTPUT ---")
print("\nGantt Chart:", schedule)

print("\nProcess    Waiting Time    Turnaround Time")
for i, p in enumerate(processes):
    print(f"{p['name']:8} {WT[i]:14} {TT[i]:17}")

print(f"\nAverage Waiting Time = {sum(WT)/len(WT):.2f}")
print(f"Average Turnaround Time = {sum(TT)/len(TT):.2f}")

plot_gantt_chart(schedule, title)

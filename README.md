### Program:
```
Name: Aruru Sai Bandhavi
Reg No: 212221240006
```
```
import queue
import random
import time
def hot_potato(names, num):
    sim_queue = queue.Queue()
    for name in names:
        sim_queue.put(name)
    while sim_queue.qsize() > 1:
        for _ in range(num):
            sim_queue.put(sim_queue.get())
        eliminated = sim_queue.get()
        print(f"{eliminated} is eliminated!")
    return sim_queue.get()
def main():
    players = ["Alice", "Bob", "Charlie", "David", "Eve"]
    num_passes = random.randint(1, 10)
    #num_passes=2
    print("Hot Potato Game Start!")
    time.sleep(1)
    winner = hot_potato(players, num_passes)
    print(f"\nThe winner is: {winner}")
if __name__ == "__main__":
    main()
```
### Output:
![image](https://github.com/user-attachments/assets/39d268b3-8d99-4032-9966-6e64b4952e19)

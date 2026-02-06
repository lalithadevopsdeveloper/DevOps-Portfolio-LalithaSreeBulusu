# Linux System Performance & Process Management - Complete Guide

## Lab Overview
**Platform:** Amazon Linux 202
**Duration:** 2-3 hours  
**Goal:** Master process management, CPU, memory, and I/O monitoring

---
### What is a Process?

A process is a running program. When you start an application, the OS creates a process for it.

**Every process has:**
- PID (Process ID) - Unique identifier
- Parent PID (PPID) - Who started this process
- User - Who owns the process
- State - Running, Sleeping, Stopped, Zombie
- Priority - How important it is
- Resources - CPU, Memory it's using

---
### View All Processes

```bash
# See all processes (snapshot)
ps aux
```
![alt text](image.png)


```bash
ps aux | head -20
```

![alt text](image-1.png)


### finding specific processes

```bash
ps aux | grep nginx
```
![alt text](image-2.png)

```bash
pgrep nginx
ps -p 10 -f
```
![alt text](image-3.png)
![alt text](image-4.png)

```bash
pstree
```
![alt text](image-5.png)

## Process tree with parent id ##
** Every process has a parent and pid 1 is the init system(systemmd on linux)
```bash
pstree -p
```
![alt text](image-6.png)
![alt text](image-7.png)
![alt text](image-8.png)

**Key Concept** Kill a parent process all the children will die too. 

---
## Real time CPU Monitoring with top
```bash
top
```
![alt text](image-9.png)

```bash
htop -u ec2-user
```

![alt text](image-10.png)

## Finding CPU hogs
```bash
# Top 4 CPU consumers
ps aux --sort=-%cpu | head -5
```
![alt text](image-11.png)

```bash
#continously monitor top cpu user
watch -n 1 'ps aux --sort=-%cpu | head'
ps -eo pid --sort=-%cpu | head -4
ps -eo %mem --sort=-%cpu | head
```

![alt text](image-12.png)
![alt text](image-13.png)

##Load Average
```bash
uptime
nproc
lscpu
```
![alt text](image-14.png)
![alt text](image-15.png)
![alt text](image-16.png)

## Generating CPU Load for Testing
** Excercise 1
```bash
stress-ng --cpu 1 --timeout 30s
```
![alt text](image-18.png)
![alt text](image-17.png)

**Excercise 2
```bash
# Terminal 1
stress-ng --cpu 2 --timeout 120s
# Terminal 2
uptime
```
** Terminal 1 output 
![alt text](image-21.png)
** Terminal 2 output
![alt text](image-19.png)
![alt text](image-20.png)
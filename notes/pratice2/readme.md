
# Kubernetes Practice Challenges (Jobs, CronJobs, Services, DaemonSets)

---

# Job Challenges

### Challenge 1
Create a Job named `hello-job` that runs a container using the `busybox` image and prints `Hello Kubernetes` once.

---

### Challenge 2
Create a Job named `date-job` that runs `date` inside a `busybox` container.

---

### Challenge 3
Create a Job named `retry-job` that runs the command `exit 1` using `busybox`.  
The job should retry **4 times** before failing.

---

### Challenge 4
Create a Job named `parallel-job` that runs **5 pods** in parallel and completes when **5 successful executions** occur.  
Each pod should run `echo parallel job`.

---

### Challenge 5
Create a Job named `sleep-job` that runs a container using `busybox` and executes `sleep 30`.

---

# CronJob Challenges

### Challenge 6
Create a CronJob named `hello-cron` that runs every **minute** and prints `Hello from CronJob`.

---

### Challenge 7
Create a CronJob named `time-printer` that runs every **2 minutes** and executes the `date` command.

---

### Challenge 8
Create a CronJob named `cleaner-cron` that runs every **3 minutes** using `busybox` and prints `cleanup task`.

---

### Challenge 9
Create a CronJob named `limited-history-cron` that runs every **minute** and keeps only:
- 2 successful jobs
- 1 failed job

---

### Challenge 10
Create a CronJob named `long-run-cron` that runs every **5 minutes** and executes `sleep 20`.

---

# Service Challenges

### Challenge 11
Create a Deployment named `nginx-deploy` with **3 replicas** using the `nginx` image.

---

### Challenge 12
Expose the `nginx-deploy` Deployment with a **ClusterIP Service** named `nginx-service` on port **80**.

---

### Challenge 13
Create a **NodePort Service** named `nginx-nodeport` that exposes the nginx pods on port **30007**.

---

### Challenge 14
Create a Deployment named `httpd-deploy` using the `httpd` image with **2 replicas**.

---

### Challenge 15
Expose `httpd-deploy` using a **ClusterIP Service** named `httpd-service` on port **80**.

---

# DaemonSet Challenges

### Challenge 16
Create a DaemonSet named `busybox-daemon` that runs a `busybox` container executing `sleep 3600`.

---

### Challenge 17
Create a DaemonSet named `logger-daemon` using `busybox` that runs the command `echo logging`.

---

### Challenge 18
Label one node with `env=prod` and create a DaemonSet named `prod-daemon` that runs only on nodes with that label.


---


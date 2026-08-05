# Day 17 — DevOps Interview Prep

**Delhivery DevOps Intern — R1 Interview Prep Guide**

**Candidate:** Atrayee Pathak  
**Interviewer:** Bhaskar Prajapati (Senior DevOps Engineer, Delhivery)  
**Date & Time:** Wednesday, 5 Aug 2026, 5:00 PM – 6:00 PM IST  
**Location / Link:** Google Meet (meet.google.com/nsy-okdc-htu)

---

## 1. Self-Pitch (Introduction)

**When to use:** Open with this if asked "Tell me about yourself" or "Walk me through your resume."

> "I'm a final-year CS Engineering student at UPES, graduating this year. I've completed two internships — a full-stack internship at Wheels on Lease working with Next.js, NestJS, and PostgreSQL, and a DevOps internship at Austere System Limited where I worked hands-on with Terraform and deployment pipelines. 
> 
> That DevOps internship made me fall in love with infrastructure work because I enjoyed making sure systems stay up, scale, and recover gracefully — rather than just making code work on my local machine. Since then, I've built a public GitHub portfolio featuring a Terraform/AWS infrastructure lab and a daily learning log. I'm looking to bring this mix of full-stack understanding and infrastructure hands-on experience to Delhivery."

* **Tip:** Keep it under 90 seconds. Rehearse it out loud twice before the call!

---

## 2. Behavioral & HR Questions

### Q: Why DevOps?
* **Answer:** "During my internship, I realized I liked system reliability, automation, and scaling more than just building pure application features. I love knowing how code actually runs reliably in production."

### Q: Why Delhivery?
* **Answer:** "Delhivery operates at massive scale — handling millions of shipments across 18,000+ pin codes. Managing infrastructure, high availability, and automated scaling at that scale is an exciting engineering challenge that I want to learn from and contribute to."

### Q: Why should we hire you?
* **Answer:** "I bring a rare combination of full-stack coding (Next.js/NestJS) and practical DevOps tooling (Terraform, AWS, Docker). Plus, I am a self-driven learner with an active GitHub portfolio and daily learning commits."

---

## 3. CI/CD (Continuous Integration & Delivery)

### Q: Walk me through a CI/CD pipeline you have set up.
* **Answer:** 
  1. **Trigger:** Developer pushes code or creates a Pull Request on GitHub.
  2. **Lint & Test:** Automatically run code formatting checks, unit tests, and security scans.
  3. **Build:** Build and tag the Docker container image.
  4. **IaC Check:** Run `terraform plan` to preview infrastructure updates.
  5. **Deploy:** Deploy automatically (or via manual approval step) to the environment using `terraform apply` or image deployment.

### Q: Difference between CI, Continuous Delivery, and Continuous Deployment?
* **Continuous Integration (CI):** Automatically building and testing code on every commit to catch bugs early.
* **Continuous Delivery:** Automatically testing and preparing code for production, but requiring a **manual human click** to deploy to live production.
* **Continuous Deployment:** Fully automated pipeline — every change that passes all tests goes **straight to production** with zero human intervention.

### Q: A pipeline fails intermittently (flaky pipeline). How do you debug it?
* **Answer:** 
  1. Check if it's a **flaky test** vs a **runner resource issue** (e.g., running out of memory/disk space).
  2. Read step-by-step runner logs to pinpoint the exact failing command.
  3. Try reproducing the step locally on your machine.
  4. Look for race conditions, network timeouts, or third-party dependency updates.

### Q: How do you handle application rollbacks?
* **Answer:** Keep deployments **versioned and immutable**. Never deploy using mutable tags like `latest`; always use explicit tags (like `v1.2.0` or git commit hashes). Rollback simply means redeploying the previous known-good container tag.

---

## 4. Docker & Containerization

### Q: Difference between an Image and a Container?
* **Docker Image:** A read-only template with instructions/layers used to build a container (like a blueprint or class).
* **Docker Container:** A running instance of an image (like an object created from a class).

### Q: What is a Multi-Stage Build and why use it?
* **Answer:** Using multiple `FROM` statements in one `Dockerfile`. You build the application in a heavy first stage (with SDKs and compilers), then copy **only the final executable** into a tiny runtime stage. This keeps the production image extremely small and secure.

### Q: Docker Volumes vs. Bind Mounts?
* **Volumes:** Managed fully by Docker on the host machine. Portable, secure, and easy to back up.
* **Bind Mounts:** Maps a direct path from the host file system into the container. Dependent on host folder paths.

### Q: How do you debug a container stuck in a crash loop?
* **Answer:**
  1. `docker logs <container_id>` to view terminal errors/exceptions.
  2. `docker inspect <container_id>` to check exit codes (**Exit code 137** = Out of Memory / OOM Kill).
  3. Run it interactively to test: `docker run -it --entrypoint sh <image_name>`.

### Q: CMD vs. ENTRYPOINT?
* **ENTRYPOINT:** Sets the fixed main command that always runs when the container starts.
* **CMD:** Provides default flags or default commands that can be easily overridden at runtime during `docker run`.

### Q: COPY vs. ADD?
* **COPY:** Simply copies local files into the container. Best practice for 95% of cases.
* **ADD:** Can pull files from remote URLs and automatically extract `.tar` archives.

### Q: How would you containerize a Flask application?
* **Answer:**
  1. Base image: `FROM python:3.11-slim`
  2. Copy `requirements.txt` and run `pip install -r requirements.txt`
  3. Copy app code into `/app` directory
  4. Expose port `5000`
  5. Run production server: `CMD ["gunicorn", "-w", "4", "-b", "0.0.0.0:5000", "app:app"]`

### Q: Container Security Best Practices?
* **Answer:** Always run containers as non-root users (`USER appuser`) and scan images for security vulnerabilities using tools like **Trivy** or **Docker Scout**.

---

## 5. Linux Fundamentals

### Q: How do you check CPU and Memory usage on a server?
* **Live Monitoring:** `top` or `htop`
* **Process Snapshot:** `ps aux --sort=-%cpu` (CPU) or `ps aux --sort=-%mem` (RAM)
* **System RAM:** `free -h`

### Q: Explain file permissions: What does `chmod 755` mean?
* **Owner (7):** Read (4) + Write (2) + Execute (1) = **7** (Full access)
* **Group (5):** Read (4) + Execute (1) = **5** (Read & execute only)
* **Others (5):** Read (4) + Execute (1) = **5** (Read & execute only)

### Q: How do you find which process is using port 8080?
* `sudo lsof -i :8080` OR `sudo netstat -tulpn | grep 8080`

### Q: Hard Link vs. Soft (Symbolic) Link?
* **Hard Link:** Directly points to the file's data block (inode). Deleting the original file does **not** break a hard link.
* **Soft Link (Shortcut):** Points to the file path. If you delete or move the original file, the soft link breaks.

### Essential Linux Commands Cheat Sheet
* `ps`: View running processes
* `grep`: Search for text patterns inside files or output
* `find`: Search for files on the disk
* `systemctl`: Start, stop, or check status of system background services (`systemctl status nginx`)
* `journalctl`: View logs generated by system services (`journalctl -u nginx -f`)

---

## 6. Networking Fundamentals

### Q: What happens when you type a URL into a browser?
1. **DNS Lookup:** Browser resolves domain name (e.g., google.com) to an IP address.
2. **TCP Handshake:** Establishes connection via 3-way handshake (SYN → SYN-ACK → ACK).
3. **TLS Handshake:** Encrypts data transmission for HTTPS connection.
4. **HTTP Request:** Browser sends request (GET/POST) to the server IP.
5. **Server Response:** Server processes request and returns status code + data (HTML/JSON).
6. **Rendering:** Browser renders the webpage.

### Q: TCP vs. UDP?
* **TCP:** Reliable, ordered, connection-based. Guarantees delivery (used for web, file transfers, SSH).
* **UDP:** Ultra-fast, connectionless, no delivery guarantees (used for video calls, gaming, DNS queries).

### Q: Layer 4 vs. Layer 7 Load Balancing?
* **Layer 4 (Transport):** Routes traffic based purely on IP addresses and TCP/UDP ports without reading packet contents.
* **Layer 7 (Application):** Reads HTTP headers, cookies, and URL paths (`/api` vs `/static`) to make smart routing decisions.

### Common HTTP Status Codes
* `200 OK`: Success
* `301`: Permanent Redirect
* `400`: Bad Request (client syntax error)
* `401`: Unauthorized (not logged in)
* `403`: Forbidden (logged in, but no access permission)
* `404`: Not Found
* `500`: Internal Server Error (backend code crashed)

---

## 7. Terraform (Infrastructure as Code)

### Q: What is Terraform State (`.tfstate`) and why is it important?
* **Answer:** It is a mapping file that tracks real-world cloud resources created by your code. Terraform uses it to calculate changes, detect configuration drift, and know what to create or destroy.

### Q: `terraform plan` vs. `terraform apply`?
* **`terraform plan`:** A dry run / preview that shows what changes will happen without touching real cloud resources.
* **`terraform apply`:** Executes the actual creation, update, or deletion of cloud infrastructure.

### Q: How do you handle Remote State and State Locking in a team?
* **Answer:** Save the state file remotely in a centralized cloud bucket (**AWS S3** or **Azure Blob**). Use a key-value store (**AWS DynamoDB**) for state locking so two team members cannot run `apply` simultaneously and corrupt the state file.

### Q: What is Infrastructure Drift and how do you fix it?
* **Answer:** Drift happens when someone manually edits cloud resources via the web console instead of Terraform code. Run `terraform plan` to spot the diffs, then either update code or run `terraform apply` to overwrite manual changes back to code state.

---

## 8. Cloud Computing (AWS & Scaling)

### Q: EC2 vs. ECS vs. Lambda — When to use which?
* **EC2:** Virtual Machines (full OS control, good for legacy apps or custom setups).
* **ECS:** Managed Docker container orchestration (run containerized apps easily).
* **Lambda:** Serverless execution (run short, event-driven code without managing servers).

### Q: IAM Roles vs. IAM Policies?
* **IAM Policy:** A JSON document listing allowed or denied actions (e.g., "allow read access to S3").
* **IAM Role:** An identity attached to a service (like an EC2 instance) or user that temporarily adopts permissions listed in policies.

### Q: How do you structure a secure VPC architecture?
* **Public Subnet:** Internet-accessible resources like Load Balancers and NAT Gateways.
* **Private Subnet:** Database and application servers with **no direct internet access**.
* **NAT Gateway:** Allows private instances to send outgoing requests (e.g., package updates) while blocking incoming internet connections.

### Q: Horizontal vs. Vertical Scaling?
* **Vertical Scaling (Scale Up):** Adding more CPU/RAM to a single machine. Limited by hardware limits and requires downtime.
* **Horizontal Scaling (Scale Out):** Adding more server instances behind a load balancer. Preferred in cloud/DevOps for zero downtime and infinite scalability.

---

## 9. Kubernetes (Fundamentals)

### Q: Explain Pods, Deployments, and Services.
* **Pod:** The smallest unit in Kubernetes, wrapping one or more containers.
* **Deployment:** Manages Pod replicas, handles automated rolling updates, and self-healing.
* **Service:** Gives a stable IP address and DNS entry to route incoming traffic across dynamic Pods.

### Q: A Pod is stuck in `CrashLoopBackOff`. How do you troubleshoot?
1. `kubectl describe pod <pod_name>` — check event logs for resource limits or missing configs.
2. `kubectl logs <pod_name> --previous` — view application crash logs.
3. Check memory allocation (Out Of Memory / OOM).
4. Verify environment variables, ConfigMaps, and Secrets.

---

## 10. Incident Response & Monitoring

### Q: How do you set up Monitoring & Observability?
* **Metrics:** Use **Prometheus** to collect metrics (CPU, RAM, latency) and display them on **Grafana** dashboards.
* **Logs:** Centralized logging using **ELK Stack** (Elasticsearch, Logstash, Kibana) or **Loki**.
* **Alerts:** Triggers sent to Slack/PagerDuty when thresholds are breached.

### Q: Scenario: Production service breaks at 2 AM. Walk me through your response.
1. **Acknowledge:** Accept the alert to notify team you are on it.
2. **Assess:** Look at Grafana dashboards to identify what failed (Database, App, Network).
3. **Check Deployments:** See if a code release happened right before the incident.
4. **Mitigate:** If caused by a new release, **roll back immediately** to restore user service.
5. **Post-Mortem:** Investigate root cause after recovery and document preventive measures.

---

## 11. Scripting & Command Tasks

### Disk Usage Monitoring Script
```bash
#!/bin/bash
# Check if any disk partition exceeds 80% usage
df -H | grep -vE '^Filesystem|tmpfs|cdrom' | awk '{ print $5 " " $1 }' | while read output;
do
  usep=$(echo "$output" | awk '{ print $1}' | cut -d'%' -f1)
  partition=$(echo "$output" | awk '{ print $2 }')
  if [ "$usep" -ge 80 ]; then
    echo "Warning: Disk space on '$partition' is at$usep% on $(hostname) as of$(date)"
  fi
done
```

Add this in day 17 folder as interview prep question for the devops role

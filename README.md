# load-balancer

### 🔄 **Load Balancer in AWS (Elastic Load Balancing - ELB)**

#### ✅ **What is Load Balancer in AWS?**

A **Load Balancer** in AWS automatically distributes incoming traffic across multiple **EC2 instances**, **containers**, or **IP addresses** to ensure:

* High **availability**
* **Scalability**
* **Fault tolerance**

---

## 🚀 **Types of Load Balancers in AWS**

AWS offers **4 types** of Load Balancers under **Elastic Load Balancing (ELB)**:

| Type                                | Best for                  | Protocols        | Layer       |
| ----------------------------------- | ------------------------- | ---------------- | ----------- |
| **ALB** (Application Load Balancer) | HTTP/HTTPS traffic        | HTTP, HTTPS      | Layer 7     |
| **NLB** (Network Load Balancer)     | TCP/UDP, high performance | TCP, UDP         | Layer 4     |
| **CLB** (Classic Load Balancer)     | Legacy use                | HTTP, HTTPS, TCP | Layer 4 & 7 |
| **Gateway Load Balancer**           | 3rd party appliances      | All IP           | Layer 3/4   |

---

## 🛠️ **Step-by-Step: Set Up an Application Load Balancer (ALB)**

### ✅ Step 1: Create EC2 Instances

1. Launch **2 EC2 instances** (Amazon Linux or Ubuntu)
2. Install Apache/PHP or your app
3. Allow ports: **22 (SSH), 80 (HTTP)** in Security Group

```bash
sudo yum install httpd -y
sudo systemctl start httpd
echo "Server 1/2" | sudo tee /var/www/html/index.html
```

---

### ✅ Step 2: Create Target Group

1. Go to **EC2 Dashboard > Load Balancing > Target Groups**
2. Click **"Create target group"**
3. Type: `Instances`, Protocol: `HTTP`, Port: `80`
4. Register your EC2 instances
5. Health check path: `/index.html` (or default `/`)

---

### ✅ Step 3: Create Load Balancer

1. Go to **EC2 > Load Balancers**
2. Click **"Create Load Balancer" > Application Load Balancer**
3. Name it, choose **Internet-facing**
4. Listener: `HTTP` on port `80`
5. Select **at least 2 AZs** (Availability Zones)
6. Select the target group you created

---

### ✅ Step 4: Test Load Balancer

* Copy the **DNS name** from Load Balancer page
* Open in browser:

  ```
  http://your-load-balancer-name.elb.amazonaws.com
  ```
* It should show responses from EC2 instance 1 and 2 alternately.

---

## ⚙️ **Important Terms**

| Term             | Meaning                                                |
| ---------------- | ------------------------------------------------------ |
| **Listener**     | Checks for connection requests using protocol and port |
| **Target Group** | Group of EC2 instances or IPs behind the load balancer |
| **Health Check** | Ensures only healthy targets receive traffic           |

---

## 🎯 Use Cases

* Distribute traffic across **multiple servers**
* Auto scale EC2 instances with **Auto Scaling Group (ASG)**
* Handle **millions of requests/sec**


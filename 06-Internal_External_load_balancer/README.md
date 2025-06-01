# Task : Create a Internal and External Load Balancer

## Prerequisites :
Before starting, make sure:

- You have at least two VMs in the same VNet and Subnet (e.g., webvm1, webvm2 in Subnet-1).

- Both VMs are running Nginx or Apache web server on port 80.

- Network Security Group allows HTTP (port 80) and ICMP (optional).

# 🔷 Part A: Create External Load Balancer
### 1. Go to Azure Portal > Create a resource > Search “Load Balancer”
- Type: Public

- SKU: Standard

- Name: external-lb

- Region: Same as your VMs

- Frontend IP: Create new Public IP (e.g., external-lb-ip)

- Virtual Network: Select the one with webvm1 and webvm2

- Subnet: Use the one with the VMs

- Availability zone: Choose "No Zone" or based on your preference

Click Review + Create and then Create.

### 2. Configure Backend Pool
- Go to your Load Balancer > Backend pools > Add

- Name: webBackendPool

- VMs: Select both webvm1 and webvm2

- Target NIC: Select their NICs

- Target IP: Select their private IPs

### 3. Add Health Probe
- Go to Load Balancer > Health probes > Add

- Name: http-probe

- Protocol: HTTP

- Port: 80

- Path: /

- Interval: 5

- Unhealthy threshold: 2

### 4. Add Load Balancing Rule
- Go to Load Balancing rules > Add

- Name: http-rule

- IP Version: IPv4

- Frontend IP: external-lb-ip

- Protocol: TCP
 
- Port: 80

- Backend Port: 80

- Backend Pool: webBackendPool

- Health Probe: http-probe

Click Add.

### 5. Test External Load Balancer
- Copy the Public IP from Load Balancer frontend

- Open it in browser: http://<external-lb-ip>

- Refresh multiple times – you should see responses alternating from webvm1 and webvm2.

![6](screenshots/01.png)
![6](screenshots/02.png)
![6](screenshots/03.png)
![6](screenshots/04.png)
![6](screenshots/05.png)
![6](screenshots/06.png)
![6](screenshots/07.png)
![6](screenshots/08.png)
![6](screenshots/09.png)
![6](screenshots/10.png)
![6](screenshots/11.png)
![6](screenshots/12.png)
![6](screenshots/13.png)


# 🔶 Part B: Create Internal Load Balancer
### 1. Go to Azure Portal > Create a resource > Search “Load Balancer”
- Type: Internal

- SKU: Standard

- Name: internal-lb

- Frontend IP: New (e.g., internal-lb-ip)

- Set private IP: e.g., 10.0.1.100 (must match subnet range)

- VNet & Subnet: Same as webvm1 and webvm2

Click Review + Create and then Create.

### 2. Configure Backend Pool
(Same steps as External LB)

- Use same NICs or create new backend pool if needed.

### 3. Add Health Probe
(Same config: HTTP on port 80)

### 4. Add Load Balancing Rule
- Name: internal-rule

- Frontend IP: internal-lb-ip

- Port: 80

- Backend port: 80

- Backend pool: same

- Probe: http-probe

5. Test Internal Load Balancer
- SSH into webvm1 or webvm2Create a Internal and External Load Balancer

`curl http://10.0.1.100`

- You should see the Nginx page or Welcome from webvmX.

![6](screenshots/14.png)
![6](screenshots/15.png)
![6](screenshots/16.png)
![6](screenshots/17.png)
![6](screenshots/18.png)
![6](screenshots/19.png)
![6](screenshots/20.png)
![6](screenshots/21.png)
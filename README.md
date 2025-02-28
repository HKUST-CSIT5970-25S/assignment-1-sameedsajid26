[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/IAASVEAZ)
# CSIT5970 Assignment-1: EC2 Measurement (2 questions, 4 marks)

### Deadline: 11:59PM, Feb, 28, Friday

---

### Name: Sameed Sajid
### Student Id: 21135456
### Email: ssajid@connect.ust.hk

---

## Question 1: Measure the EC2 CPU and Memory performance

1. (1 mark) Report the name of measurement tool used in your measurements (you are free to choose *any* open source measurement software as long as it can measure CPU and memory performance). Please describe your configuration of the measurement tool, and explain why you set such a value for each parameter. Explain what the values obtained from measurement results represent (e.g., the value of your measurement result can be the execution time for a scientific computing task, a score given by the measurement tools or something else).

    > The tool used here is Phoronix test suite. We used the compression test for cpu performance, and an integer copy operation for memory performance as demonstrated in the lab. for cpu, the command used is phoronix-test-suite run pts/compress-7zip, for memory test, the command used is phoronix-test-suite run pts/ramspeed

2. (1 mark) Run your measurement tool on general purpose `t2.micro`, `t2.medium`, and `c5d.large` Linux instances, respectively, and find the performance differences among these instances. Launch all the instances in the **US East (N. Virginia)** region. Does the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource?

    In order to answer this question, you need to complete the following table by filling out blanks with the measurement results corresponding to each instance type.

    | Size        | CPU performance (MIPS) | Memory performance MB/s |
    | ----------- | --------------- | ------------------ |
    | `t2.micro` |        4264        |      11463.85       |
    | `t2.medium`  |       10252          |        19812.90   |
    | `c5d.large` |        7544         |           14066.90   |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI.

    We can see that the cpu speed increases from t2.micro to t2.medium, but decreases at c5d.large.This suggests cpu performance does not nessecarily increase with the number of vCPUs. We can see a similar trend for memory speed as well. 


## Question 2: Measure the EC2 Network performance

1. (1 mark) The metrics of network performance include **TCP bandwidth** and **round-trip time (RTT)**. Within the same region, what network performance is experienced between instances of the same type and different types? In order to answer this question, you need to complete the following table.

    | Type                      | TCP b/w (Gbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | `t3.medium` - `t3.medium` |     4.0           |    0.189      |
    | `m5.large` - `m5.large`   |     9.47           |    0.13    |
    | `c5n.large` - `c5n.large` |      4.96          |     0.183     |
    | `t3.medium` - `c5n.large` |       2.25         |    0.790     |
    | `m5.large` - `c5n.large`  |      4.96          |     0.173     |
    | `m5.large` - `t3.medium`  |       2.74         |      0.546    |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. Note: Use private IP address when using iPerf within the same region. You'll need iPerf for measuring TCP bandwidth and Ping for measuring Round-Trip time.

    We see that instances of the same type all have good bandwidth above 4.0 Gb/s. For different instance types, the bandwidth can decrease, this happened between c5n.large-t3.med, and also between m5.large-t3.medium . Good bandwidth generally corresponds to a lower RTT.

2. (1 mark) What about the network performance for instances deployed in different regions? In order to answer this question, you need to complete the following table.

    | Connection                | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | N. Virginia - Oregon      |       31.6        |   61.1 |
    | N. Virginia - N. Virginia |       4950        |   0.189  |
    | Oregon - Oregon           |     9370        |   0.261   |
 
    > Region: US East (N. Virginia), US West (Oregon). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. All instances are `c5.large`. Note: Use public IP address when using iPerf within the same region.

    We see that across different data centers, the bandwidth and RTT decrease significantly when in different regions as compared to within the same region.

# Load-Balancer

🌟Load Balancer:

Load balancer distribute workload and improve website and application performance.load balancer distribute incomming application traffic across multiple backend(target).load balancer also called as Frontend or reverse proxy.

![Screenshot 2024-02-28 193427](https://github.com/Pratikshinde55/Load-Balancer/assets/145910708/8373fe05-3fbf-46f1-9f39-cb58c1a2c5e0)


⭐Haproxy⭐:-

HAproxy is one of the product of load balancer, HAproxy is a high-performance, open source load balancer & reverse proxy for HTTP and TCP .

For Loadbalancer setup i launched 4 instances one instance make Load Balancer(Frontend),and remaining
three make backend for my case named as Backend-1 (ip-172-31-44-4) ,Backend-2 (ip-172-31-33-138),Backend-3(ip-172-31-40-19).

⚡Backend Configuration:

 on three Backend instances, configure following same set-up on each backend node:
 1.install httpd php software(Apache)


    # yum install httpd php -y

 2.DocumentRoot for "Apache server is /var/www/htmt" create here one code folder which for client.
   here put webpage named as index.php


    #vim index.php

code:-


     <pre>
     <?php

          print_r($_SERVER);

     ?>
     </pre>

 3.Start the httpd service

     #systemctl enable httpd --now

⚡Load Balancer configuration:-
  
1. Install HAproxy load balancer in frontend instance.


      # yum install haproxy -y

2.Registration of Backend to Load Balancer, HAproxy has config file "/etc/haproxy/haproxy.cfg" where add backend node and also add port no. which can helps to client to access application.
for this do follow setup:

   #vim /etc/haproxy/haproxy.cfg
  
 ADD this code in config file:

    //screnshot

Note: here we use Round Robin Algorithm that work as client will connect to web server through Load
balancer , 1st connect to web 1 then web 2 and next web 3 then again go to 1.
here also bind the port no. as 8080

3. Start HAproxy service

     #systemctl restart haproxy
     #systemctl start haproxy
     #systemctl status haproxy

4.check HAproxy config file is valid or not

    # haproxy -f haproxy.cfg -c



Now loadbalancer configuration is done 
 note :
    Load Balancer(Frontend) instance change Inbound rule allow all traffic Anywhere


Check Load balancer on browser:
    Public IP of LB + port no. (http://65.0.18.65:8080) 
    also on local command prompt -->>(curl http://65.0.18.65:8080)
  


    











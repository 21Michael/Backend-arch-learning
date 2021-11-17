# DDoS
**DDoS (Distributed Denial of Service - "распределенный отказ в обслуживании")** атаки 
относятся к так называемым виртуальным методам терроризма. Их цель – вывести из строя
сервер, подключенный к сети Интернет, путем посылки на него огромного количества запросов.
В результате либо сервер, либо канал связи, им используемый, становится перегруженным. 
Это приводит к неработоспособности находящихся на атакуемом сервере ресурсов, например,
веб-сервера, сервера электронной почты, облачного хранилища данных и т.п. При этом 
реальные пользователи «упавшего» сайта не могут получить к нему доступ — всё это влечет 
за собой финансовые убытки. 

![link](https://timeweb.com/media/default/0001/01/7e8f663a5268630a35716aaec9a5535d034d47fd.png)

## Types of DDoS attacks:
  - ### Application layer attacks: 
    **The goal** of these attacks is to exhaust the target’s resources to create a 
    denial-of-service.  
    --  
    **HTTP flood:** The attacks target the layer where web pages are generated on the server and 
    delivered in response to HTTP requests. A single HTTP request is computationally
    cheap to execute on the client side, but it can be expensive for the target server
    to respond to, as the server often loads multiple files and runs database queries
    in order to create a web page.
    ![link](https://www.cloudflare.com/img/learning/ddos/what-is-a-ddos-attack/http-flood-ddos-attack.png)
    
  - ### Protocol attacks:
    **The goal of the attack:**  
    Protocol attacks, also known as a state-exhaustion attacks, cause a service 
    disruption by over-consuming server resources and/or the resources of network 
    equipment like firewalls and load balancers.  
    --  
    Protocol attacks utilize weaknesses in layer 3 and layer 4 (TCP/UDP) of the protocol
    stack to render the target inaccessible.   
    --  
    **Example (SYN flood):**  
    The worker receives a request, goes and gets the package, and waits for confirmation
    before bringing the package out front. The worker then gets many more package 
    requests without confirmation until they can’t carry any more packages, become 
    overwhelmed, and requests start going unanswered.

    This attack exploits the TCP handshake — the sequence of communications by which
    two computers initiate a network connection — by sending a target a large number
    of TCP “Initial Connection Request” SYN packets with spoofed source IP addresses.
    ![link](https://cloudflare.com/img/learning/ddos/what-is-a-ddos-attack/syn-flood-ddos-attack.png)
    
  - ### Volumetric attacks:
    **The goal of the attack:**  
    This category of attacks attempts to create congestion by consuming all available 
    bandwidth between the target and the larger Internet. Large amounts of data are sent
    to a target by using a form of amplification or another means of creating massive 
    traffic, such as requests from a botnet.  
    --  
    **Example (DNS Amplification):**
    A DNS amplification is like if someone were to call a restaurant and say “I’ll have
    one of everything, please call me back and repeat my whole order,” where the 
    callback number actually belongs to the victim. With very little effort, a long 
    response is generated and sent to the victim.  
    By making a request to an open DNS server with a spoofed IP address (the IP address
    of the victim), the target IP address then receives a response from the server.
    ![link](https://cloudflare.com/img/learning/ddos/what-is-a-ddos-attack/ntp-amplification-botnet-ddos-attack.png)
    
## Preventing mechanisms:
  - **Anycast network diffusion:**  
    This mitigation approach uses an Anycast network to scatter the attack traffic 
    across a network of distributed servers to the point where the traffic is absorbed
    by the network.  
    ![link](https://www.cloudflare.com/img/learning/cdn/glossary/anycast/anycast-cdn.png)
    
    After other DDoS mitigation tools filter out some of the attack traffic, Anycast
    distributes the remaining attack traffic across multiple data centers, preventing 
    any one location from becoming overwhelmed with requests. If the capacity of the 
    Anycast network is greater than the attack traffic, the attack is effectively 
    mitigated.
    ![link](https://www.cloudflare.com/img/learning/cdn/glossary/anycast/anycast-unicast-botnet-attack.png)
  - **Rate limiting:**  
    Limiting the number of requests a server will accept over a certain time window is 
    also a way of mitigating denial-of-service attacks.

    While rate limiting is **useful in slowing web scrapers from stealing content and for
    mitigating brute force login attempts, it alone will likely be insufficient to 
    handle a complex DDoS attack effectively.**
    ![link](https://drive.google.com/uc?id=1aNApH158ymwOKBWs1_jt0sqezMHvYkQM)
    
  - **Web application firewall (WAF):**  
    A Web Application Firewall (WAF) is a tool that can assist in mitigating a layer 7
    DDoS attack. By putting a WAF between the Internet and an origin server, the WAF 
    may act as a reverse proxy, protecting the targeted server from certain types of
    malicious traffic.
    A WAF or web application firewall helps protect web applications by filtering 
    and monitoring HTTP traffic between a web application and the Internet.
    ![link](https://www.cloudflare.com/img/learning/ddos/glossary/waf/waf.png)

    By filtering requests based on a series of rules used to identify DDoS tools, 
    layer 7 attacks can be impeded. One key value of an effective WAF is the ability
    to quickly implement custom rules in response to an attack.   
    --  
    **WAF list:**  
    - **Blocklist**
    - **Allowlist**

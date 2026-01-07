2.) Need to include lead time from order to delivery = ~3 weeks, can't go lower than that as raspberry pi vendor also need 5-8 days, casing vendor would also need 8-10 days, and we would also need 5-6 days to test the final module before handover, even at a very efficient speed of 20 devices per day or roughly 15-20 mins per device. If feasible 1 month would be recommended. If we want it faster we can build up a supply chain such that we always have around 200 cases present in office as casing vendor has the most unreliable delivery and case is comparatively the cheapest part in the whole module so even having a few in buffer is not expensive for us. Raspberry Pi is a standard item with comparatively established supply chain so they'll have more predictable delivery patterns.

4.) Mention Azure consumption cost, if Draeger will host the API. Mention what needs to be done if Draeger wont host the APi but end customer would host (Each of the customers)
### **Draeger Hosted (Centralized SaaS Model)**

**PROS:**

- **Speed & Simplicity**: Quick deployment with minimal setup required
- **Maintenance-Free**: Draeger handles updates, security patches, and infrastructure
- **Scalability**: Automatic scaling to handle demand spikes
- **Reliability**: Professional-grade infrastructure with high uptime guarantees
- **Support**: Dedicated technical support and documentation
- **Security**: Enterprise-level security managed by experts
- **Time-to-Market**: Faster implementation and go-live

**CONS:**

- **Vendor Lock-in**: Dependency on provider's roadmap and pricing
- **Data Location**: Data resides on provider's servers (compliance concerns)
- **Ongoing Costs**: Recurring subscription fees that scale with usage
- **Shared Resources**: Performance may be affected by other customers

Cost
Compute : App Service P2mv3 - 4vCPU 32GB RAM ₹24,625.088/month
Database:  Azure SQL Database S2 ₹7,216.9878/month
Bandwidth: First 100 GB/Month is free then ₹10.2845 per GB

This is sufficient for about 10k devices since they're only pushing data at vehicle start and about 100-150 fleet management users/clients who are pulling the data.

---

### **Customer Self-Hosted (Distributed Model)**

**PROS:**

- **Full Control**: Complete customization and configuration flexibility
- **Data Sovereignty**: Data remains on customer's infrastructure
- **No Vendor Lock-in**: Freedom to modify or migrate solutions
- **Compliance**: Easier to meet specific regulatory requirements
- **Cost Predictability**: No recurring subscription fees after initial setup
- **Performance**: Dedicated resources for optimal performance
- **Integration**: Easier integration with existing internal systems

**CONS:**

- **Technical Expertise**: Requires skilled IT staff for deployment and maintenance
- **Maintenance Burden**: Customer responsible for updates, security, and monitoring
- **Scalability Challenges**: Manual scaling and capacity planning required
- **Security Risk**: Customer responsible for implementing security measures
- **Support Limitations**: Limited support compared to SaaS offerings
- **Time Investment**: Longer implementation and deployment cycles

Cost
Compute : App Service P0v3 - 1vCPU 4GB RAM ₹5,130.227/month
Database:  Azure SQL Database S0 ₹1,443.1369/month
Bandwidth: They'll probably never cross the free limit

This is sufficient for about 1k devices since they're only pushing data at vehicle start and about 4-5 fleet management users/clients who are pulling the data.


5.) Can offline date be retrieved from Raspberry Pi by directly connecting it with laptop/computer and what would be data format in that case? Can have a side on this one - steps and screenshots

The simplest way would be that we also add one ethernet cable in the module.
1. Connect the ethernet cable to the router
2. Install RealVNC Viewer on laptop where we want to read the data
3. Have the laptop connect to the same network
4. Enter the credentials provided by us for the raspberry Pi
5. This will open a connection similar to RDP where you can browse the Raspberry Pi
6. Open the DB Viewer application (pre-installed by us during setup)
7. View all data present which is not yet synced



Bandwidth Comsumption
Assuming 100 client pulling 100 rows per page, viewing 50 pages of data per session, each having 10 such sessions every day for 365 days where each row is less than 2KB of data
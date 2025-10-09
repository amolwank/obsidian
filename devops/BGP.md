## **BGP (Border Gateway Protocol) - Short Answer**

**BGP** is the **routing protocol of the Internet** that connects different autonomous systems ([[ASNs]]) together. It's how [[ISPs]] and large networks exchange routing information and determine the best paths for traffic across the global internet.

---

### **Key Points:**

**What it does:**

- Exchanges routing information between autonomous systems
    
- Makes routing decisions based on policies, not just shortest path
    
- Maintains the global Internet routing table
    

**How it works:**

- Uses **TCP port 179** for reliable communication
    
- **Path Vector protocol** - selects routes based on AS path, policies, and attributes
    
- **Incremental updates** - only sends changes, not entire routing tables
    

**Key Concepts:**

- **ASN (Autonomous System Number)**: Unique ID for each network (e.g., AWS AS16509)
    
- **Route Advertisement**: Announcing IP prefixes to neighbors
    
- **Path Selection**: Choosing best route based on attributes
    
- **Peering**: BGP sessions between routers
    

**Why it matters:**

- Without BGP, the Internet wouldn't work as a connected global network
    
- Enables **anycast** (same IP from multiple locations)
    
- Provides **policy-based routing** and traffic engineering
    

**Real-world analogy:** BGP is like the **GPS for Internet traffic** - it figures out how to get your data from one network to another across the global Internet.
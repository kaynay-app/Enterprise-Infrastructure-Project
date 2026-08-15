---

## ⚖️ Kemp Load Balancing & IIS Web Server HA

- **KLM-KempLB01** provides Layer 7 load balancing for the IIS web-server tier.
- A custom virtual service was configured to provide a single frontend endpoint for the web application.
- HTTP and HTTPS virtual services distribute incoming requests across:
  - `KLM-WEB01`
  - `KLM-WEB02`
- The HTTPS virtual service uses the `portal.king.klm` certificate.
- Backend health monitoring allows the LoadMaster to determine whether each IIS server is available to receive traffic.
- If one IIS server becomes unavailable, traffic can continue through the remaining healthy server, providing **basic application-level high availability**.
- The design allows additional IIS servers to be added to the backend pool as the environment grows.
- Internal VIP and backend IP addresses are intentionally omitted from this public documentation.

### Traffic Flow

```text
                    +-------------------------+
                    |     KLM-KempLB01        |
                    |      Kemp LoadMaster    |
                    |                         |
                    |  Layer 7 Virtual        |
                    |  Services               |
                    |  HTTP / HTTPS           |
                    +------------+------------+
                                 |
                    +------------+------------+
                    |                         |
                    v                         v
             +-------------+           +-------------+
             | KLM-WEB01   |           | KLM-WEB02   |
             | IIS Web     |           | IIS Web     |
             | Server      |           | Server      |
             +-------------+           +-------------+
                    |                         |
                    +------------+------------+
                                 |
                         Web Application

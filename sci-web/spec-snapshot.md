# Software Carbon Intensity for Web Specification (DRAFT SNAPSHOT)

## 1\. Introduction

This specification extends the Software Carbon Intensity (SCI) methodology to the unique characteristics of web applications. It provides a standardized method for measuring and reporting the carbon emissions associated with software systems that deliver functional value to human users primarily through browser-based interfaces accessed via HTTP/HTTPS protocols.

Web applications consume energy across a distributed system encompassing servers, networks, content delivery systems, third-party services, and end-user devices. Unlike monolithic server-side software, where energy consumption is concentrated in datacenter infrastructure, web applications distribute computation and rendering across infrastructure that no single party fully controls. This specification addresses that distributed reality.

The SCI for Web specification builds upon the core principles established in ISO/IEC 21031:2024 while adding considerations specific to web applications, including their distributed architecture, client-side execution model, dependency on third-party services, and the diversity of end-user devices and network conditions.

This specification aims to:

- Provide a consistent framework for measuring the carbon footprint of web applications across servers, networks, client devices, and third-party services  
- Enable meaningful comparison between different web application implementations and architectures  
- Guide practitioners in making environmentally responsible decisions in web application design, development, and operation  
- Incentivize carbon efficiency improvements that represent genuine emission reductions rather than displacement or gaming  
- Create market pressure for third-party service providers and hosting suppliers to disclose and reduce their carbon impact

Like the parent SCI specification, SCI for Web is a rate rather than a total: carbon emissions per functional unit. Lower scores indicate better efficiency. Reaching zero is impossible, but continuous improvement is always possible. Reducing an SCI for Web score requires actual elimination of emissions through more efficient code, more efficient infrastructure, or lower-carbon energy sources. Market-based measures such as carbon offsets and renewable energy certificates do not reduce SCI for Web scores.

This specification recognizes that web applications exist across a spectrum of complexity and organizational capability. It provides progressive implementation tiers that enable teams to start measuring with readily available tools and industry defaults, then advance to more sophisticated measurement as capability grows. All tiers are legitimate when methodology is transparently disclosed.

## 2\. Scope

This specification covers the full spectrum of browser-based web applications, defined by three essential criteria:

1. **Delivery mechanism**: Content and functionality delivered over HTTP/HTTPS protocols  
2. **Execution environment**: Rendering and execution occurring primarily within web browser environments or equivalent web rendering engines  
3. **Interaction pattern**: Interfaces designed for direct human interaction and consumption rather than exclusively machine-to-machine communication

### 2.1 Application Types In Scope

- Static content websites (blogs, documentation, marketing pages)  
- Dynamic web platforms (content management systems, portals)  
- Single-page applications (SPAs)  
- Progressive web applications (PWAs)  
- Server-side rendered applications  
- E-commerce systems  
- Media streaming services delivered via browser  
- Software-as-a-Service (SaaS) platforms  
- Real-time collaborative tools (document editors, whiteboards, messaging)  
- API-driven applications with browser-based interfaces

### 2.2 Boundary Cases

API-driven services require classification based on their primary access pattern:

- **In scope**: APIs accessed primarily through browser-based interfaces, such as those with interactive documentation as the primary usage method, or APIs coupled with browser-based management dashboards, where the browser interface represents the primary human interaction mode  
- **Out of scope**: Pure machine-to-machine APIs serving only programmatic clients; these should use the parent SCI methodology directly

The determining factor is whether human users consume the service's value through browser rendering, not whether HTTP protocols are involved.

### 2.3 Architectural Patterns In Scope

- Client-side rendering (CSR)  
- Server-side rendering (SSR)  
- Static site generation (SSG)  
- Hybrid and incremental rendering (ISR)  
- Serverless and edge computing architectures  
- Micro-frontend architectures

## 3\. Normative References

The following documents are referred to in the text in such a way that some or all of their content constitutes requirements of this document:

- ISO/IEC 21031:2024 \-- Information technology \-- Software Carbon Intensity (SCI) specification

## 4\. Terms and Definitions

For the purposes of this document, the terms and definitions given in ISO/IEC 21031:2024 and the following apply.

ISO and IEC maintain terminological databases for use in standardization at the following addresses:

- ISO Online browsing platform: available at [https://www.iso.org/obp](https://www.iso.org/obp)  
- IEC Electropedia: available at [http://www.electropedia.org/](http://www.electropedia.org/)

T.1 **Web Application** Software system that delivers functional value to human users primarily through browser-based interfaces accessed via HTTP/HTTPS protocols, characterized by browser-mediated human interaction

T.2 **Client-Side Energy** Energy consumed by end-user devices (desktops, laptops, tablets, smartphones) during browser rendering, JavaScript execution, and interaction with web application interfaces

T.3 **Server-Side Energy** Energy consumed by origin servers, application servers, database servers, and other backend infrastructure that generates and delivers web application responses

T.4 **Network Transfer Energy** Energy consumed by network infrastructure in transmitting data between servers and end-user devices, including core internet infrastructure, content delivery networks, and last-mile network access

T.5 **Third-Party Service** External service integrated into a web application that is not under direct operational control of the web application provider, including but not limited to: analytics services, advertising networks, authentication providers, payment processors, content delivery networks, and API services

T.6 **Operational Serving** The runtime operation of a web application serving end-user requests, excluding development, testing, and build infrastructure

T.7 **Functional Unit (Web-Specific)** The unit by which a web application's usage scales, measuring delivered functionality such as user sessions, transactions completed, content items consumed, or tasks performed

T.8 **Implementation Tier** The level of measurement sophistication adopted by an organization, ranging from entry-level automated measurement to advanced comprehensive instrumentation

T.9 **Reference Device** A representative end-user device used for standardized client-side energy measurement, selected from defined device categories and performance tiers

T.10 **Energy Displacement** The practice of shifting computation from measured locations to unmeasured locations to improve metrics without reducing total system energy consumption

The following abbreviations are used throughout this specification in addition to those defined in the parent specification:

- **O\_server** \-- Operational emissions from server-side infrastructure (within datacenter boundary)  
- **O\_network** \-- Operational emissions from network transfer (datacenter egress to client device NIC). OPTIONAL component; see §8.3.  
- **O\_client** \-- Operational emissions from client-side execution (on end-user devices)  
- **M\_server** \-- Embodied emissions from server-side hardware and datacenter infrastructure  
- **M\_network** \-- Embodied emissions from network infrastructure (routers, cell towers, cables, exchange points)  
- **M\_client** \-- Embodied emissions from end-user devices  
- **O\_dev** \-- Operational emissions from development lifecycle (optional; see §6.7)  
- **PUE** \-- Power Usage Effectiveness (datacenter efficiency metric)

Note: O\_thirdparty is not a top-level component. Third-party operational emissions are attributed within O\_server, O\_network, and O\_client based on where execution occurs, with mandatory first-party / third-party sub-dimension disclosure per component (see §6.3.1).

## 5\. Web Application Architecture Components

For the purpose of measuring carbon emissions, a web application system is decomposed into the following components, each contributing to either operational or embodied emissions:

### 5.1 Server-Side Infrastructure

Server-side infrastructure encompasses all backend systems that generate, process, and deliver web application responses. This includes:

- **Origin and application servers**: Systems executing server-side application logic  
- **Database and storage systems**: Relational databases, NoSQL stores, object storage, caching layers  
- **Edge and CDN infrastructure**: Content delivery network nodes, edge computing functions, edge caches  
- **Supporting services**: Load balancers, reverse proxies, API gateways, service mesh, monitoring systems  
- **Serverless execution environments**: Function-as-a-Service platforms, edge function runtimes

### 5.2 Network Transfer

Network transfer encompasses all data transmission between server infrastructure and end-user devices:

- **Core internet infrastructure**: Backbone and transit networks  
- **CDN and edge networks**: Content delivery and distribution networks  
- **Last-mile access**: ISP networks, WiFi, mobile/cellular networks

### 5.3 Client-Side Execution

Client-side execution encompasses all computation occurring on end-user devices:

- **Browser rendering**: Layout, paint, and composite operations  
- **JavaScript execution**: Parsing, compilation, and runtime execution  
- **Asset processing**: Image decoding, video playback, font rendering, CSS processing  
- **Interaction processing**: Event handling, animation, real-time updates  
- **Service Workers**: Background processing, caching, offline functionality

### 5.4 Third-Party Services

Third-party services encompass external services integrated into the web application:

- **Analytics and monitoring**: Usage tracking, error reporting, performance monitoring  
- **Advertising networks**: Ad serving, targeting, tracking  
- **Authentication and identity**: Login, SSO, identity verification  
- **Payment processing**: Transaction processing, fraud detection  
- **External APIs**: Data services, AI/ML services, communication services  
- **Client-side scripts**: Tag managers, chat widgets, social media embeds

Note: Third-party services are not a separate top-level component in the SCI for Web formula. Their energy consumption is attributed within O\_server, O\_network, or O\_client based on where execution occurs, with a mandatory first-party / third-party sub-dimension per component (see §6.3.1).

### 5.5 End-User Devices

End-user devices encompass the hardware on which browsers render and execute web applications:

- **Desktop computers**: Workstations, all-in-one systems  
- **Laptop computers**: Including Chromebooks and similar  
- **Smartphones**: All mobile phones with web browsers  
- **Tablets**: Including hybrid devices

## 6\. Persona-Based Software Boundary Definition

The SCI for Web specification defines measurement responsibilities based on three primary persona groups, each with different spheres of control and agency over the web application's carbon footprint. These personas align with the parent SCI specification's principle that teams should be accountable for elements they can reasonably control or influence.

### 6.1 Frontend Developer Boundary

The Frontend Developer boundary encompasses components where frontend developers and design practitioners have direct control over energy consumption:

- Client-side code efficiency (JavaScript bundle size, execution time)  
- Asset delivery and optimization (images, fonts, videos, CSS)  
- Rendering strategies (progressive enhancement, code splitting, lazy loading)  
- Third-party client-side dependencies (analytics scripts, advertising trackers, external fonts)  
- User interaction patterns (infinite scroll vs. pagination, auto-playing media)  
- Browser caching strategies (service workers, cache headers)

**What this boundary measures**: O\_client (including third-party sub-dimension for client-side scripts the frontend developer chose to include), contribution to O\_network (data transferred to client)

**What this boundary excludes**: Server-side infrastructure decisions, database architecture, hosting provider selection, network infrastructure between datacenter and user, end-user device hardware specifications

### 6.2 Backend and Infrastructure Engineer Boundary

The Backend and Infrastructure Engineer boundary encompasses components where backend developers, infrastructure engineers, and DevOps practitioners have direct control:

- Server-side compute and storage resources  
- Database efficiency and architecture  
- Geographic hosting location and carbon intensity exposure  
- Infrastructure capacity relative to actual traffic (right-sizing)  
- Caching at server and CDN levels  
- API efficiency and server-side code performance

**What this boundary measures**: O\_server (including third-party sub-dimension for server-side API dependencies), M\_server, contribution to O\_network (server-side network configuration)

**What this boundary excludes**: End-user device choices, browser vendor implementations, client-side third-party script behavior (though controls whether to include them)

### 6.3 Product Owner and Technical Manager Boundary

The Product Owner and Technical Manager boundary encompasses strategic and architectural decisions:

- Feature prioritization and lifecycle management ("feature gardening")  
- Performance and environmental budget setting  
- Vendor selection and third-party service decisions  
- Team time allocation for optimization  
- Architectural standards and patterns  
- Non-functional requirements including sustainability targets

**What this boundary influences**: All components (O\_server, O\_network, O\_client, M\_server, M\_network, M\_client) through architectural decisions and prioritization, including third-party service selection whose emissions appear as sub-dimensions within the appropriate operational component (see §6.3.1)

**What this boundary excludes**: Day-to-day implementation details, supplier internal implementations, end-user behavior and device choices

### 6.3.1 First-Party vs Third-Party Attribution

Client-side energy consumption includes all execution on the end-user device, regardless of script origin. This includes first-party application code (the organization's own JavaScript, WASM, rendering logic), third-party scripts executing in the browser (analytics, advertising, chat widgets, embedded media), and hybrid execution (first-party code invoking third-party libraries).

Energy is attributed to the decision maker who introduced the dependency, not the legal entity providing the code:

- Frontend developer includes analytics widget → O\_client (third-party sub-dimension)  
- Backend developer integrates payment API → O\_server (third-party sub-dimension)  
- Infrastructure team selects CDN provider → O\_network (third-party sub-dimension)  
- User installs browser extension → Not attributed to the web application

Client-side third-party execution is measurable using Long Task API for JavaScript execution time by origin, Resource Timing API for third-party asset loading, JavaScript profiling in browser DevTools, and Real User Monitoring (RUM) tools with script attribution. Where direct attribution is impractical, organizations may estimate using script bundle sizes with disclosed estimation methodology.

O\_client MUST be reported with first-party / third-party breakdown:

- O\_client\_first: Energy from the organization's own client-side code  
- O\_client\_third: Energy from third-party scripts executing in the browser  
- Total: O\_client = O\_client\_first + O\_client\_third

Organizations unable to separate first-party and third-party client execution MUST disclose this limitation and report blended O\_client with "attribution: undifferentiated."

The same first-party / third-party sub-dimension applies to O\_server and O\_network, disclosed even if one side is zero or not separately measurable.

### 6.4 Consolidated Software Boundary

While persona boundaries define responsibility and agency, the SCI for Web score is calculated across the **consolidated software boundary** encompassing all components:

**Mandatory inclusions**:

- Server-side infrastructure (origin servers, databases, caching, serverless functions, edge nodes, load balancers, API gateways)  
- Network transfer (all data transmitted between server infrastructure and end-user devices across all network segments)  
- Client-side execution (browser rendering, JavaScript execution, asset processing on end-user devices)  
- End-user devices (embodied emissions allocated proportionally to web application usage)  
- Third-party services (external services providing integral functionality)

**Optional inclusions with disclosure**:

- Content Delivery Networks operated or contracted by the web application provider  
- Monitoring and observability infrastructure (if significantly contributing to energy consumption)  
- Redundancy and failover systems (idle failover infrastructure)

**Explicit exclusions**:

- Development and build infrastructure (developer workstations, CI/CD pipelines, build processes, automated testing, staging environments) \-- to avoid perverse incentives discouraging essential development practices  
- Post-delivery artifacts (email delivery after send, file downloads after transfer, offline processing triggered independently)  
- Native mobile applications (even those using WebViews)  
- Browser extensions, plugins, or assistive technologies

*Rationale for development exclusion*: Measuring development infrastructure within SCI for Web would create perverse incentives to reduce testing, security scanning, and quality assurance. Development lifecycle energy may be measured separately using the parent SCI methodology.

### 6.7 Development Lifecycle Operational Emissions (O\_dev) — Optional

O\_dev captures operational energy consumed during software development activities: CI/CD pipelines, build processes, automated testing, development environment operation, and version control infrastructure.

O\_dev is not required for baseline SCI for Web compliance but is explicitly recognized as a valid supplementary component for organizations seeking comprehensive lifecycle accounting. Including O\_dev acknowledges that development is the lifecycle stage where teams have direct measurement control, that pre-deployment energy is attributable to specific software artifacts, and that optimization incentives exist (faster builds, efficient CI/CD, targeted testing).

Organizations including O\_dev should define clear boundaries (e.g., from commit to deployment artifact creation), allocate development energy to deployed features proportionally (e.g., by time-to-market or feature complexity), declare measurement methodology and tooling used, and report O\_dev separately from the six mandatory components to maintain comparability.

When including O\_dev, organizations must define how development energy amortizes over the functional unit. Example approaches include allocating evenly across all instances of R during a deployment period, weighting by feature usage if development was feature-specific, or amortizing over expected feature lifetime.

## 7\. Functional Units

### 7.1 General Guidance

The functional unit (R) for a web application SHALL describe how the application scales and delivers value to users. Following the parent specification, R SHALL be consistent across all components in the software boundary.

For web applications, functional units SHALL measure **delivered functionality** rather than **technical operations**. This prevents gaming through quality degradation and ensures SCI scores reflect efficiency of value delivery.

Web applications MAY define **multiple functional units** representing distinct value-delivery pathways. Complex applications SHOULD define multiple FUs when the application serves distinctly different user journeys or when features have substantially different resource intensities. Each functional unit has its own SCI score. There is no requirement to reduce complex applications to a single headline number.

Comparability across functional units operates at two levels: per-FU comparability (e.g., "purchase completed" SCI is comparable across e-commerce sites) and maturity comparability (organizations tracking more sophisticated FUs demonstrate deeper SCI integration). Comparability weakens as functional units become more application-specific; this is expected and acceptable.

### 7.2 Recommended Functional Units by Application Type

The table below provides suggested examples of commonly used functional units. Given the diversity of web application types and usage models, these examples are indicative and not exhaustive.

| Web Application Type | Suggested Functional Unit | Rationale |
| :---- | :---- | :---- |
| Content and media websites | Content item consumed (article read, video watched) | Captures delivered value; resistant to page-splitting gaming |
| E-commerce platforms | Completed transaction | Aligns with business value delivery; scales with actual usage |
| SaaS applications | Task completion (document created, report generated) | Measures delivered functionality, not login frequency |
| Collaboration tools | Active collaboration session or user-hour | Captures sustained engagement and value delivery |
| API-driven applications with browser UI | User workflow completed | Measures end-to-end value, not individual API calls |
| Marketing and informational websites | User session (with engagement threshold) | Appropriate for content consumption patterns |
| Real-time applications | Active user-minute | Captures ongoing resource consumption proportionally |

### 7.3 Functional Unit Selection Criteria

When selecting a functional unit, organizations SHALL consider:

1. **Scaling relationship**: The functional unit SHOULD scale proportionally with resource consumption  
2. **User value alignment**: The functional unit SHOULD represent delivered value, not technical implementation details  
3. **Measurability**: The functional unit SHALL be objectively measurable from analytics or instrumentation  
4. **Stability**: The functional unit definition SHOULD remain stable over time to enable comparison  
5. **Gaming resistance**: The functional unit SHOULD NOT incentivize reducing functionality or quality

### 7.4 Discouraged Functional Units

The following functional units SHOULD generally be avoided:

- **Raw page views**: Does not account for page complexity or user value delivered  
- **API calls**: Technical metric easily gamed by consolidating or splitting calls  
- **Data transferred**: Incentivizes reducing content quality rather than improving efficiency  
- **Server requests**: Backend technical metric disconnected from user value

Exceptions may exist when these metrics genuinely represent delivered value. If used, justification SHALL be disclosed.

### 7.5 Reporting Expectations

Organizations SHALL clearly state:

- The chosen functional unit and the rationale behind its selection  
- How the functional unit is measured (analytics instrumentation, server logs, etc.)  
- Any engagement thresholds applied (e.g., minimum session duration for "user session")  
- How the functional unit relates to the application's primary value delivery

### 7.6 Bot Traffic and Non-Human Access

Bot traffic and non-human access SHALL be handled based on detection capability:

- **Preferred approach**: Separate functional units for human and non-human traffic (e.g., R\_human for "human page view", R\_bot for "bot page view" or "automated API access"), each with its own SCI score  
- **Combined reporting**: Acceptable when reliable human/non-human separation is not feasible; reported as combined FU with disclosure of detection limitations and estimated bot proportion  
- **Exclusion**: Permitted only with reliable detection, justification (e.g., malicious bot traffic), and disclosure of exclusion methodology

Organizations MUST disclose: whether bot traffic is included, excluded, or reported separately; what detection method was used; and estimated bot proportion of total traffic. Neither inclusion nor exclusion of bot traffic is inherently correct — comparability comes from transparency.

Engagement thresholds (e.g., minimum 30-second session duration, at least one interaction event) are set by the organization and disclosed. No universal session threshold is mandated, as legitimate session shapes vary too widely across application types. Examples given in this specification are illustrative only and SHOULD NOT be treated as informal defaults — organizations SHALL select thresholds that reflect their actual user-behaviour patterns (a 30-second minimum is inappropriate for marketing or content-discovery sites with legitimately short sessions, for example).

## 8\. Methodology

### 8.1 General Formula

SCI for Web extends the parent specification formula to explicitly decompose web-specific operational and embodied components:

`SCI = (O + M) per R`

Where for web applications, O is decomposed as:

`O = O_server + O_client  [+ O_network, optional — see §8.3]`

And M is decomposed as:

`M = M_server + M_network + M_client`

Therefore, the mandatory SCI for Web formula is:

`SCI = (O_server + O_client + M_server + M_network + M_client) per R`

Organizations MAY additionally include O\_network when a defensible methodology is available (see §8.3). When included, the reported SCI score becomes:

`SCI (with O_network) = (O_server + O_network + O_client + M_server + M_network + M_client) per R`

Where:

- `O_server` \= Operational emissions from server-side infrastructure (within datacenter boundary)  
- `O_network` \= Operational emissions from network transfer (datacenter egress to client device NIC). OPTIONAL — see §8.3 for rationale and methodology requirements.  
- `O_client` \= Operational emissions from client-side execution on end-user devices (including third-party scripts; see §6.3.1)  
- `M_server` \= Embodied emissions from server-side hardware  
- `M_network` \= Embodied emissions from network infrastructure (see §8.8)  
- `M_client` \= Embodied emissions from end-user device hardware  
- `R` \= Functional unit measuring delivered value

**Why O\_network is optional**: Operational network emissions are currently difficult to measure defensibly. Widely-used estimation approaches based on bytes-transferred (e.g., SWDM) are acknowledged proxies that can produce misleading results by incentivising apparent efficiency improvements (compression, smaller assets) that do not correspond to reductions in actual network energy use. Rather than mandate a known-weak methodology that could discredit SCI for Web scores, this specification requires reporting without O\_network as the baseline, and permits O\_network inclusion as a supplementary disclosure when methodology supports it. Embodied network emissions (M\_network) remain mandatory because they are structurally present regardless of traffic patterns.

Organizations SHALL disclose whether O\_network was included or omitted from their reported SCI for Web score, and if included, the methodology used (see §8.3 and §12.1).

Third-party operational emissions are attributed within O\_server and O\_client (and within O\_network where reported) based on where execution occurs, with mandatory first-party / third-party sub-dimension disclosure (see §6.3.1).

Organizations MAY additionally report O\_dev (development lifecycle emissions) as a supplementary component (see §6.7). When reported, O\_dev is disclosed separately and does not alter the mandatory formula above.

Each operational component follows the pattern `O = E * I` from the parent specification, where E is energy consumed in kWh and I is location-based carbon intensity in gCO2eq/kWh.

### 8.2 Server-Side Operational Emissions (O\_server)

`O_server = E_server * I_server`

Where:

- `E_server` \= Energy consumed by all server-side infrastructure per functional unit (kWh)  
- `I_server` \= Carbon intensity of electricity consumed by server infrastructure (gCO2eq/kWh)

**Energy (E\_server)** includes energy consumed by:

- Origin servers and application servers  
- Database servers and caching infrastructure  
- Serverless function execution environments  
- Edge computing nodes (CDN edge servers, edge functions)  
- Supporting infrastructure (load balancers, firewalls, monitoring systems)

Energy consumption SHALL include all energy consumed by hardware reserved or provisioned for the web application, including idle resources, following the parent specification guidance.

If servers are located in datacenters, energy measurements SHALL account for datacenter efficiency by incorporating Power Usage Effectiveness (PUE):

`E_server = E_compute * PUE`

For multi-tenant infrastructure (shared hosting, cloud computing), energy SHALL be attributed based on resource allocation (vCPUs, memory, storage) proportional to total capacity.

For geographically distributed server infrastructure:

`E_server = SUM(E_region_i)` for all regions i

**Carbon Intensity (I\_server)**: For geographically distributed systems, carbon intensity SHALL be calculated as an energy-weighted average:

`I_server = SUM(E_region_i * I_region_i) / SUM(E_region_i)`

Carbon intensity values SHALL use location-based grid carbon intensity, excluding any market-based measures per the parent specification.

### 8.3 Network Transfer Operational Emissions (O\_network)

**Status**: O\_network is an OPTIONAL component of the SCI for Web score. The mandatory formula (see §8.1) excludes O\_network. Organizations MAY additionally report O\_network as a supplementary disclosure when a defensible methodology is available.

**Why optional**: Operational network emissions are currently difficult to measure defensibly. The most widely-used estimation approaches allocate energy based on bytes transferred, which is an acknowledged-weak proxy for actual network energy consumption. Including a mandatory component whose methodology is known to produce misleading results risks discrediting the overall SCI for Web score. This specification therefore separates the reliably-measurable components (O\_server, O\_client, M\_server, M\_network, M\_client) from the harder-to-measure O\_network, and permits but does not require the latter.

**If reported**, O\_network is calculated as:

`O_network = E_network * I_network`

Where:

- `E_network` \= Energy consumed by network infrastructure to transfer data per functional unit (kWh)  
- `I_network` \= Carbon intensity of electricity consumed by network infrastructure (gCO2eq/kWh)

**Methodology hierarchy (when O\_network is reported)**:

Organizations SHALL use the most direct method available and SHALL NOT use bytes-transferred as the sole basis of calculation except as a last-resort fallback with explicit disclosure.

**Preferred — Direct Measurement**: Where instrumentation is available (e.g., ISP or CDN partner supplying measured energy data for the traffic attributable to the application), direct measurement SHALL be used.

**Acceptable — Hybrid Model**: A calculation combining measured or vendor-disclosed network segment data (e.g., last-mile operator energy reports) with modelled remainder. Organizations using this approach SHALL disclose which segments are measured versus modelled, and the rationale for any modelling coefficients.

**Fallback — Data-Transfer Estimation**: Bytes-transferred proxies (e.g., SWDM, CO2.js coefficients) MAY be used only when no measurement or hybrid approach is available. Organizations using this fallback SHALL disclose: (a) the model and coefficients used, (b) that bytes-transferred is an acknowledged-weak proxy for network energy, (c) why more direct methods were not available, and (d) that the reported O\_network value carries high methodological uncertainty.

**Data transfer measurement** (when used) SHALL include all bytes transferred between server infrastructure and end-user devices, including HTML, CSS, JavaScript, images, videos, fonts, API responses and request bodies, WebSocket and real-time protocols, and HTTP headers and protocol overhead. Data SHALL be measured at the application layer after compression.

**Gaming guard**: Organizations using bytes-transferred fallback methods SHOULD NOT report reductions in O\_network as the primary narrative for efficiency improvements, because bytes-reduction can occur without corresponding network energy reduction (e.g., edge caching shifts energy rather than eliminating it). This aligns with the parent SCI specification's principle that SCI reductions must reflect actual emission reductions, not accounting shifts.

**Preventing Double-Counting with CDN and Edge Services**:

The boundary between O\_server and O\_network occurs at datacenter facility egress. CDN and edge services energy is attributed based on measurement regime, not service type:

1. If measured as facility energy (edge datacenter with PUE, metered infrastructure): include in O\_server  
2. If measured as transmission energy (traffic-based, SWDM-style allocation): include in O\_network  
3. If bundled by provider without clear separation: organizations MUST disclose which component received the allocation and why

When a provider supplies bundled energy figures, practitioners MUST document which SCI components received portions of the bundled figure, what allocation rationale was used, and what assumptions about measurement regime justified the split.

**Connection-Type Weighting**: Mobile radio access networks consume roughly an order of magnitude more energy per bit than fiber connections. SWDM default coefficients provide blended averages. Entry Tier organizations may use default SWDM coefficients. Standard and Advanced Tier organizations SHOULD apply connection-type weighting when user traffic distribution is known. Connection-type weighting is encouraged but not mandatory; disclosure of whether weighting was applied is mandatory.

**SWDM Double-Counting Rule**: When using SWDM, use ONLY the network segment for O\_network. Discard SWDM's datacenter and device allocations, replacing them with direct measurement for O\_server and O\_client. SWDM allocates a single system energy total across three segments; taking network from SWDM and server/client from direct measurement avoids summing overlapping allocations. Organizations using SWDM for O\_network MUST disclose the SWDM version and coefficients used, whether connection-type weighting was applied, how edge facility energy was handled, and known limitations.

**Preventing Double-Counting with CDN and Edge Services**:

The boundary between O\_server and O\_network occurs at datacenter facility egress. CDN and edge services energy is attributed based on measurement regime, not service type:

1. If measured as facility energy (edge datacenter with PUE, metered infrastructure): include in O\_server  
2. If measured as transmission energy (traffic-based, SWDM-style allocation): include in O\_network  
3. If bundled by provider without clear separation: organizations MUST disclose which component received the allocation and why

When a provider supplies bundled energy figures, practitioners MUST document which SCI components received portions of the bundled figure, what allocation rationale was used, and what assumptions about measurement regime justified the split.

*Illustrative bundled-allocation example (non-normative)*: A CDN provider publishes a single "CDN total energy for your traffic = 42 kWh/month" figure. An application that uses the CDN for static asset delivery and edge functions may allocate this using a cache-hit-ratio split: if 70% of requests are cache hits served without origin compute, attribute 70% of the 42 kWh to O\_network (transmission) and 30% to O\_server (edge compute). The operator discloses: the allocation rule, the ratio sources (CDN analytics), and a note that if the CDN publishes component-specific figures in future, the allocation will switch to those.

**Connection-Type Weighting**: Mobile radio access networks consume roughly an order of magnitude more energy per bit than fiber connections. SWDM default coefficients provide blended averages. Entry Tier organizations may use default SWDM coefficients. Standard and Advanced Tier organizations SHOULD apply connection-type weighting when user traffic distribution is known. Connection-type weighting is encouraged but not mandatory; disclosure of whether weighting was applied is mandatory.

**SWDM Double-Counting Rule**: When using SWDM, use ONLY the network segment for O\_network. Discard SWDM's datacenter and device allocations, replacing them with direct measurement for O\_server and O\_client. SWDM allocates a single system energy total across three segments; taking network from SWDM and server/client from direct measurement avoids summing overlapping allocations. Organizations using SWDM for O\_network MUST disclose the SWDM version and coefficients used, whether connection-type weighting was applied, how edge facility energy was handled, and known limitations.

### 8.4 Client-Side Operational Emissions (O\_client)

`O_client = E_client * I_client`

Where:

- `E_client` \= Energy consumed by end-user devices for browser rendering and execution per functional unit (kWh)  
- `I_client` \= Carbon intensity of electricity consumed by end-user devices (gCO2eq/kWh)

**Energy (E\_client)** includes:

- Browser rendering engine (layout, paint, composite)  
- JavaScript execution (parsing, compilation, runtime)  
- CSS processing and style calculation  
- Asset decoding (images, videos, audio)  
- User interaction processing  
- Service Worker execution

Organizations SHALL measure client-side energy using one of the following approaches (aligned with implementation tiers):

**Tier 1 \-- Reference Device Testing**: Measure energy consumption on reference devices representing the user base using browser profiling tools. Report device types and models used.

**Tier 2 \-- Device Mix Weighted Average**: Measure energy across multiple device categories (desktop, laptop, tablet, mobile), weighted by actual device distribution from analytics data.

**Tier 3 \-- Real User Monitoring**: Instrument browsers to collect energy consumption telemetry from actual users. Privacy-preserving sampling and anonymization required.

**Carbon Intensity (I\_client)**: Organizations SHALL use one of:

- **User-location-based**: Weighted average grid carbon intensity based on user geographic distribution  
- **Conservative estimate**: High percentile (e.g., 75th percentile) of global grid carbon intensity  
- **Disclosed assumption**: Global average grid carbon intensity with clear disclosure

### 8.5 Third-Party Service Attribution

Third-party operational emissions are not a separate top-level component. Instead, they are attributed within O\_server, O\_network, and O\_client based on where execution occurs (see §6.3.1 for the attribution framework).

Organizations SHALL account for third-party services using one of the following estimation approaches within the appropriate component:

**Method A \-- Vendor Disclosure**: Use energy and carbon intensity data published by the vendor. Attribute to the component where execution occurs. Disclose vendor, data source, and date.

**Method B \-- API Call Estimation**: For server-side API-based services, estimate energy as: `E_service = API_calls * E_per_call` where E\_per\_call is either vendor-disclosed or an industry default value. Attribute to O\_server (third-party sub-dimension). Disclose estimation methodology and coefficients.

**Method C \-- Client-Side Script Estimation**: For third-party scripts executing in the browser, estimate based on script execution time (Long Task API), data transferred, and resource consumption. Attribute to O\_client (third-party sub-dimension). Disclose methodology and limitations.

Organizations SHALL disclose which third-party services are measured, estimated, or excluded, and in which component they are attributed. Services contributing less than 1% of total estimated energy MAY be excluded but SHALL be listed in limitations disclosure.

### 8.6 Server-Side Embodied Emissions (M\_server)

Following the parent SCI specification:

`M_server = TE_server * TS_server * RS_server`

Where:

- `TE_server` \= Total embodied emissions of server-side hardware (gCO2eq)  
- `TS_server` \= Time-share: proportion of hardware lifespan reserved for this web application  
- `RS_server` \= Resource-share: proportion of hardware resources reserved for this web application

Expanded:

`M_server = TE_server * (TiR_server / EL_server) * (RR_server / ToR_server)`

For cloud infrastructure where physical hardware details are unavailable, organizations MAY use instance type specifications and embodied emissions databases (e.g., Boavizta, Cloud Carbon Footprint), virtual resource allocation as proxy for resource-share, or cloud provider embodied emissions data if disclosed.

### 8.7 Client-Side Embodied Emissions (M\_client)

`M_client = SUM(TE_device_type * TS_device_type * RS_device_type)` for each device type

Where for each device type (desktop, laptop, tablet, smartphone):

- `TE_device_type` \= Total embodied emissions for that device type (gCO2eq)  
- `TS_device_type` \= Time-share: proportion of device lifespan used for this web application  
- `RS_device_type` \= Resource-share: proportion of device resources used during usage time

**Time-share**: For a user session of duration D (hours) with device expected lifespan EL\_device (hours): `TS_device_type = D / EL_device`

**Resource-share**: Estimated as average CPU utilization during web application usage relative to total device active time.

**Device type distribution**: Organizations SHALL determine device mix using actual analytics data showing device type distribution, or industry default distribution with disclosure.

**Default embodied emissions values** (organizations MAY use more specific data if available):

| Device Type | Embodied Emissions | Expected Lifespan |
| :---- | :---- | :---- |
| Desktop computer | 400 kg CO2eq | 5 years |
| Laptop computer | 300 kg CO2eq | 4 years |
| Tablet | 100 kg CO2eq | 4 years |
| Smartphone | 80 kg CO2eq | 3 years |

Organizations using defaults SHALL disclose this choice. Organizations with access to device-specific lifecycle analysis data SHOULD use those values.

### 8.8 Network Infrastructure Embodied Emissions (M\_network)

M\_network captures embodied carbon in network infrastructure hardware: routers, switches, cell towers, undersea cables, internet exchange points, and edge points of presence.

**Status**: M\_network is structurally required as a top-level component to ensure completeness and prevent silent exclusion of material emissions. However, allocation of global network embodied carbon to individual web applications presents practical challenges.

**Allocation basis (important)**: Bytes-transferred (data volume) is NOT an acceptable basis for allocating M\_network to an individual web application. Network hardware embodied carbon does not meaningfully scale with the amount of data an application sends — it scales with deployment footprint, user count, connection sessions, coverage area, and hardware lifespan. Allocating by data volume creates an incentive structure where apparent reductions in file size correspond to a paper reduction in M\_network that does not reflect any real reduction in embodied hardware emissions. This mirrors the rationale for excluding bytes-transferred as the mandatory basis for O\_network in §8.3.

Valid allocation bases follow the parent SCI embodied pattern `M = TE * TS * RS`, where TS is time-share of hardware lifespan and RS is resource-share of hardware capacity. Practical proxies that fit this pattern include active user-sessions, user-hours, concurrent-connection-hours, or vendor-supplied allocation; bytes transferred does not fit this pattern.

**Tier-Based Implementation**:

- **Entry Tier**: May declare M\_network as "unpopulated — insufficient allocation methodology" with documented rationale  
- **Standard Tier**: Should apply industry-default embodied factors (e.g., Boavizta network hardware defaults) using an operator-disclosed non-bytes allocation methodology — for example, active user-sessions, user-hours, or vendor-supplied allocation. Assumptions and the chosen allocation basis MUST be disclosed. Bytes-transferred is not an acceptable allocation basis.  
- **Advanced Tier**: Should seek vendor-specific embodied data for major network providers (ISP, CDN, mobile operator) where available. Where vendors publish their own allocation methodology, organizations MAY adopt it with disclosure.

**Materiality Threshold**: Organizations MAY omit M\_network population only after documented materiality analysis showing network embodied emissions contribute less than 5% of total embodied emissions (M\_server + M\_network + M\_client). For network-intensive applications (streaming, real-time collaboration, large file transfer), M\_network is presumed material unless analysis demonstrates otherwise.

**Mandatory Disclosure**: Even when M\_network is unpopulated, organizations MUST disclose: why allocation was deemed impractical or immaterial, what data sources were evaluated, whether the application profile is network-intensive, and a commitment to revisit as allocation methodologies improve. An unpopulated-M\_network declaration SHOULD be revisited at least annually. For network-intensive applications, annual review is REQUIRED.

## 9\. Implementation Tiers

Organizations SHALL select one of three implementation tiers based on measurement sophistication and data availability. All tiers are legitimate when methodology is transparently disclosed.

### 9.1 Entry Tier

**Target users**: Teams beginning SCI for Web adoption with limited measurement infrastructure.

**Requirements**:

- Automated measurement using freely available tools  
- Direct measurement of server-side energy (cloud provider APIs, infrastructure monitoring)  
- Reference device measurement of client-side energy (minimum 1 device per major category)  
- Industry default coefficients for network energy  
- Third-party services estimated using conservative defaults or excluded with disclosure  
- Measurement period minimum 7 consecutive days of representative traffic  
- Full disclosure of methodology, tools, and limitations

**Acceptable data sources**:

- Cloud provider energy/carbon APIs  
- Browser developer tools for client-side profiling  
- Sustainable Web Design Model for network energy  
- Default embodied emissions values from this specification  
- Industry default third-party service coefficients

### 9.2 Standard Tier

**Target users**: Teams with established measurement practice seeking improved accuracy.

**Requirements**:

- Direct measurement of server-side and client-side energy across representative scenarios  
- Device-mix-weighted client-side measurements (minimum 2 devices per major category)  
- Network energy calculated using validated model (SWDM or equivalent)  
- Third-party services included using vendor data or documented estimation methodology  
- Carbon intensity calculated with daily granularity minimum  
- Measurement period minimum 30 consecutive days or representative business cycle  
- Validation of accuracy against published benchmarks where available  
- Comprehensive disclosure of methodology, data sources, and uncertainty

**Acceptable data sources**:

- Infrastructure instrumentation and telemetry  
- Browser profiling across device types  
- Network traffic analysis and modeling  
- Third-party vendor disclosure or API-based estimation  
- Regional grid carbon intensity databases (ElectricityMaps, WattTime, etc.)

### 9.3 Advanced Tier

**Target users**: Organizations with sophisticated measurement capabilities and sustainability commitments.

**Requirements**:

- Continuous measurement infrastructure for server-side and network components  
- Real user monitoring (RUM) for client-side energy with statistical sampling  
- Comprehensive third-party service inclusion with vendor engagement  
- Carbon intensity calculated with hourly granularity enabling carbon-aware optimization  
- Geographic and temporal carbon intensity distribution  
- Continuous measurement with regular reporting (monthly/quarterly)  
- Independent validation or audit of methodology  
- Public disclosure of methodology, data sources, and results  
- Embodied emissions using device-specific lifecycle analysis where available

### 9.4 Quantification Method by Tier

Organizations SHALL disclose for each component whether measurement or calculation was used:

| Component | Entry Tier | Standard Tier | Advanced Tier |
| :---- | :---- | :---- | :---- |
| O\_server | Measurement or calculation | Measurement preferred | Continuous measurement |
| O\_network (optional) | Not reported, or data-transfer fallback with disclosure | Hybrid or direct measurement where available; data-transfer fallback only if no alternative | Direct measurement or hybrid model; data-transfer fallback strongly discouraged |
| O\_client | Measurement (reference devices) | Measurement (device mix) | Measurement (RUM) |
| M\_server | Calculation (defaults or LCA) | Calculation (LCA databases) | Calculation (specific LCA) |
| M\_network | Unpopulated with disclosure | Calculation (industry defaults) | Calculation (vendor-specific) |
| M\_client | Calculation (defaults) | Calculation (device-specific) | Calculation (device-specific LCA) |
| O\_dev (optional) | Calculation if included | Measurement if included | Measurement if included |

Note: Third-party operational emissions are reported as sub-dimensions within O\_server, O\_network, and O\_client (see §6.3.1), not as a separate component row.

## 10\. Procedure

The steps required to calculate and report an SCI for Web score extend the parent specification procedure:

1. **Select Implementation Tier**: Choose Entry, Standard, or Advanced tier based on organizational capability and measurement sophistication goals (see Section 9).  
     
2. **Bound**: Decide on the software boundary; i.e., the components of the web application system to include. For web applications, this SHALL include at minimum: server-side infrastructure, network transfer, client-side execution, and end-user devices (see Section 6.4).  
     
3. **Scale**: Pick the functional unit which best describes how the application scales and delivers value to users. For web applications, this SHOULD measure delivered functionality rather than technical operations (see Section 7).  
     
4. **Define**: For each software component listed in the software boundary, decide on the quantification method: direct measurement using instrumentation and telemetry, or calculation using models and industry defaults (see Section 9.4).  
     
5. **Quantify**: Calculate a rate for every software component. The SCI for Web value of the whole application is the sum of the component values.  
     
6. **Report**: Disclose the SCI for Web score, implementation tier, software boundary, functional unit, calculation methodology, data sources, and limitations following the disclosure requirements (see Section 12).

## 11\. Implementation Examples

This section provides examples of how to apply the SCI for Web specification in real-world scenarios.

### 11.1 E-Commerce Platform Example

For a typical e-commerce web application, an SCI for Web score is calculated as follows:

**Functional Unit**: Completed transaction

**Boundary**: Server-side infrastructure (application servers, database, CDN edge), network transfer, client-side execution, third-party services (payment processor, analytics), end-user devices

**Calculation Method**:

1. Measure all mandatory operational and embodied carbon within the software boundary over a defined period (e.g., 30 days):  
   - O\_server: Energy consumed by application servers, databases, and CDN edge nodes, multiplied by regional carbon intensity. Third-party API calls to payment processor included under O\_server (third-party sub-dimension).  
   - O\_client: Client-side energy per transaction measured on reference devices, multiplied by user-location-weighted carbon intensity. Analytics script execution included under O\_client (third-party sub-dimension).  
   - M\_server, M\_network, M\_client: Embodied emissions allocated per §8.6–§8.8  
2. Optionally: report O\_network separately when a defensible methodology is available (see §8.3). In this example the organisation has chosen not to report O\_network because no direct measurement is available and they prefer not to rely on bytes-transferred estimates.  
3. Sum all included components to get total carbon (C)  
4. Count total completed transactions during the period (R)  
5. Calculate: `SCI = C / R`

**Example (mandatory components only)**:

- O\_server: 2,100 kg CO2eq/month (includes third-party API, 90 kg sub-dimension)  
- O\_client: 890 kg CO2eq/month (includes third-party scripts, 120 kg sub-dimension)  
- M\_server: 320 kg CO2eq/month  
- M\_network: 40 kg CO2eq/month (Boavizta defaults, industry average)  
- M\_client: 150 kg CO2eq/month  
- Total C: 3,500 kg CO2eq/month  
- Total completed transactions (R): 500,000/month  
- **SCI = 7.00 g CO2eq per completed transaction**

The organisation has disclosed that O\_network is not included in the reported score and provides rationale in the limitations section.

### 11.2 Content/Media Website Example

For a news or media website:

**Functional Unit**: Content item consumed (article read)

**Boundary**: Server-side (application servers, CMS, CDN), network transfer, client-side execution, third-party services (analytics, advertising), end-user devices

**Example**:

- Total C: 1,250 kg CO2eq/month  
- Total articles read (with engagement threshold of 30+ seconds): 2,000,000/month  
- **SCI \= 0.63 g CO2eq per article read**

### 11.3 SaaS Application Example

For a project management SaaS application:

**Functional Unit**: Active user session (minimum 5 minutes engagement)

**Boundary**: Server-side (application servers, database, real-time messaging infrastructure), network transfer, client-side execution, third-party services (authentication, email notification API), end-user devices

**Example**:

- Total C: 4,600 kg CO2eq/month  
- Total active user sessions: 150,000/month  
- **SCI \= 30.7 g CO2eq per active user session**

### 11.4 Reporting

For the e-commerce example above, the following should be reported:

- **SCI for Web Score**: 7.00 g CO2eq per completed transaction  
- **Implementation Tier**: Standard  
- **Software Boundary**: Application servers (AWS eu-west-1), PostgreSQL database, CloudFront CDN, client-side React application, Stripe payment API, Google Analytics  
- **O\_network Inclusion**: Excluded from score. No direct or vendor-disclosed network energy data available; organisation chose not to use bytes-transferred fallback due to acknowledged methodological weakness. Will revisit when CDN partner publishes measured energy data.  
- **Functional Unit**: Completed transaction (checkout flow resulting in order confirmation)  
- **Measurement Period**: 2026-01-01 to 2026-01-31 (31 days), average 16,100 transactions/day  
- **Component Breakdown**: O\_server 60% (including 2.6% third-party), O\_client 25% (including 3.4% third-party), M\_server 9%, M\_client 4%, M\_network 1%  
- **Quantification Methods**: O\_server measured via AWS Carbon Footprint Tool (Stripe API estimated via Method B, attributed as O\_server third-party sub-dimension); O\_client measured on 6 reference devices weighted by analytics device mix (Google Analytics script execution estimated via Method C, attributed as O\_client third-party sub-dimension); M\_network calculated using Boavizta network hardware defaults proportional to data volume  
- **Carbon Intensity**: ElectricityMaps daily average for eu-west-1; global average for client-side  
- **Limitations**: O\_network not reported (see above); third-party analytics client-side energy partially estimated; mobile device measurements limited to 2 models

## 12\. Disclosure Requirements

### 12.1 Mandatory Disclosures

Organizations reporting SCI for Web scores SHALL disclose:

1. **SCI for Web Score**: The calculated value with units (gCO2eq per \[functional unit\])  
2. **Implementation Tier**: Entry, Standard, or Advanced  
3. **Software Boundary**: Complete description of included and excluded components  
4. **O\_network Inclusion**: Whether O\_network was included in the reported score. If included, the methodology used (direct measurement, hybrid, or data-transfer fallback) and known limitations. If excluded, this SHALL be stated explicitly.  
5. **Functional Unit**: Definition of R with justification for selection  
6. **Measurement Period**: Start date, end date, duration, and traffic characterization  
7. **Quantification Methods**: For each mandatory component (O\_server, O\_client, M\_server, M\_network, M\_client) and for O\_network if reported:  
   - Measurement or calculation approach  
   - Tools and instrumentation used  
   - Data sources (including third-party data providers)  
   - Coefficients and constants used  
   - Estimation methodologies where measurement unavailable  
8. **First-party / Third-party Breakdown**: For each operational component where reported, the first-party / third-party sub-dimension split (see §6.3.1)  
9. **Carbon Intensity Data**: Sources, temporal granularity, geographic coverage  
10. **Limitations and Uncertainties**: Components with limited accuracy, excluded third-party services, estimation uncertainties, known gaps  
11. **Calculation Date**: When the SCI for Web score was calculated  
12. **Specification Version**: Version of SCI for Web specification used

### 12.2 Recommended Disclosures

1. **Component Breakdown**: Individual values for each component  
2. **Baseline Comparison**: Previous version or alternative implementation comparison  
3. **Improvement Actions**: Sustainability actions taken between measurements  
4. **Third-Party Details**: List of services measured, estimated, or excluded  
5. **Device Testing Details**: Specific device models used for client-side measurement  
6. **Geographic Distribution**: Server regions and user geographic distribution  
7. **Temporal Patterns**: Carbon intensity variation during measurement period

### 12.3 Disclosure Format

Organizations SHOULD provide disclosures in structured, machine-readable format (JSON, YAML) in addition to human-readable documentation.

## 13\. Handling of Edge Cases

### 13.1 Static Site Generation

- O\_server includes only energy to serve static files (web server, CDN edge)  
- Build-time generation energy is excluded (development lifecycle)  
- O\_client and O\_network included as normal

### 13.2 Single Page Applications (SPAs)

- Initial page load and all subsequent API calls included in functional unit  
- Functional unit SHOULD represent complete user workflow, not just initial load  
- Client-side hydration and ongoing JavaScript execution included in O\_client

### 13.3 Progressive Web Applications (PWAs)

- Online functionality included normally  
- Offline functionality from cached resources: no O\_server or O\_network; O\_client still measured  
- Service Worker execution included in O\_client

### 13.4 Serverless and Edge Computing

- Serverless function execution included in O\_server  
- Cold start overhead included (represents actual resource consumption)  
- Edge function execution at CDN nodes included in O\_server  
- Allocation methodology for shared infrastructure SHALL be disclosed

### 13.5 API-First Architectures

- Backend API serving energy in O\_server  
- Frontend application consuming APIs in O\_client  
- Functional unit SHOULD represent end-user value delivery, not individual API calls

## 14\. Measurement Period and Traffic Characterization

### 14.1 Minimum Measurement Periods

- **Entry tier**: Minimum 7 consecutive days  
- **Standard tier**: Minimum 30 consecutive days or one complete business cycle (whichever is longer)  
- **Advanced tier**: Continuous measurement with monthly or quarterly reporting

### 14.2 Traffic Characterization

Organizations SHALL disclose: average and peak traffic levels, traffic distribution (geographic, device types), deviation from typical traffic, and seasonal factors if applicable.

### 14.3 Normalization

When comparing SCI scores over time or across implementations, traffic patterns SHALL be normalized to ensure comparable functional unit denominator. Normalization methodology SHALL be disclosed.

## 15\. Carbon Intensity Data Sources

Organizations SHALL use location-based grid carbon intensity data. Recommended sources:

- ElectricityMaps ([https://www.electricitymaps.com/](https://www.electricitymaps.com/))  
- WattTime ([https://www.watttime.org/](https://www.watttime.org/))  
- International Energy Agency (IEA) emission factors  
- Regional/national grid operators' published carbon intensity data  
- UNFCCC emission factors

**Temporal granularity**:

- Entry tier: Annual average acceptable  
- Standard tier: Daily average minimum  
- Advanced tier: Hourly recommended

## 16\. Reference Devices

To enable comparable client-side measurements, organizations SHOULD select devices representing their actual user base from the following categories:

| Category | High-End | Mid-Range | Low-End |
| :---- | :---- | :---- | :---- |
| Desktop | Modern workstation (6+ core, dedicated GPU) | Standard desktop (4 core, integrated graphics) | Budget desktop (2 core, integrated graphics) |
| Laptop | Performance laptop (MacBook Pro 16" class) | Standard laptop (MacBook Air class) | Budget laptop (Chromebook class) |
| Smartphone | Current generation flagship | Mid-tier smartphone | Budget or older generation |
| Tablet | iPad Pro class | iPad Air class | Entry-level tablet |

Organizations SHALL disclose device make, model, OS version, and browser version used for testing.

## 17\. Core Characteristics

As this specification develops, the following core characteristics SHALL remain true, extending those defined in the parent SCI specification:

- **Sensitivity to web-specific sustainability actions**: Actions that reduce emissions in any component (client-side optimization, network transfer reduction, third-party service efficiency, distributed system carbon awareness, caching strategies) SHALL reduce SCI for Web scores.  
    
- **Systems-impact view across distributed architecture**: SCI for Web SHALL measure comprehensively across servers, networks, CDNs, third-party services, and client devices to prevent energy displacement.  
    
- **Progressive adoption enabling widespread implementation**: SCI for Web SHALL be implementable at different sophistication levels via implementation tiers, enabling teams with varying capabilities to adopt appropriate measurement.  
    
- **Encouragement of granular measurement with pragmatic defaults**: SCI for Web encourages the most granular measurement available while providing industry defaults for components where measurement is challenging.  
    
- **Prevention of gaming through comprehensive boundaries and disclosure**: SCI for Web SHALL resist gaming (energy displacement, quality degradation, boundary manipulation) through comprehensive boundaries, mandatory disclosure, and functional units measuring delivered value.  
    
- **Alignment with parent SCI principles**: All core characteristics of the parent SCI specification are preserved and extended with web-specific guidance.

## 18\. Exclusions

### 18.1 Market-Based Measures

Following the parent SCI specification, the following SHALL NOT reduce SCI for Web scores:

- Carbon offsets or credits  
- Renewable Energy Credits (RECs)  
- Power Purchase Agreements (PPAs) used to claim carbon-neutral energy  
- Electricity Attribute Certificates (EACs)  
- "Green hosting" certifications based solely on renewable energy purchases

Carbon intensity calculations SHALL use location-based grid carbon intensity excluding market-based adjustments.

### 18.2 Development and Testing Infrastructure

Development infrastructure is excluded from SCI for Web scores:

- Developer workstations  
- CI/CD pipelines  
- Build processes  
- Automated testing systems  
- Staging environments

These MAY be measured separately using parent SCI methodology.

## 19\. Baseline Comparison

When comparing an improved implementation to a baseline, organizations SHALL:

1. Maintain identical functional unit  
2. Maintain identical software boundary  
3. Use equivalent traffic profiles  
4. Apply consistent methodology  
5. Document what changed between baseline and comparison  
6. Disclose both scores with methodology

## 20\. Bibliography

\[1\] *Software Carbon Intensity (SCI) Specification v1.1.0*, Green Software Foundation, [https://sci.greensoftware.foundation/](https://sci.greensoftware.foundation/)

\[2\] *Sustainable Web Design Model v4*, Sustainable Web Design Community Group, [https://sustainablewebdesign.org/calculating-digital-emissions/](https://sustainablewebdesign.org/calculating-digital-emissions/)

\[3\] *Web Sustainability Guidelines (WSG)*, W3C, [https://www.w3.org/TR/web-sustainability-guidelines/](https://www.w3.org/TR/web-sustainability-guidelines/)

\[4\] *Greenhouse Gas Protocol ICT Sector Guidance*, GHG Protocol, [https://ghgprotocol.org/](https://ghgprotocol.org/)

\[5\] *The Net-Zero Standard*, Science Based Targets initiative (SBTi), [https://sciencebasedtargets.org/net-zero](https://sciencebasedtargets.org/net-zero)

\[6\] *CO2.js Documentation*, Green Web Foundation, [https://developers.thegreenwebfoundation.org/co2js/overview/](https://developers.thegreenwebfoundation.org/co2js/overview/)

\[7\] *Boavizta Environmental Footprint Data*, Boavizta, [https://www.boavizta.org/](https://www.boavizta.org/)

\[8\] *Cloud Carbon Footprint Methodology*, Cloud Carbon Footprint, [https://www.cloudcarbonfootprint.org/docs/methodology](https://www.cloudcarbonfootprint.org/docs/methodology)

---

## Appendices

### Appendix A: Disclosure Template

(To be developed: Structured JSON/YAML template for mandatory and recommended disclosures)

### Appendix A.1: Non-Normative Implementation Templates

The following templates are illustrative only and not normative. They are provided to help organizations structure their disclosures and internal analysis. Organizations SHOULD adapt them to their context.

#### A.1.1 M\_network Materiality Analysis Template

Use when evaluating whether M\_network can justifiably be declared unpopulated.

```
Application profile:
  - Application type:           [e.g., streaming / e-commerce / SaaS / informational]
  - Network-intensive?          [yes / no — justification]
  - Primary traffic type:       [cellular / fixed / mixed, with estimated breakdown]

Materiality estimate (using rough defaults):
  - M_server (estimated):       [X kg CO2eq / month]
  - M_client (estimated):       [Y kg CO2eq / month]
  - M_network (estimated, industry-default basis): [Z kg CO2eq / month]
  - Ratio:                      M_network / (M_server + M_network + M_client) = [%]

Data sources evaluated:
  - [e.g., Boavizta network hardware dataset — accessed / rejected because …]
  - [e.g., vendor X sustainability report — available / unavailable]

Decision:
  [ ] Populate M_network at Standard Tier using [allocation basis]
  [ ] Declare unpopulated — ratio < 5% and application is not network-intensive

Revisit cadence:
  [ ] Annual review scheduled for [date]
  [ ] Trigger events: [new data source / app profile change / vendor disclosure]
```

#### A.1.2 Functional Unit Selection Template (Multi-Purpose Applications)

Use when an application serves distinctly different user journeys.

```
Application overview:
  - Primary value-delivery pathways:
     1. [journey name — e.g., "purchase completed"]
     2. [journey name — e.g., "search performed"]
     3. [journey name — e.g., "account management session"]

Per-journey FU definition:
  For each journey above:
    - Name:                     [FU name]
    - Measurement source:       [analytics event / server log / synthetic]
    - Engagement threshold:     [if applicable, with rationale]
    - First-party / third-party attribution approach: [method]
    - Expected comparability:   [cross-org at per-FU level / internal-only]

Reporting plan:
  [ ] Report per-FU SCI for each journey
  [ ] Do not construct a single aggregate headline SCI
  [ ] Declare maturity level: [number of FUs tracked]

Governance:
  - Owner(s) of each FU definition:   [product / engineering / sustainability]
  - Review cadence:                   [e.g., quarterly]
```

#### A.1.3 O\_client First-Party / Third-Party Attribution Example

Illustrative per the §6.3.1 mandatory disclosure.

```
Component:     O_client
Total:         4.2 g CO2eq per completed transaction
Breakdown:
  O_client_first:  3.1 g CO2eq  (74% — application JavaScript, rendering, assets)
  O_client_third:  1.1 g CO2eq  (26% — Google Analytics 0.4g, Intercom 0.5g,
                                  Stripe.js 0.2g)

Measurement approach:
  - Long Tasks API for JavaScript execution time by origin (sampled RUM)
  - Resource Timing API for asset load energy attribution
  - Script bundle size × device-mix-weighted energy coefficient as fallback
    where attribution is impractical

Limitations disclosed:
  - Google Analytics: client-side execution partially estimated because the
    script does not expose fine-grained execution telemetry
```

#### A.1.4 CDN Bundled-Vendor-Data Allocation Template

Use when the CDN provider publishes a single bundled energy figure.

```
Vendor figure:
  - Source:                     [e.g., CDN provider sustainability portal]
  - Period:                     [e.g., 2026-01-01 to 2026-01-31]
  - Bundled energy:             [X kWh] for this application's traffic
  - Carbon intensity applied:   [y gCO2eq/kWh — source]
  - Bundled carbon:             [X * y] gCO2eq

Allocation rule:
  - Rationale:                  [e.g., cache-hit ratio split]
  - Split:                      [e.g., 70% O_network / 30% O_server]
  - Assumptions:                [e.g., cache hits are transmission-only;
                                 dynamic edge functions are compute-equivalent]
  - Data sources for split:     [e.g., CDN analytics dashboard]

Disclosure statement:
  "Allocation will transition to vendor-component-specific figures if/when
   the provider publishes them."
```

### Appendix B: Worked Calculation Examples

(To be developed: Step-by-step calculations for each application type with realistic data)

### Appendix C: Reference Values and Coefficients

(To be developed: Compiled reference values for embodied emissions, network energy coefficients, PUE defaults, and other constants)

### Appendix D: Tool and Data Source Directory

(To be developed: Curated list of measurement tools, instrumentation approaches, and data sources for each component)

---

## Document History

**Version 0.2.0-draft** (2026-02-18): First draft specification based on REPORT.md design requirements, structured to align with SCI for AI specification format.

**Future versions**: This specification will evolve through expert assembly, community feedback, implementation experience, and alignment with parent SCI specification updates.

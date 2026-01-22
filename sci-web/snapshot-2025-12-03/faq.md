# Scope

## Q: Are Progressive Web Apps (PWAs) in scope for SCI for Web?

Yes. PWAs that deliver functionality through browser-based interfaces fall within scope regardless of installability, offline capability, or service worker usage. The
architectural characteristics of PWAs (web platform APIs, browser rendering engines, HTTP delivery) align with the core definitional criteria. Organizations should measure
PWAs using the same methodology as traditional web applications, with cache behavior and offline functionality captured through standard measurement parameters.

## Q: How do I classify an API service that has both programmatic access and a browser-based dashboard?

Classify based on primary value delivery mode. If the browser dashboard is the main interface through which humans access the service's functionality, the entire system falls
within SCI for Web scope. If the API serves primarily machine clients with the dashboard as a secondary administrative interface, use base SCI methodology. The determining
factor is whether browser-mediated human interaction represents the primary usage pattern, not merely whether a browser interface exists.

## Q: Does SCI for Web apply to Electron or Tauri desktop applications?

Depends on architectural dependency. Applications that function as browser-based web applications wrapped in native containers (like Slack desktop, which requires continuous
server connectivity for core value delivery) fall within scope. Applications providing substantial standalone functionality with local file system integration and offline
capability (like VS Code) are out of scope and should use base SCI methodology. The classification depends on whether the application fundamentally operates as a web
application with a native wrapper versus a native application using web rendering technologies.

## Q: Are static content websites like blogs or documentation sites in scope?

Yes. Static content websites that deliver information to human users through browser rendering over HTTP/HTTPS protocols meet the core scope criteria. While these sites may
have minimal interactivity, they deliver functional value (content consumption) through browser-based interfaces. The scope intentionally includes the full spectrum from
passive content delivery to highly interactive applications to ensure comprehensive coverage of browser-based software.

## Q: What are examples of applications that fall OUTSIDE the SCI for Web scope?

Native mobile applications: Apps downloaded from app stores that use native UI frameworks (Swift UI, Jetpack Compose) rather than browser rendering engines fall outside scope,
even if they consume web APIs. Use base SCI methodology.

Desktop applications: Standalone software using native rendering (Microsoft Office, Adobe Creative Suite) is out of scope, even if internet-connected. Use base SCI
methodology.

Pure backend services: APIs, microservices, databases, and processing systems accessed only by other software (not through browser interfaces) fall outside scope. Use base SCI
methodology.

IoT and embedded systems: Smart home devices, industrial controllers, and embedded systems operating without browser-based interfaces are out of scope, even if networked. Use
base SCI methodology.

Command-line tools: Terminal applications and CLI utilities accessed through shell interfaces rather than browsers fall outside scope. Use base SCI methodology.

The key distinction: Applications fall outside SCI for Web scope when they fail one or more of the three core criteria: (1) HTTP/HTTPS protocol delivery, (2) browser rendering
environment, or (3) human interaction through browser interfaces. These applications should use the base SCI methodology instead.

## Q: How should I classify emerging technologies like voice interfaces, AR/VR, or future interaction paradigms?

Apply the three core definitional criteria regardless of interaction modality:

Voice interfaces to web applications: If users access a web application through voice commands that are processed by a browser-based interface (e.g., voice search on a
website, voice control of a web dashboard), this remains in-scope. The browser still mediates the interaction and renders the interface, even if voice is an input method.

AR/VR web experiences: WebXR applications delivered through browsers via HTTP/HTTPS and rendered by browser engines fall within scope, regardless of immersive interaction
paradigms. The delivery mechanism and rendering context determine scope, not the presentation modality.

Future technologies: As technology evolves, classify based on these principles:
- Protocol delivery: Does it use HTTP/HTTPS delivery?
- Rendering context: Does it use browser or web rendering engines?
- Human interaction: Do humans consume value through that rendered interface?

If all three criteria are met, the application falls within SCI for Web scope. This technology-agnostic approach ensures the specification remains relevant as interaction
paradigms evolve, without requiring constant redefinition. The focus on delivery mechanism and rendering context, rather than specific input/output modalities, provides
stability across technological change.

Platform-independence principle: The scope intentionally avoids tying definitions to current interaction patterns (keyboard/mouse/touch) or display characteristics
(rectangular screens). This future-proofs the specification for emerging interfaces while maintaining clear classification criteria.
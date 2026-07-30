Quick Start

Overview

The goal of this project is to minimize the amount of template customization required for each deployment.

Rather than modifying multiple Jinja templates, deployment-specific information is centralized in 00-import.j2. The remaining templates consume this data to generate the appropriate FortiGate configuration.

Outside of gui timeouts for admins and gui sessions. For most deployments, 00-import.j2 and valid meta-variables should be the only files that requires modification.

⸻

The 00-import File

00-import.j2 contains the variables and objects that define your deployment.

Typical items include:

* Global variables
* Feature toggles
* Underlay definitions
* Network definitions
* Hub definitions
* IPsec endpoint definitions
* eBGP neighbor definitions

As requirements change, update the data in 00-import.j2 rather than modifying the rendering templates.

⸻

Global Variables

Global variables control deployment-wide behavior.

Examples include enabling or disabling features such as:

* ADVPN
* VRF

The rendering templates automatically adjust based on these settings, allowing the same template set to support multiple deployment scenarios.

⸻

Underlays

Define each WAN underlay used by the deployment.

Each underlay can be configured for either nased on the value of the mata-variable. These can used in a pre-run scripts:

* Static addressing
* DHCP

Templates automatically generate the appropriate interface configuration based on the values provided.

⸻

Networks

Network objects define the addressing used throughout the deployment.

Keeping these definitions centralized ensures that all templates reference the same values and reduces the chance of configuration inconsistencies.

⸻

Hub Definitions

Each hub is defined as a single object.

A hub contains all information required to build the hub configuration, including:

* Hub name
* Serial number
* Exchange IP
* eBGP neighbors
* IPsec endpoints

Adding a new hub or modifying an existing one typically only requires updating this object.

⸻

Endpoint Definitions

Each endpoint defines everything needed to build an IPsec tunnel, including:

* Phase1 interface
* Remote gateway
* Network ID
* Hub interface
* Branch interface

Templates iterate through these endpoint definitions to generate the required configuration automatically.

⸻
Templates marked {#       Pre-VDOM FMG Jinja Script      #}  must be set as such
⸻

Typical Workflow

1. Load your use case specific meta-variables into FMG
2. Open 00-import.j2.
3. Configure the global variables.
4. Enable or disable features such as ADVPN and VRF.
5. Confirm your WAN underlays.
6. Define your network objects based on your meta-variables.
7. Configure your hub and endpoint objects.
8. Render the templates in FortiManager via blue prints, model device or manual.
9. Review the generated CLI before installation.

By keeping deployment-specific information in a single file, the rendering templates remain reusable across multiple customers and deployment scenarios.

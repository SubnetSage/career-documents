# BGP Data Collection and Analysis Project

This project is designed to automate the process of collecting BGP (Border Gateway Protocol) information from a network device, storing the gathered data in a text file, indexing the data for efficient retrieval, and querying the indexed data for insights. This is done in order to gather information in my MPLS lab and combine programming with AI.

## How the Project Works

### 1. Device Connection and Data Collection

The script connects to a Cisco IOS device using `netmiko` and executes several commands to gather BGP neighbor details and routing information for a specified VRF (Virtual Routing and Forwarding) and neighbor.

#### Commands executed include:

- `show ip bgp vpnv4 vrf {vrf_name} summary`
- `show ip bgp vpnv4 vrf {vrf_name} neighbors {bgp_neighbor} received-routes`
- `show ip bgp vpnv4 vrf {vrf_name} neighbors {bgp_neighbor} advertised-routes`
- `show ip bgp vpnv4 all`

### 2. Saving Data

The collected data is saved into a text file named `bgp_analysis_output.txt`.

### 3. Indexing the Data

- Moves the text file to a `data` directory.
- Uses `LlamaIndex` to read the text file and create a vector store index for efficient data retrieval.
- The index is persisted for future use if it doesn't already exist.

### 4. Querying the Data

- Loads the existing index if available, otherwise creates a new one.
- Uses a query engine to ask questions about the indexed data.
- Example query: "What are the received routes for BGP neighbor {bgp_neighbor}?" (replace with relevant queries based on the BGP data).

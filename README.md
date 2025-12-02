# Google Cloud Resource Visibility
This Repo describes the permissions and roles required to programmatically read resource utilization metrics and instance shapes.

Based on our testing, here is the comprehensive review of the permissions required to successfully run the final Smart Parsing Audit Script.

We have narrowed this down to exactly 4 permissions. This is a highly restrictive "Least Privilege" set that grants read-only access to specific infrastructure metadata and metric history, without exposing code, storage, or other sensitive data.

# Least Privilege Permissions
In addition to the permissions already specified in the custom ProsperOps Role, we need:

# Compute Engine
compute.instances.list		
Inventory: Used to fetch the list of VM IDs (12345...) and map them to their Machine Type names (e2-medium, custom-2-4096).

compute.machineTypes.list
Specs Dictionary: Used to download the catalog of standard machine types (e.g., to know that n1-standard-4 has 15GB RAM).

# Cloud Monitoring
monitoring.timeSeries.list		
The Data: Used by curl to fetch the actual CPU/Memory usage history points.

# Resource Manager
resourcemanager.projects.get		
Handshake: Required by client libraries and API calls to validate the project ID exists before running queries.

# Misc Extra
compute.instances.listEffectiveTags 
Tagging Visibility: Separate need here but documenting for future reference.

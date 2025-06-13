## general kql notes

stats(values) in sql equivalent

```
TableName
| summarize item1_values = make_set(item1), count() by item2
```

List all assessments names about container vulnerabilities

```
securityresources 
| where type == "microsoft.security/assessments"
| extend resourceType = tostring(properties.resourceDetails.ResourceType)
| extend displayName = tostring(properties.displayName)
| where resourceType == "acr.containerimage" or resourceType == "microsoft.containerregistry/registries" or resourceType contains "microsoft.containerservice/managedclusters/securityentitydata" or name == "c609cf0f-71ab-41e9-a3c6-9a1f7fe1b8d5" or displayName contains "[Preview] Containers running in Azure should have vulnerability findings resolved"
| where displayName != "Container registries should not allow unrestricted network access" and displayName != "Container registries should use private link"
//| where displayName contains "[Preview] Containers running in Azure should have vulnerability findings resolved"
| distinct  displayName
```

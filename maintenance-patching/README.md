# Maintenance Patching

Maintenance patching is where we want to get the patch out, across all deployments, but it is not time critical and we can wait for our automated dependency checkers & testing suites to execute.

One way to handle this, is to create a centralized composer patching package. Where we can declare a selection of patches, we want applied to the entire infrastructure. And require this package within the rest of our projects. 

```json
{
    "name": "acme-agency/m2-module-patches",
    "description": "Magento 2 Module containing all required M2 Patches",
    "extra": {
        "patches": {
            "*": {
                "CVE-2025-54236 (Session Reaper)": {
                    "source": "patches/CVE-2025-54236.patch",
                    "depends": {
                        "magento/framework": "<=104.0.0"
                    }
                }
            }
        }
    }
}
```

## Example Demo 
Both the Magento 2 Projects are vanilla Magento installations which include the `m2-module-patches` module. You can adjust the module to add / remove patches, then perform a composer install on both the project folders to see the result.
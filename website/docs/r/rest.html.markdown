---
layout: "aci"
page_title: "ACI: aci_rest"
sidebar_current: "docs-aci-resource-rest"
description: |-
  Manages ACI Model Objects via REST API calls. Any Model Object that is not supported by provider can be created/managed using this resource. 
---

# aci_rest #
Manages ACI Model Objects via REST API calls. Any Model Object that is not supported by provider can be created/managed using this resource. 

## Example Usage ##

```hcl
resource "aci_tenant" "tenant_for_rest_example" {
  name        = "tenant_for_rest"
  description = "This tenant is created by terraform ACI provider"
}

resource "aci_rest" "rest_l3_ext_out" {
  path       = "api/node/mo/${aci_tenant.tenant_for_rest_example.id}/out-test_ext.json"
  class_name = "l3extOut"

  content = {
    "name" = "test_ext"
  }
}
```

## Argument Reference ##
* `path` - (Required) ACI path where object should be created. Starting with api/node/mo/{parent-dn}(if applicable)/{rn of object}.json  
* `class_name` - (Optional) Which class object is being created. (Make sure there is no colon in the classname )
* `content` - (Required) Map of key-value pairs those needed to be passed to the Model object as parameters. Make sure the key name matches the name with the object parameter in ACI.

* `dn` - (Optional) Distinguished name of object being managed. 

## Attribute Reference

The only attribute that this resource exports is the `id`, which is set to the
Dn of the object created by it.

## Importing ##

This resource does not support import.
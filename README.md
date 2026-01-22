# Konflux Doc Templates ✍

## Description

The Konflux Doc Templates repository contains documentation templates for Konflux pipelines in [Jinja](https://jinja.palletsprojects.com/en/stable/) YAML format. 
Jinja is suitable for documentation templates because it moves logic into the templates instead of the code.

Currently, the following templates are available: 

* `container-y.yaml`: Container template for y-stream
* `container-z.yaml`: Container template for z-stream
* `rpm-y.yaml`: RPM template for y-stream
* `rpm-z.yaml`: RPM template for z-stream

The templates contains the following shared variables:

*  `{%- set product_version_str = advisory.spec.product_version | string() %}`
*  `{%- set rhel_major_version = product_version_str.split('.')[0] %} `: For example 10 for RHEL 10
*  `{%- set rhel_minor_version = product_version_str.split('.')[:2] | join('.') %}`: For example 10.1 for RHEL 10.1


The template defines shared variables in the `vars` section:

* `{{ advisory.spec.severity }}`: For RHSA advisory type only
* `{{ advisory.spec.product_name }}`
* `{{ package_name }}`: For z-stream RPM templates only
* `{{ image_description }}`: For z-stream container templates only


Differences between templates are summarized in the following table: 

*Note*: The `solution` field is the same for all cases, therefore it is not listed in the table. 

| Advisory type | YAML field name | y-stream release | z-stream release |
|--------------|------------------------|------------------|------------------|
| **RHSA** | synopsis | ✅ Multi component | ✅ Single component |
|  | topic | ✅ Multi component | ✅ Single component |
|  | description | ✅ Multi component (Updated Images/Packages tab) | ✅ Single component (image/package description)|
|  | references | ✅ DO link to Release Notes | ❌ DO NOT link to Release Notes |
| **RHBA / RHEA** | synopsis | ✅ Required | ✅ Required |
|  | topic | ✅ Required | ✅ Required |
|  | description | ✅ Multi component (Updated Images/Packages tab) | ✅ Single component (image/package description)|
|  | references | ✅ DO link to Release Notes | ❌ DO NOT link to Release Notes |

## Notes

* JIRA tracker RHEL 9.8/10.2: [RHELDOCS-21378](https://issues.redhat.com/browse/RHELDOCS-21378)
* JIRA tracker RHEL 9.7/10.1: [RHELDOCS-20161](https://issues.redhat.com/browse/RHELDOCS-20161)
* JIRA tracker for RHEL on Konflux: [ROK-1220](https://issues.redhat.com/browse/ROK-1220)


## Acknowledgement

This work is based on my `errata_doc_approver.py` script, which approves advisories in the Errata Tool and is provided in the [docs-errata-approver](https://gitlab.cee.redhat.com/gnecasov/docs-errata-approver) repository. 


♥️ I would like to thank the following colleagues. Without their support it would have been impossible to complete this work:
* Konflux team: Chuang Cao and Lu Zhang. 
* CCS team: Marci Wolfe, Catherine Tomasko.
* All engineers, package owners, QAs, and so on for their valuable discussions and insights. 


## Support
Gabriela Nečasová, gnecasov@redhat.com, Slack: Gabi N. 

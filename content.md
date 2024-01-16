# Secrets Rotation

## Overview

Secret rotation is the process of regularly changing the cryptographic secrets used to secure sensitive information and data within an organization. This is done to mitigate the risk of compromise due to potential exposure,  unauthorized access to sensitive information, data breaches, and damaged reputation. The process involves generating a new set of secrets to replace the old ones and then securely updating the affected systems and applications with the new secrets.

## Problem Statement

Inadvertent sharing of secrets is a significant security risk that organizations must address. Among the most common ways in which secrets get exposed are embedding the secrets directly in code or leaking them through run-time processes, automation pipelines, and logs. One way to mitigate the risk of leaked secrets is to adopt a proactive approach to secrets management, including regular secrets rotation and proper storage.

## Effective Key Rotation Strategy

Effective secrets management is essential for preventing unauthorized access to sensitive information, and one of the best practices is regular secret rotation. To implement this practice, developers should store secrets outside of code repositories using a secure [Secrets Store](https://github.com/microsoft/secrets-store), which can be accessed programmatically. It is crucial to use [secret detection methods](https://github.com/microsoft/secrets-detection) to scan for secrets that may be hard-coded in code repositories, as these could be easily exposed to unauthorized parties.

### Secret Rotation Goals

The goal of an effective secret rotation strategy is to minimize disruption while ensuring that the new secret value is reliably and securely transmitted to all relevant systems. This requires careful planning and coordination to minimize downtime, avoid potential data loss or corruption, and ensure that all systems are updated with the new secret value in a secure and consistent manner. By prioritizing these considerations, organizations can implement secret rotation with confidence, knowing that they are protecting their sensitive data and assets against unauthorized access and exposure.

It is essential to align rotation plans with the secret inventory discussed in the [Microsoft Solutions Playbook](https://github.com/microsoft/secrets-detection), in the Secrets Lifecycle Management guidance found under Governance. This ensures that the current rotation strategy for each secret is easily accessible to those responsible for DevOps processes. Any updates or additions to the rotation method for a given secret should be reflected in the inventory, making it simple for implementation. Maintaining an up-to-date inventory is vital in ensuring that secrets remain secure and protected against unauthorized access or exposure throughout their lifecycle.

## Proposed Actions

Secret rotation is a crucial aspect of a comprehensive secrets management strategy, and there are two primary actions to consider when implementing it.

### Scheduled Rotation

Secrets should be rotated on a predetermined schedule to reduce their lifetime, minimizing the risk of long-term exposure of assets that rely on a specific secret.

### On-Demand Rotation

In the event that a secret is accidentally leaked, a rapid rotation strategy is required to help to proactively mitigate the exposure of resources protected by the compromised secret.

### Secret Rotation Recommendations

1. Choose a reasonable time for rotation.This applies to both time of day and frequency.
1. Consider using encryption key strength in relation to what is being protected. Longer keys provide stronger security, but may also result in slower key processing and decryption times.
1. Leverage the benefits of highly-available infrastructure during key rotation to reduce the likelihood of downtime where possible.
1. In the course of Rotating keys/certificates ensure that the new keys or certificates have the same parameters and strength as the ones being replaced.
1. Avoid creating secrets with empty expiration dates.
1. When re-encryption of data is necessary, increase the time between scheduled rotations to optimize resource utilization. It is common to leverage (symmetric) Data Encryption Keys to protect data at rest and (asymmetric) Key Encryption Keys for data in transit. Schemes as described in this document, fit well into the Key Vault model.
1. When the responsibility of application or system is transferred, it is recommended to rotate all the secrets.This mitigates the risk of continued access to the application and it's data by those who previously controlled the system.

## Resources

- [Automated Key Rotation configuration in Azure Key Vault](https://learn.microsoft.com/en-us/azure/key-vault/keys/how-to-configure-key-rotation)
- [On-Demand Manual Key Rotation](https://learn.microsoft.com/en-us/azure/key-vault/keys/how-to-configure-key-rotation#rotation-on-demand)
- [Configure Key Rotation using the Azure CLI](https://learn.microsoft.com/en-us/azure/key-vault/keys/how-to-configure-key-rotation#azure-cli-1)
- [Tutorial: Automatic rotation of a single set of authentication credentials](https://learn.microsoft.com/azure/key-vault/secrets/tutorial-rotation)
- [Tutorial: Automatic rotation of two sets of authentication credentials](https://learn.microsoft.com/azure/key-vault/secrets/tutorial-rotation-dual)
- [Sample: Using Terraform to store and rotate Azure Function API keys used by API Management in Key Vault](https://github.com/mspnp/vnet-integrated-serverless-microservices/blob/main/docs/key_rotation.md)

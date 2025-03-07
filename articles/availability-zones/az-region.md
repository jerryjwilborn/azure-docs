---
title: Azure services that support availability zones
description: Learn what services are supported by availability zones and understand resiliency across all Azure services.
author: awysza
ms.service: azure
ms.topic: conceptual
ms.date: 12/10/2021
ms.author: rarco
ms.reviewer: cynthn
ms.custom: references_regions
---
# Azure services that support availability zones

Azure [regions and availability zones](az-overview.md) are physically separate locations within each Azure region that are tolerant to datacenter failures because of redundant infrastructure and logical isolation of Azure services. 

Azure services that support availability zones are designed to provide the right level of resiliency and flexibility along with ultra-low latency. With Azure services that support availability zones, whether you architect your own resiliency or opt for automatic replication and distribution, the benefit is the same. You get superior resiliency across highly available services, no matter the service type. 

Azure strives to enable high resiliency across every service and offering. Running Azure services that support availability zones provides fully transparent and consistent resiliency against nearly all scenarios, without interruption.

## Azure regions with availability zones

Azure provides the most extensive global footprint of any cloud provider and is rapidly opening new regions and availability zones. The following regions currently support availability zones.

| Americas | Europe | Africa | Asia Pacific |
|--------------------|----------------------|---------------------|----------------|
| Brazil South | France Central | South Africa North | Australia East |
| Canada Central | Germany West Central | | Central India |
| Central US | North Europe | | Japan East |
| East US | Norway East | | Korea Central |
| East US 2 | UK South | | Southeast Asia |
| South Central US | West Europe | | East Asia |
| US Gov Virginia | Sweden Central |  | |
| West US 2 | | | |
| West US 3 | | | |

For a list of Azure services that support availability zones by Azure region, see the [availability zones documentation](az-overview.md).

## Highly available services

Three types of Azure services support availability zones: *zonal*, *zone-redundant*, and *always-available* services. You can combine all three of these architecture approaches when you design your resiliency strategy.

- **Zonal services**: A resource can be deployed to a specific, self-selected availability zone to achieve more stringent latency or performance requirements. Resiliency is self-architected by replicating applications and data to one or more zones within the region. Resources can be pinned to a specific zone. For example, virtual machines, managed disks, or standard IP addresses can be pinned to a specific zone, which allows for increased resiliency by having one or more instances of resources spread across zones.
- **Zone-redundant services**: Resources are replicated or distributed across zones automatically. For example, zone-redundant services replicate the data across three zones so that a failure in one zone doesn't affect the high availability of the data. 
- **Always-available services**: Always available across all Azure geographies and are resilient to zone-wide outages and region-wide outages. For a complete list of always-available services, also called non-regional services, in Azure, see [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).

Azure offerings are grouped into three categories that reflect their _regional_ availability: *foundational*, *mainstream*, and *strategic* services. Azure's general policy on deploying services into any given region is primarily driven by region type, service category, and customer demand. For more information, see [Azure services](region-types-service-categories-azure.md).

- **Foundational services**: Available in all recommended and alternate regions when a region is generally available, or within 90 days of a new foundational service becoming generally available.
- **Mainstream services**: Available in all recommended regions within 90 days of a region's general availability. Mainstream services are demand-driven in alternate regions, and many are already deployed into a large subset of alternate regions.
- **Strategic services**: Targeted service offerings, often industry-focused or backed by customized hardware. Strategic services are demand-driven for availability across regions, and many are already deployed into a large subset of recommended regions.

Azure services that support availability zones, including zonal and zone-redundant offerings, are continually expanding.

For more information on older-generation virtual machines, see [Previous generations of virtual machine sizes](../virtual-machines/sizes-previous-gen.md).

The following tables provide a summary of the current offering of zonal, zone-redundant, and always-available Azure services. They list Azure offerings according to the regional availability of each.

##### Legend
![Legend containing icons and meaning of each with respect to service category and regional availability of each service in the table.](media/legend.png) 

In the Product Catalog, always-available services are listed as "non-regional" services.

### ![An icon that signifies this service is foundational.](media/icon-foundational.svg) Foundational services 

| **Products**   | **Resiliency**   |
| --- | --- |
| [Azure Application Gateway (V2)](../application-gateway/application-gateway-autoscaling-zone-redundant.md) | ![An icon that signifies this service is zonal.](media/icon-zonal.svg)  |
| [Azure Backup](../backup/backup-create-rs-vault.md)  | ![An icon that signifies this service is zonal.](media/icon-zonal.svg)  |
| [Azure Cosmos DB](../cosmos-db/high-availability.md) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg)   |
| [Azure DNS: Azure DNS Private Zones](../dns/private-dns-getstarted-portal.md) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg)  |
| [Azure ExpressRoute](../expressroute/designing-for-high-availability-with-expressroute.md) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg)  |
| [Azure Public IP](../virtual-network/ip-services/public-ip-addresses.md) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) ![An icon that signifies this service is zonal.](media/icon-zonal.svg) |
| [Azure Site Recovery](../site-recovery/azure-to-azure-how-to-enable-zone-to-zone-disaster-recovery.md) | ![An icon that signifies this service is zonal](media/icon-zonal.svg) |
| [Azure SQL](../azure-sql/database/high-availability-sla.md) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) |
| [Azure Event Hubs](../event-hubs/event-hubs-geo-dr.md#availability-zones) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) |
| [Azure Key Vault](../key-vault/general/disaster-recovery-guidance.md) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) |
| [Azure Load Balancer](../load-balancer/load-balancer-standard-availability-zones.md) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) ![An icon that signifies this service is zonal](media/icon-zonal.svg) |
| [Azure Service Bus](../service-bus-messaging/service-bus-geo-dr.md#availability-zones) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) |
| [Azure Service Fabric](../service-fabric/service-fabric-cross-availability-zones.md) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) ![An icon that signifies this service is zonal](media/icon-zonal.svg)  |
| [Azure Storage account](../storage/common/storage-redundancy.md)  | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) |
| [Azure Storage: Azure Data Lake Storage](../storage/blobs/data-lake-storage-introduction.md) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg)  |
| [Azure Storage: Disk Storage](../storage/common/storage-redundancy.md) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) |
| Azure Storage: [Blob Storage](../storage/common/storage-redundancy.md) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg)  |
| Azure Storage: [Managed Disks](../virtual-machines/managed-disks-overview.md) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) ![An icon that signifies this service is zonal](media/icon-zonal.svg) |
| [Azure Virtual Machine Scale Sets](../virtual-machine-scale-sets/scripts/cli-sample-zone-redundant-scale-set.md) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) ![An icon that signifies this service is zonal.](media/icon-zonal.svg) |
| [Azure Virtual Machines](../virtual-machines/windows/create-powershell-availability-zone.md) | ![An icon that signifies this service is zonal.](media/icon-zonal.svg)  |
| Virtual Machines: [Av2-Series](../virtual-machines/windows/create-powershell-availability-zone.md) | ![An icon that signifies this service is zonal.](media/icon-zonal.svg) |
| Virtual Machines: [Bs-Series](../virtual-machines/windows/create-powershell-availability-zone.md) | ![An icon that signifies this service is zonal.](media/icon-zonal.svg) |
| Virtual Machines: [DSv2-Series](../virtual-machines/windows/create-powershell-availability-zone.md) | ![An icon that signifies this service is zonal.](media/icon-zonal.svg) |
| Virtual Machines: [DSv3-Series](../virtual-machines/windows/create-powershell-availability-zone.md) | ![An icon that signifies this service is zonal.](media/icon-zonal.svg) |
| Virtual Machines: [Dv2-Series](../virtual-machines/windows/create-powershell-availability-zone.md) | ![An icon that signifies this service is zonal.](media/icon-zonal.svg) |
| Virtual Machines: [Dv3-Series](../virtual-machines/windows/create-powershell-availability-zone.md) | ![An icon that signifies this service is zonal.](media/icon-zonal.svg) |
| Virtual Machines: [ESv3-Series](../virtual-machines/windows/create-powershell-availability-zone.md) | ![An icon that signifies this service is zonal.](media/icon-zonal.svg) |
| Virtual Machines: [Ev3-Series](../virtual-machines/windows/create-powershell-availability-zone.md) | ![An icon that signifies this service is zonal.](media/icon-zonal.svg) |
| Virtual Machines: [F-Series](../virtual-machines/windows/create-powershell-availability-zone.md) | ![An icon that signifies this service is zonal.](media/icon-zonal.svg)  |
| Virtual Machines: [FS-Series](../virtual-machines/windows/create-powershell-availability-zone.md) | ![An icon that signifies this service is zonal.](media/icon-zonal.svg) |
| Virtual Machines: [Shared Image Gallery](../virtual-machines/shared-image-galleries.md#make-your-images-highly-available) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg)  |
| [Azure Virtual Network](../vpn-gateway/create-zone-redundant-vnet-gateway.md) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) |
| [Azure VPN Gateway](../vpn-gateway/about-zone-redundant-vnet-gateways.md) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) |

\*VMs that support availability zones: AV2-series, B-series, DSv2-series, DSv3-series, Dv2-series, Dv3-series, ESv3-series, Ev3-series, F-series, FS-series, FSv2-series, and M-series.\*

### ![An icon that signifies this service is mainstream.](media/icon-mainstream.svg) Mainstream services

| **Products**   | **Resiliency**   |
| --- | --- |
| [Azure Active Directory Domain Services](../active-directory-domain-services/overview.md) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) |
| [Azure API Management](../api-management/zone-redundancy.md) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) |
| [Azure App Configuration](../azure-app-configuration/faq.yml#how-does-app-configuration-ensure-high-data-availability) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) |
| [Azure App Service](../app-service/how-to-zone-redundancy.md) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) |
| [Azure App Service: App Service Environments](../app-service/environment/zone-redundancy.md) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) ![An icon that signifies this service is zonal](media/icon-zonal.svg) |
| [Azure Bastion](../bastion/bastion-overview.md) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) |
| [Azure Batch](../batch/create-pool-availability-zones.md) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) |
| [Azure Cache for Redis](../azure-cache-for-redis/cache-high-availability.md) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) ![An icon that signifies this service is zonal](media/icon-zonal.svg) |
| [Azure Cognitive Search](../search/search-performance-optimization.md#availability-zones) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) |
| [Azure Container Instances](../container-instances/container-instances-region-availability.md) | ![An icon that signifies this service is zonal](media/icon-zonal.svg) |
| [Azure Container Registry](../container-registry/zone-redundancy.md) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) |
| [Azure Data Explorer](/azure/data-explorer/create-cluster-database-portal) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) |
| [Azure Data Factory](../data-factory/index.yml) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) |
| Azure Database for MySQL – [Flexible Server](../mysql/flexible-server/concepts-high-availability.md) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) |
| Azure Database for PostgreSQL – [Flexible Server](../postgresql/flexible-server/overview.md) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) |
| [Azure DDoS Protection](../ddos-protection/ddos-faq.yml) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) |
| [Azure Disk Encryption](../virtual-machines/disks-redundancy.md) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) |
| [Azure Event Grid](../event-grid/overview.md) | ![An icon that signifies this service is zone-redundant](media/icon-zone-redundant.svg) |
| [Azure Firewall](../firewall/deploy-availability-zone-powershell.md) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) |
| [Azure Firewall Manager](../firewall-manager/quick-firewall-policy.md) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) |
| [Azure Functions](../azure-functions/azure-functions-az-redundancy.md) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) |
| [Azure HDInsight](../hdinsight/hdinsight-use-availability-zones.md) | ![An icon that signifies this service is zonal](media/icon-zonal.svg)  |
| [Azure IoT Hub](../iot-hub/iot-hub-ha-dr.md) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) |
| [Azure Kubernetes Service (AKS)](../aks/availability-zones.md) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) ![An icon that signifies this service is zonal](media/icon-zonal.svg) |
| Azure Logic Apps | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) |
| [Azure Monitor](../azure-monitor/logs/availability-zones.md)  | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) |
| [Azure Monitor: Application Insights](../azure-monitor/logs/availability-zones.md)  | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) |
| [Azure Monitor: Log Analytics](../azure-monitor/logs/availability-zones.md) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) |
| [Azure Network Watcher](../network-watcher/frequently-asked-questions.yml) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) |
| Azure Network Watcher: [Traffic Analytics](../network-watcher/frequently-asked-questions.yml) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) |
| Azure Notification Hubs | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) |
| [Azure Private Link](../private-link/private-link-overview.md) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) |
| [Azure Route Server](../route-server/route-server-faq.md) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) |
| Azure Stream Analytics | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg)  |
| [SQL Server on Azure Virtual Machines](../azure-sql/database/high-availability-sla.md) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) |
| Azure Storage: [Files Storage](../storage/files/storage-files-planning.md) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) |
| [Azure Virtual WAN](../virtual-wan/virtual-wan-faq.md#how-are-availability-zones-and-resiliency-handled-in-virtual-wan) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) |
| [Azure Web Application Firewall](../firewall/deploy-availability-zone-powershell.md) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) |
| [Power BI Embedded](/power-bi/admin/service-admin-failover#what-does-high-availability) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) |
| Virtual Machines: [Azure Dedicated Host](../virtual-machines/windows/create-powershell-availability-zone.md) | ![An icon that signifies this service is zonal.](media/icon-zonal.svg) |
| Virtual Machines: [Ddsv4-Series](../virtual-machines/windows/create-powershell-availability-zone.md) | ![An icon that signifies this service is zonal.](media/icon-zonal.svg) |
| Virtual Machines: [Ddv4-Series](../virtual-machines/windows/create-powershell-availability-zone.md) | ![An icon that signifies this service is zonal.](media/icon-zonal.svg) |
| Virtual Machines: [Dsv4-Series](../virtual-machines/windows/create-powershell-availability-zone.md) | ![An icon that signifies this service is zonal.](media/icon-zonal.svg) |
| Virtual Machines: [Dv4-Series](../virtual-machines/windows/create-powershell-availability-zone.md) | ![An icon that signifies this service is zonal.](media/icon-zonal.svg) |
| Virtual Machines: [Edsv4-Series](../virtual-machines/windows/create-powershell-availability-zone.md) | ![An icon that signifies this service is zonal.](media/icon-zonal.svg) |
| Virtual Machines: [Edv4-Series](../virtual-machines/windows/create-powershell-availability-zone.md) | ![An icon that signifies this service is zonal.](media/icon-zonal.svg) |
| Virtual Machines: [Esv4-Series](../virtual-machines/windows/create-powershell-availability-zone.md) | ![An icon that signifies this service is zonal.](media/icon-zonal.svg) |
| Virtual Machines: [Ev4-Series](../virtual-machines/windows/create-powershell-availability-zone.md) | ![An icon that signifies this service is zonal.](media/icon-zonal.svg) |
| Virtual Machines: [Fsv2-Series](../virtual-machines/windows/create-powershell-availability-zone.md) | ![An icon that signifies this service is zonal.](media/icon-zonal.svg) |
| Virtual Machines: [M-Series](../virtual-machines/windows/create-powershell-availability-zone.md) | ![An icon that signifies this service is zonal.](media/icon-zonal.svg) |
| Virtual WAN: [Azure ExpressRoute](../virtual-wan/virtual-wan-faq.md#how-are-availability-zones-and-resiliency-handled-in-virtual-wan) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) |
| Virtual WAN: [Point-to-site VPN Gateway](../vpn-gateway/about-zone-redundant-vnet-gateways.md) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) |
| Virtual WAN: [Site-to-site VPN Gateway](../vpn-gateway/about-zone-redundant-vnet-gateways.md) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) |

### ![An icon that signifies this service is strategic.](media/icon-strategic.svg) Strategic services

| **Products**   | **Resiliency**   |
| --- | --- |
| [Azure IoT Hub Device Provisioning Service](../iot-dps/about-iot-dps.md) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) |
| Azure Red Hat OpenShift | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg) ![An icon that signifies this service is zonal](media/icon-zonal.svg) |
| [Azure Managed Instance for Apache Cassandra](../managed-instance-apache-cassandra/create-cluster-portal.md) | ![An icon that signifies this service is zone redundant.](media/icon-zone-redundant.svg)  |
| Azure Storage: Ultra Disk | ![An icon that signifies this service is zonal.](media/icon-zonal.svg) |

### ![An icon that signifies this service is non-regional.](media/icon-always-available.svg) Non-regional services (always-available services)

| **Products**   | **Resiliency**   | 
| --- | --- |
| Azure Active Directory  | ![An icon that signifies this service is always available.](media/icon-always-available.svg) |
| Azure Advanced Threat Protection  | ![An icon that signifies this service is always available.](media/icon-always-available.svg) |
| Azure Advisor  | ![An icon that signifies this service is always available.](media/icon-always-available.svg) |
| Azure Blueprints  | ![An icon that signifies this service is always available.](media/icon-always-available.svg) |
| Azure Bot Services  | ![An icon that signifies this service is always available.](media/icon-always-available.svg) |
| Azure Cloud Shell  | ![An icon that signifies this service is always available.](media/icon-always-available.svg) |
| Azure Content Delivery Network  | ![An icon that signifies this service is always available.](media/icon-always-available.svg) |
| Azure Cost Management and Billing | ![An icon that signifies this service is always available.](media/icon-always-available.svg) |
| Microsoft Defender for IoT  | ![An icon that signifies this service is always available.](media/icon-always-available.svg) |
| Azure DNS  | ![An icon that signifies this service is always available.](media/icon-always-available.svg) |
| Azure Front Door  | ![An icon that signifies this service is always available.](media/icon-always-available.svg) |
| Azure Information Protection  | ![An icon that signifies this service is always available.](media/icon-always-available.svg) |
| Azure Lighthouse  | ![An icon that signifies this service is always available.](media/icon-always-available.svg) |
| Azure Managed Applications  | ![An icon that signifies this service is always available.](media/icon-always-available.svg) |
| Azure Maps  | ![An icon that signifies this service is always available.](media/icon-always-available.svg) |
| Azure Peering Service  | ![An icon that signifies this service is always available.](media/icon-always-available.svg) |
| Azure Performance Diagnostics  | ![An icon that signifies this service is always available.](media/icon-always-available.svg) |
| Azure Policy  | ![An icon that signifies this service is always available.](media/icon-always-available.svg) |
| Azure Portal  | ![An icon that signifies this service is always available.](media/icon-always-available.svg) |
| Azure Resource Graph  | ![An icon that signifies this service is always available.](media/icon-always-available.svg) |
| Azure Stack Edge  | ![An icon that signifies this service is always available.](media/icon-always-available.svg) |
| Azure Traffic Manager  | ![An icon that signifies this service is always available.](media/icon-always-available.svg) |
| Customer Lockbox for Microsoft Azure  | ![An icon that signifies this service is always available.](media/icon-always-available.svg) |
| Microsoft Defender for Cloud  | ![An icon that signifies this service is always available.](media/icon-always-available.svg) |
| Microsoft Graph  | ![An icon that signifies this service is always available.](media/icon-always-available.svg) |
| Microsoft Intune  | ![An icon that signifies this service is always available.](media/icon-always-available.svg) |
| Microsoft Sentinel  | ![An icon that signifies this service is always available.](media/icon-always-available.svg) |

For a list of Azure services that support availability zones by Azure region, see the [availability zones documentation](az-overview.md).

## Pricing for virtual machines in availability zones

You can access Azure availability zones by using your Azure subscription. To learn more, see [Bandwidth pricing](https://azure.microsoft.com/pricing/details/bandwidth/).

## Next steps

- [Building solutions for high availability using availability zones](/azure/architecture/high-availability/building-solutions-for-high-availability)
- [High availability with Azure services](/azure/architecture/framework/resiliency/overview)
- [Design patterns for high availability](/azure/architecture/framework/resiliency/app-design)
---
title: Cmdlets de implementación e infraestructura
TOCTitle: Cmdlets de implementación e infraestructura
ms:assetid: 0a6e872a-9f70-4f23-a4a5-8820dbf55370
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398153(v=OCS.15)
ms:contentKeyID: 48274378
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Cmdlets de implementación e infraestructura

 

_**Última modificación del tema:** 2016-12-08_

Los cmdlets de implementación e infraestructura que se incluyen en Microsoft Lync Server 2013 pueden facilitar la instalación e implementación iniciales del producto; después de implementar Lync Server, estos cmdlets son válidos para acciones como comprobar que los componentes funcionen según lo previsto, administrar las opciones de replicación, realizar copias de seguridad, así como restaurar las opciones de configuración, directivas y topologías de Lync Server.

## Cmdlets de implementación e infraestructura

Son muy pocas las ocasiones en que los administradores deben ejecutar cmdlets de implementación e infraestructura. El motivo es que estos cmdlets se invocan automáticamente al ejecutar el programa de instalación o Generador de topologías. (Una excepción destacada podría ser el cmdlet **Export-CsConfiguration**, que permite realizar una copia de seguridad de las opciones de configuración, directivas y topologías de Lync Server). No obstante, si es necesario, los cmdlets de implementación e infraestructura también se pueden ejecutar en el Shell de administración de Lync Server o en un script. El uso de un script permite automatizar algunas tareas. A continuación se presenta una lista de cmdlets directamente relacionados con implementación e infraestructura:

**[Cmdlets de Active Directory](lync-server-2013-active-directory-cmdlets.md)**

  -   
    [Disable-CsAdDomain](disable-csaddomain.md)

  -   
    [Enable-CsAdDomain](enable-csaddomain.md)

  -   
    [Get-CsAdDomain](get-csaddomain.md)

  -   
    [Disable-CsAdForest](disable-csadforest.md)

  -   
    [Enable-CsAdForest](enable-csadforest.md)

  -   
    [Get-CsAdForest](get-csadforest.md)

  -   
    [Get-CsAdServerSchema](get-csadserverschema.md)

  -   
    [Install-CsAdServerSchema](install-csadserverschema.md)

**[Cmdlets de replicación](lync-server-2013-replication-cmdlets.md)**

  -   
    [Debug-CsInterPoolReplication](debug-csinterpoolreplication.md)

  -   
    [Invoke-CsManagementStoreReplication](invoke-csmanagementstorereplication.md)

  -   
    [Get-CsManagementStoreReplicationStatus](get-csmanagementstorereplicationstatus.md)

  -   
    [Enable-CsReplica](enable-csreplica.md)

  -   
    [Test-CsReplica](test-csreplica.md)

  -   
    [Get-CsUserReplicatorConfiguration](get-csuserreplicatorconfiguration.md)

  -   
    [New-CsUserReplicatorConfiguration](new-csuserreplicatorconfiguration.md)

  -   
    [Remove-CsUserReplicatorConfiguration](remove-csuserreplicatorconfiguration.md)

  -   
    [Set-CsUserReplicatorConfiguration](set-csuserreplicatorconfiguration.md)

**[Cmdlets de topología](lync-server-2013-topology-cmdlets.md)**

  -   
    [Get-CsPool](get-cspool.md)

  -   
    [Get-CsSite](get-cssite.md)

  -   
    [Set-CsSite](set-cssite.md)

  -   
    [Enable-CsTopology](enable-cstopology.md)

  -   
    [Get-CsTopology](get-cstopology.md)

  -   
    [Publish-CsTopology](publish-cstopology.md)

  -   
    [Test-CsTopology](test-cstopology.md)

  -   
    [Export-CsConfiguration](export-csconfiguration.md)

  -   
    [Import-CsConfiguration](import-csconfiguration.md)

  -   
    [Get-CsServerVersion](get-csserverversion.md)

  -   
    [Disable-CsComputer](disable-cscomputer.md)

  -   
    [Enable-CsComputer](enable-cscomputer.md)

  -   
    [Get-CsComputer](get-cscomputer.md)

  -   
    [Test-CsComputer](test-cscomputer.md)

  -   
    [Get-CsNetworkInterface](get-csnetworkinterface.md)

**[Cmdlets de copia de seguridad y de alta disponibilidad](lync-server-2013-backup-and-high-availability-cmdlets.md)**

  - [Get-CsBackupServiceConfiguration](get-csbackupserviceconfiguration.md)

  - [Remove-CsBackupServiceConfiguration](remove-csbackupserviceconfiguration.md)

  - [Set-CsBackupServiceConfiguration](set-csbackupserviceconfiguration.md)

  - [Get-CsBackupServiceStatus](get-csbackupservicestatus.md)

  - [Invoke-CsBackupServiceSync](invoke-csbackupservicesync.md)

  - [Debug-CsIntraPoolReplication](debug-csintrapoolreplication.md)

  - [Backup-CsPool](backup-cspool.md)

  - [Get-CsPoolBackupRelationship](get-cspoolbackuprelationship.md)

  - [Get-CsPoolFabricState](get-cspoolfabricstate.md)

  - [Invoke-CsPoolFailBack](invoke-cspoolfailback.md)

  - [Invoke-CsPoolFailOver](invoke-cspoolfailover.md)

  - [Get-CsPoolUpgradeReadinessState](get-cspoolupgradereadinessstate.md)

  - [Invoke-CsStorageServiceFlush](invoke-csstorageserviceflush.md)

  - [Sync-CsUserData](sync-csuserdata.md)

  - [Remove-CsUserStoreBackupData](remove-csuserstorebackupdata.md)

## Vea también

#### Otros recursos

[Blog de Lync Server PowerShell](http://go.microsoft.com/fwlink/?linkid=203150%26clcid=0xc0a)


---
title: Cmdlets de servidor de libreta de direcciones
TOCTitle: Cmdlets de servidor de libreta de direcciones
ms:assetid: 33da45da-3c57-4d04-9679-f0e5a0cfd37e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg415643(v=OCS.15)
ms:contentKeyID: 48274879
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Cmdlets de servidor de libreta de direcciones

 

_**Última modificación del tema:** 2016-12-08_

Los servidores de libreta de direcciones son intermediarios entre Servicios de dominio de Active Directory y Microsoft Lync Server 2013. El servidor de libreta de direcciones comprueba que la información de los usuarios almacenada en Lync Server 2013 esté sincronizada con la información de los usuarios almacenada en Active Directory. Con este fin, sincroniza periódicamente los archivos de libreta de direcciones con la información almacenada en la base de datos de usuarios. A su vez, Lync Server presenta una serie de cmdlets para administrar servidores de libretas de direcciones.

## Cmdlets de servidor de libreta de direcciones

Las opciones de la libreta de direcciones no pueden configurarse en Panel de control de Lync Server. Windows PowerShell es la herramienta principal para administrar estas opciones de configuración. A continuación se presenta una lista de cmdlets directamente relacionados con el servidor de libreta de direcciones:

**Servidor de libreta de direcciones**

  -   
    [Get-CsAddressBookConfiguration](get-csaddressbookconfiguration.md)

  -   
    [New-CsAddressBookConfiguration](new-csaddressbookconfiguration.md)

  -   
    [Remove-CsAddressBookConfiguration](remove-csaddressbookconfiguration.md)

  -   
    [Set-CsAddressBookConfiguration](set-csaddressbookconfiguration.md)

<!-- end list -->

  -   
    [Update-CsAddressBook](update-csaddressbook.md)

  -   
    [Debug-CsAddressBookReplication](debug-csaddressbookreplication.md)

<!-- end list -->

  -   
    [Test-CsAddressBookService](test-csaddressbookservice.md)

  -   
    [Test-CsAddressBookWebQuery](test-csaddressbookwebquery.md)

## Vea también

#### Otros recursos

[Blog de Lync Server PowerShell](http://go.microsoft.com/fwlink/?linkid=203150%26clcid=0xc0a)


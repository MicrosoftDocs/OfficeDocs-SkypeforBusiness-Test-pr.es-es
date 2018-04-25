---
title: Parámetros opcionales y obligatorios
TOCTitle: Parámetros opcionales y obligatorios
ms:assetid: e766362f-e2e9-4598-a595-fdf5eedd9ad6
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362851(v=OCS.15)
ms:contentKeyID: 56271364
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Parámetros opcionales y obligatorios

 

_**Última modificación del tema:** 2015-06-22_

Los parámetros de Windows PowerShell se dividen en dos categorías: obligatorios y opcionales. Los *parámetros obligatorios* son aquellos que deben incluirse al ejecutar un comando. Por ejemplo, el cmdlet [Remove-CsUserAcp](remove-csuseracp.md) se usa para cancelar la asignación de un proveedor de servicios de audioconferencia que anteriormente se había asignado a un usuario. Al ejecutar el cmdlet **the Remove-CsUserAcp**, debe incluir el parámetro Identity, que indica al cmdlet el usuario al que se debe quitar el proveedor de servicios de audioconferencia. Como es obvio, ejecutar este comando sin parámetros no resultará de gran utilidad:

    Remove-CsUserAcp

En un caso como este, el cmdlet no sería capaz de identificar al usuario al que se debe quitar el proveedor. De hecho, es necesario especificar el parámetro Identity del usuario:

    Remove-CsUserAcp -Identity "Ken Myer"

Cuando se intente ejecutar el comando, por lo general Windows PowerShell preguntará si se desea omitir un parámetro obligatorio. Por ejemplo, escriba lo siguiente y presione ENTRAR:

    Remove-CsUserAcp

De realizar así el procedimiento, Windows PowerShell no ejecutará el comando incompleto. En su lugar, le consultará acerca del parámetro obligatorio que falta:

    cmdlet Remove-CsUserAcp en la posición 1 de la canalización de comandos
    Suministre valores para los siguientes parámetros:
    Identidad:

Si escribe un parámetro Identity válido y presiona ENTRAR, Windows PowerShell ejecutará el cmdlet **Remove-CsUserAcp** y quitará al proveedor de servicios de audioconferencia. Si cambia de idea y finalmente decide no ejecutar el comando, presione Ctrl-C para finalizarlo.

En cualquier caso, el sistema no es infalible y Windows PowerShell no siempre solicitará confirmación con relación al conjunto necesario de parámetros. Por ejemplo, algunos cmdlets se construyen de modo que uno de los parámetros A o B (pero no ambos) son obligatorios. Windows PowerShell podría preguntar sobre ambos parámetros (A y B), pero el comando generaría un error porque no se pueden usar los dos parámetros en el mismo comando. Por casos como este, se recomienda incluir todos los parámetros necesarios antes de ejecutar el comando y no confiar en que Windows PowerShell solicitará la información necesaria.

Asimismo, debe tener en cuenta que el proceso de aplicación de formato al valor de parámetro no es excesivamente intuitivo. Por ejemplo, si se incluye un valor de parámetro que contiene un espacio en blanco, deberá delimitarse con comillas dobles:

    -Identity "Ken Myer"

Las comillas solo deben usarse para escribir el parámetro y su valor como parte del comando que debe ejecutarse. Si intenta ejecutar el cmdlet **Remove-CsUserAcp** sin activar el parámetro Identity, Windows PowerShell le preguntará el valor de Identity para el usuario:

    cmdlet Remove-CsUserAcp en la posición 1 de la canalización de comandos
    Suministre valores para los siguientes parámetros:
    Identidad:

A continuación, escriba Ken Myer con el parámetro Identity delimitado por comillas dobles:

    cmdlet Remove-CsUserAcp en la posición 1 de la canalización de comandos
    Suministre valores para los siguientes parámetros:
    Identidad: "Ken Myer"

De hacerlo así, el comando generará un error con el siguiente mensaje:

    Remove-CsUserAcp : No se ha encontrado el objeto de administración para la identidad ""Ken Myer"".

En este caso se ha buscado a un usuario con la identidad de "Ken Myer" y se han incluido las comillas dobles como parte del parámetro Identity. Si se le pide que escriba un valor de parámetro, no incluya las comillas dobles:

    cmdlet Remove-CsUserAcp en la posición 1 de la canalización de comandos
    Suministre valores para los siguientes parámetros:
    Identidad:Ken Myer

En comparación, un *parámetro opcional* es exactamente lo que su nombre indica: el cmdlet puede ejecutarse sin necesidad de escribir este parámetro. Por ejemplo, imaginemos que Remove-CsUserAcp cuenta con el parámetro opcional Name. Si este parámetro se incluye en el comando, solo se quitará al proveedor de servicios de audioconferencia que se haya especificado. Este comando quitará al proveedor llamado Fabrikam ACP, pero no a los demás proveedores que se hayan asignado a Ken Myer:

    Remove-CsUserAcp -Identity "Ken Myer" -Name "Fabrikam ACP"

Si no se activa este parámetro opcional el comando se ejecutará igualmente, aunque, en ese caso, Remove-CsUserAcp eliminará todos los proveedores de servicios de audioconferencia que se hayan asignado a Ken Myer:

    Remove-CsUserAcp -Identity "Ken Myer"

## Vea también

#### Conceptos

[Introducción a Windows PowerShell y Lync Online](an-introduction-to-windows-powershell-and-skype-for-business-online.md)


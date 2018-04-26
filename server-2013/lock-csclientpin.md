---
title: Lock-CsClientPin
TOCTitle: Lock-CsClientPin
ms:assetid: 81a9895f-96e3-43c9-9dac-8129358e446a
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398650(v=OCS.15)
ms:contentKeyID: 48275857
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lock-CsClientPin

 

_**Última modificación del tema:** 2015-03-09_

Permite que un administrador impida a un usuario usar la autenticación por número de identificación personal (PIN). Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Lock-CsClientPin -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

En el ejemplo 1, se usa el cmdlet **Lock-CsClientPin** para bloquear el PIN del usuario kenmyer@litwareinc.com.

    Lock-CsClientPin -Identity "kenmyer@litwareinc.com"

## Ejemplo 2

El ejemplo 2 usa el cmdlet **Lock-CsClientPin** para bloquear los PIN de todos los usuarios que tengan asignado un PIN. Para ello, se usa el cmdlet **Get-CsUser** para devolver una colección de todos los usuarios habilitados para Lync Server. Después, la colección se canaliza al cmdlet **Get-CsClientPinInfo**, que se usa junto con el cmdlet **Where-Object** para devolver una colección de usuarios donde la propiedad IsPinSet sea igual a True. Finalmente, la colección filtrada se canaliza al cmdlet **Lock-CsClientPin**, que bloquea el número PIN de cada usuario de la colección.

    Get-CsUser | Get-CsClientPinInfo | Where-Object {$_.IsPinSet -eq $True} | Lock-CsClientPin

## Ejemplo 3

En el ejemplo 3, se usa el cmdlet **Lock-CsClientPin** para bloquear los PIN de todos los usuarios cuyos PIN hayan expirado. Para llevar a cabo esta tarea, primero se llama al cmdlet **Get-CsUser** para devolver una colección de todos los usuarios habilitados para Lync Server. Después, se canaliza la colección al cmdlet **Get-CsClientPinInfo**, que se usa junto con el cmdlet **Where-Object** para limitar la colección a los usuarios cuyos PIN hayan expirado. Para determinar los usuarios que tienen PIN expirados, el cmdlet **Where-Object** busca las cuentas cuya propiedad PinExpirationTime (que indica la fecha de expiración del PIN) es menor que la fecha actual. (La fecha actual se recupera con el cmdlet **Get-Date**). Si la fecha de expiración (por ejemplo, 1 de septiembre de 2010) es menor que la fecha actual (por ejemplo, 2 de septiembre de 2010), significa que el PIN ha expirado. Después de eso, se usa el cmdlet **Lock-CsClientPin** para bloquear todos los PIN expirados.

    Get-CsUser | Get-CsClientPinInfo | Where-Object {$_.PinExpirationTime -lt (Get-Date)} | Lock-CsClientPin

## Descripción detallada

Lync Server permite a los usuarios conectarse al sistema o unirse a conferencias de red telefónica conmutada (RTC) con un teléfono. Normalmente, para iniciar sesión en el sistema o unirse a una conferencia, el usuario debe especificar su nombre de usuario o contraseña. Sin embargo, escribir un nombre de usuario y contraseña puede suponer un problema en teléfonos que no tienen teclado alfanumérico. Por este motivo, Lync Server le permite proporcionar a los usuarios PIN que solo contengan números; cuando se les pida, los usuarios podrán iniciar sesión en el sistema o unirse a una conferencia introduciendo el PIN en lugar de un nombre de usuario y una contraseña.

Como medida de seguridad, Lync Server permite bloquear el PIN de un usuario. Cuando se bloquea un PIN, el usuario no puede usarlo para obtener acceso al sistema ni participar en una conferencia. (No obstante, podrá obtener acceso al sistema y participar en conferencias si usa una aplicación como Lync 2013 y facilita el nombre de usuario y la contraseña). Una vez bloqueado el PIN, solo podrá restaurarlo (junto con los privilegios de acceso del usuario) un administrador que lo desbloquee. Para ello, puede usar el cmdlet **Unlock-CsClientPin**.

El cmdlet **Lock-CsClientPin** permite a los administradores deshabilitar temporalmente la capacidad de un usuario para obtener acceso al sistema con la autenticación PIN. El sistema también puede bloquear los PIN: si un usuario intenta iniciar sesión en el sistema varias veces sin conseguirlo, se bloqueará automáticamente su PIN y, de nuevo, será necesario que lo desbloquee un administrador.

Tenga en cuenta que, de manera predeterminada, las excepciones de firewall para SQL Server Express no están habilitadas cuando se instala la versión Standard Edition de Lync Server. Por lo tanto, no se podrá ejecutar el cmdlet **Lock-CsClientPin** desde una instancia remota de Windows PowerShell. El motivo es que su comando no podrá atravesar el firewall y obtener acceso a la base de datos SQL Server Express. (No obstante, sí podrá iniciar el cmdlet localmente en el servidor Standard Edition). Para iniciar el cmdlet **Lock-CsClientPin** remotamente, tendrá que habilitar manualmente las excepciones del firewall para SQL Server Express.

Quién puede iniciar este cmdlet: de manera predeterminada, los miembros de los siguientes grupos están autorizados a iniciar localmente el cmdlet **Lock-CsClientPin**: RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluyendo todos los roles RBAC personalizados que haya creado), inicie el siguiente comando desde el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Lock-CsClientPin"}

## Parámetros


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Parámetro</th>
<th>Obligatorio</th>
<th>Tipo</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>Identidad de la cuenta de usuario cuyo PIN hay que bloquear. Las identidades de usuario pueden especificarse con cuatro formatos: 1) la dirección SIP del usuario; 2) el nombre principal del usuario (UPN); 3) el nombre del dominio y el nombre de inicio de sesión del usuario, con formato dominio\nombre (por ejemplo, litwareinc\kenmyer), y 4) el nombre para mostrar de Active Directory del usuario (por ejemplo, Ken Myer). También puede consultar las identidades de usuario con el nombre distintivo Active Directory del usuario.</p>
<p>Además, puede usar el asterisco (*) como carácter comodín al usar el Nombre para mostrar como la identidad del usuario. Por ejemplo, la identidad &quot;* Smith&quot; devuelve todos los usuarios cuyo nombre para mostrar termine con el valor de cadena &quot; Smith&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Suprime la visualización de los mensajes de error que no sean graves que se puedan producir al iniciar el comando.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Describe qué sucedería si se ejecutara el comando sin ejecutarlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Valor de la cadena u objeto Microsoft.Rtc.Management.ADConnect.Schema.ADUser. El cmdlet **Lock-CsClientPin** acepta la entrada canalizada de valores de cadena que representan la identidad de una cuenta de usuario. El cmdlet también acepta la entrada canalizada de objetos de usuario.

## Tipos de valores devueltos

El cmdlet **Lock-CsClientPin** no devuelve ningún valor ni objeto. En su lugar, el cmdlet configura una o más instancias del objeto Microsoft.Rtc.Management.UserPinService.PinInfoDetails.

## Vea también

#### Otros recursos

[Get-CsClientPinInfo](get-csclientpininfo.md)  
[Set-CsClientPin](set-csclientpin.md)  
[Unlock-CsClientPin](unlock-csclientpin.md)


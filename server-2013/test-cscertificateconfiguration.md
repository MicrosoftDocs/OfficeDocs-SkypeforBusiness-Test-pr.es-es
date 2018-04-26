---
title: Test-CsCertificateConfiguration
TOCTitle: Test-CsCertificateConfiguration
ms:assetid: 8086bdf7-d283-4666-9f6c-0d5a3a31b3a6
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398647(v=OCS.15)
ms:contentKeyID: 48275847
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsCertificateConfiguration

 

_**Última modificación del tema:** 2015-03-09_

Devuelve información sobre los certificados de Lync Server que se están usando en el equipo local. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Test-CsCertificateConfiguration [-Report <String>]

## Ejemplos

## Ejemplo 1

El comando que se muestra en el ejemplo 1 devuelve información sobre los certificados que Lync Server está usando actualmente (en el PC local).

    Test-CsCertificateConfiguration

## Ejemplo 2

El comando del ejemplo 2 es una variante del comando del ejemplo 1. No obstante, en este caso se usa el parámetro Report para especificar una ruta de acceso de archivo (C:\\Logs\\Certificates.xml) para el archivo de salida que se genera al ejecutar el cmdlet **Test-CsCertificateConfiguration**.

    Test-CsCertificateConfiguration -Report "C:\Logs\Certificates.xml"

## Descripción detallada

El cmdlet **Test-CsCertificateConfiguration** es un ejemplo de "transacción sintética". Las transacciones sintéticas se usan en Lync Server para comprobar que los usuarios pueden completar correctamente tareas comunes, como iniciar sesión en el sistema, intercambiar mensajes instantáneos o hacer llamadas a teléfonos de la red telefónica conmutada (RTC). Estas pruebas puede hacerlas un administrador de manera manual o iniciarlas automáticamente una aplicación, como Microsoft System Center Operations Manager (anteriormente Microsoft Operations Manager).

El cmdlet **Test-CsCertificateConfiguration** devuelve información sobre los certificados que está usando Lync Server. El cmdlet **Test-CsCertificateConfiguration** está pensado principalmente para que lo use el asistente para certificados. Recomendamos que los administradores usen el cmdlet **Get-CsCertificate** para obtener información sobre los certificados.

Quién puede iniciar este cmdlet: Para obtener una lista de todos los roles de control de acceso basado en roles (RBAC) a los que está asignado este cmdlet (incluyendo todos los roles RBAC personalizados que haya creado), inicie el siguiente comando desde el símbolo del sistema Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsCertificateConfiguration"}

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
<td><p><em>Report</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Permite especificar la ruta de acceso del archivo de registro que se crea al iniciarse el cmdlet. Por ejemplo: -Report &quot;C:\Logs\Certificates.html&quot;. Si este archivo ya existe, se sobrescribirá al iniciar el cmdlet.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno. El cmdlet **Test-CsCertificateConfiguration** no acepta entradas canalizadas.

## Tipos de valores devueltos

El cmdlet **Test-CsCertificateConfiguration** devuelve instancias del objeto Microsoft.Rtc.Management.Deployment,CertificateExists.

## Vea también

#### Otros recursos

[Get-CsCertificate](get-cscertificate.md)


---
title: Administrar al cliente de Lync
TOCTitle: Administrar al cliente de Lync
ms:assetid: d1ccc7b6-99ff-4ffd-bd29-9088fb8fe837
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362847(v=OCS.15)
ms:contentKeyID: 56271360
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Administrar al cliente de Lync

 

_**Última modificación del tema:** 2015-06-22_

Los cmdlets siguientes administran el cliente Lync:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="get-csimfilterconfiguration.md">Get-CsImFilterConfiguration</a></p></td>
<td><p>Recupera información sobre las restricciones de URI en uso en la organización.</p>
<p>Al enviar mensajes instantáneos, los usuarios pueden insertar un URI en el texto del mensaje para indicar un sitio web en particular a otros participantes de la conversación o para compartir. Skype Empresarial Online se puede configurar de modo que los hipervínculos que contengan determinados prefijos se bloqueen o no estén activos. En otras palabras, los participantes no pueden simplemente hacer clic en el vínculo y obtener acceso al sitio al que indica el URI, sino que deben copiar y pegar el vínculo manualmente en un explorador.</p></td>
</tr>
<tr class="even">
<td><p><a href="get-cspresencepolicy.md">Get-CsPresencePolicy</a></p></td>
<td><p>Devuelve información sobre dos aspectos importantes de las suscripciones de presencia: los suscriptores de consulta y las suscripciones de categoría.</p>
<p>Si le agregan a la Lista de contactos de un usuario, recibirá de forma predeterminada una notificación emergente para informarle de que se le ha agregado a esta lista. Mientras no descarte el elemento emergente, todas las notificaciones contarán como suscriptores de consulta.</p>
<p>Las suscripciones de categoría representan una solicitud para una categoría específica de información (por ejemplo, una aplicación que solicita datos del calendario).</p></td>
</tr>
<tr class="odd">
<td><p><a href="get-csprivacyconfiguration.md">Get-CsPrivacyConfiguration</a><br />
<a href="set-csprivacyconfiguration.md">Set-CsPrivacyConfiguration</a></p></td>
<td><p>Configura los valores de privacidad predeterminados de Skype Empresarial Online y permite a los usuarios cambiar estos valores si así lo desean.</p>
<p>Skype Empresarial Online permite a los usuarios compartir volúmenes importantes de información de presencia con otras personas. Los usuarios pueden publicar su propia fotografía, incluir información de ubicación detallada y que su información de presencia se encuentre disponible automáticamente para todos los miembros de una organización (sin limitarse a las personas de sus listas de contactos). Con los cmdlets <strong>CsPrivacyConfiguration</strong>, los administradores pueden configurar los valores de privacidad predeterminados de Skype Empresarial Online y los usuarios pueden cambiar estos valores si así lo desean.</p></td>
</tr>
</tbody>
</table>


Desde el Centro de administración de Skype Empresarial Online también puede administrar un subconjunto de las opciones de configuración de privacidad:

![Configuración del modo privado de presencia en el centro de administración de Lync](images/Dn362847.eb206b74-844d-4a7b-b1b3-0cfcb6e3614b(OCS.15).png "Configuración del modo privado de presencia en el centro de administración de Lync")

## Vea también

#### Conceptos

[Los cmdlets de Lync Online](the-skype-for-business-online-cmdlets.md)  
[Referencia rápida: Realizar tareas de administración comunes de Lync Online con Windows PowerShell](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)


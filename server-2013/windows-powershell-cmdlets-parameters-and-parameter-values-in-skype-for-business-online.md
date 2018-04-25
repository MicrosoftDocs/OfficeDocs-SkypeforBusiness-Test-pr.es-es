---
title: Cmdlets, parámetros y valores de parámetro de Windows PowerShell
TOCTitle: Cmdlets, parámetros y valores de parámetro de Windows PowerShell
ms:assetid: 04615700-099f-4ac5-a801-ddeffccb9e4f
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362765(v=OCS.15)
ms:contentKeyID: 56271259
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Cmdlets, parámetros y valores de parámetro de Windows PowerShell

 

_**Última modificación del tema:** 2015-06-22_

Conocer la ventana de comandos que hay en todas las versiones de Windows (o conocer MS-DOS) supondrá una ventaja cuando quiera empezar a usar Windows PowerShell. En la ventana de comandos, escriba un comando y presione ENTRAR. Como respuesta, el equipo ejecuta un comando o un archivo ejecutable. Por ejemplo, para devolver información sobre todos los archivos y las carpetas que hay en el directorio actual, escriba este comando en el símbolo del sistema y luego presione ENTRAR:

    dir

Al hacerlo, recibe información sobre todos los archivos y las carpetas que hay en el directorio actual:

``` 
    Directory: C:\

03/21/2013  03:39 PM    <DIR>          Deploy
03/21/2013  02:55 PM    <DIR>          Intel
07/26/2012  12:33 AM    <DIR>          PerfLogs
04/10/2013  10:29 AM    <DIR>          Program Files
04/08/2013  10:28 AM    <DIR>          Program Files (x86)
03/22/2013  08:44 AM    <DIR>          Users
04/11/2013  03:00 PM    <DIR>              Windows
03/13/2013  02:53 PM                 117   pldok.log
03/21/2013  03:35 PM                 769   RHDSetup.exe
03/21/2013  03:37 PM            207   setup.doc
              3 File(s)        1,093 bytes
              7 Dir(s)21,386,002,432 bytes free
```

Este ejemplo representa el resultado que se obtiene al escribir solo el nombre de un comando o un archivo ejecutable, pero muchos de los comandos que se ejecutan desde dentro de la ventana de comandos también aceptan *argumentos*. Los argumentos son datos adicionales que se pasan al comando y que modifican su comportamiento. Por ejemplo, si quisiera ver solo los nombres de los archivos y las carpetas que hay en el directorio actual (ningún otro dato más, como el tamaño del archivo o la carpeta, o la fecha y hora en que se creó la carpeta), tendría que anexar el argumento **/b** al ejecutar el comando dir:

    dir /b

Al incluir el argumento **/b**, el comando **dir** solo devuelve los nombres de las carpetas y los archivos encontrados en el directorio actual:

    Deploy
    Intel
    PerfLogs
    Program Files
    Program Files (x86)
    Users
    Windows
    pldok.log
    RHDSetup.exe
    setup.doc

En el comando anterior, el argumento **/b** es la única información necesaria para limitar los datos devueltos a los nombres de archivos y carpetas. Esto es lo que suele suceder con los comandos de la línea de comandos: la presencia de un argumento es lo único necesario para cambiar el comportamiento del comando. (Es decir, se incluye el argumento **/b** para ocultar información adicional o se excluye el argumento **/b** para mostrarla). Sin embargo, en otras ocasiones, se debe especificar un *valor de argumento*. Un valor de argumento es información adicional que se pasa al propio argumento. Por ejemplo, el argumento **/o** le permite especificar cómo quiere que el comando dir ordene los datos devueltos. Entre otras opciones, puede usar el valor de argumento **e** para ordenar por extensión de archivo o el valor de argumento **s** para ordenar por tamaño de archivo. Por ejemplo, el comando siguiente ordena los datos devueltos por extensión de archivo. Observe que el valor de argumento **e** se incluye inmediatamente después del argumento **/o**:

    dir /oe

Usando la carpeta de muestra, los datos devueltos tendrán este aspecto y los archivos estarán ordenados alfabéticamente por extensión de archivo:

``` 
    Directory: C:\

03/21/2013  03:39 PM    <DIR>          Deploy
03/21/2013  02:55 PM    <DIR>          Intel
07/26/2012  12:33 AM    <DIR>          PerfLogs
04/10/2013  10:29 AM    <DIR>          Program Files
04/08/2013  10:28 AM    <DIR>          Program Files (x86)
03/22/2013  08:44 AM    <DIR>          Users
04/11/2013  03:00 PM    <DIR>              Windows
03/21/2013  03:37 PM            207   setup.doc
03/21/2013  03:35 PM                 769   RHDSetup.exe
03/13/2013  02:53 PM                 117   pldok.log
              3 File(s)        1,093 bytes
              7 Dir(s)21,386,002,432 bytes free
```

Vea, a continuación, a qué nos referimos exactamente:

setup. **doc**  
RHDSetup. **exe**  
pldok. **log**

Aunque Windows PowerShell usa una terminología distinta, el método básico para trabajar con Windows PowerShell es el mismo que para trabajar con la ventana de comandos: escriba los comandos, incluya los argumentos y valores de argumento que necesite y presione ENTRAR para ejecutar los comandos. Sin embargo, como hemos destacado, Windows PowerShell usa una terminología diferente de la del Shell de comandos. En Windows PowerShell, los comandos que se ejecutan se denominan *cmdlets*; los argumentos que se pasan al cmdlet, *parámetros*; y los valores que se pasan a un parámetro, *valores de parámetro*.

Las definiciones anteriores se han simplificado un poco. Los cmdlets son, básicamente, miniaplicaciones que solo pueden ejecutarse desde el entorno de Windows PowerShell. Sin embargo, también se pueden ejecutar otros comandos y aplicaciones desde Windows PowerShell, incluidos la mayoría de los comandos y las aplicaciones que se pueden ejecutar desde una ventana de comandos. Por ejemplo, si quiere iniciar Bloc de notas desde Windows PowerShell, solo tiene que escribir lo siguiente y presionar ENTRAR:

    notepad.exe

Sin embargo, para administrar Skype Empresarial Online, la mayoría de los administradores usan los cmdlets de Windows PowerShell para llevar a cabo tareas administrativas. Actualmente, existen muy pocos tipos de comandos o aplicaciones diferentes para administrar Skype Empresarial Online. Algunas veces, los cmdlets de Skype Empresarial Online se pueden usar sin argumentos adicionales (como hemos dicho, los argumentos se llaman parámetros en Windows PowerShell). Por ejemplo, el comando siguiente llama al cmdlet [Get-CsOnlineUser](get-csonlineuser.md) sin ningún parámetro adicional. El comando devuelve, por sí mismo, información sobre todos los usuarios de Skype Empresarial Online:

    Get-CsOnlineUser

Sin embargo, la mayoría de los cmdlets de Skype Empresarial Online también aceptan parámetros (y valores de parámetro). Observe este comando:

    Get-CsOnlineUser -Identity "kenmyer@litwareinc.com"

Este comando tiene tres partes:

  - El cmdlet **Get-CsOnlineUser**.

  - El parámetro Identity. Recuerde que, en Windows PowerShell, los parámetros siempre van precedidos por un guión. Esto significa que, para este mismo cmdlet, el parámetro UnassignedUser se indicaría usando esta sintaxis:
    
        -UnassignedUser
    
    Es útil saber esto no solo porque los parámetros deben ir precedidos por un guión, sino también porque hay una diferencia con la ventana de comandos, donde los argumentos van precedidos por una barra diagonal (/):
    
    ``` 
    /b
    ```

  - El valor de parámetro **kenmyer@litwareinc.com**.

Además, este comando devuelve información sobre un usuario concreto: el usuario cuya identidad es kenmyer@litwareinc.com.

## Vea también

#### Conceptos

[Introducción a Windows PowerShell y Lync Online](an-introduction-to-windows-powershell-and-skype-for-business-online.md)


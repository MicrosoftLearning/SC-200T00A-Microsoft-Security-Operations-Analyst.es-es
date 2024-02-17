---
lab:
  title: 'Ejercicio 5: descripción del modelado de detección'
  module: Learning Path 7 - Create detections and perform investigations using Microsoft Sentinel
---

# Ruta de aprendizaje 7 - Laboratorio 1 - Ejercicio 5: descripción del modelado de detección

![Introducción al laboratorio.](../Media/SC-200-Lab_Diagrams_Mod7_L1_Ex5.png)
### Tarea 1: comprender los ataques

>**Importante: no realizarás ninguna acción en este ejercicio.**  Estas instrucciones son solo una explicación de los ataques que realizarás en el ejercicio siguiente. Lee detenidamente esta página.

Los patrones de ataque se basan en un proyecto de código abierto: https://github.com/redcanaryco/atomic-red-team


#### Ataque 1: persistencia con la agregación de clave del registro

Los atacantes agregarán un programa en la clave Ejecutar registro. De esta manera, se obtiene persistencia haciendo que el programa se ejecute cada vez que el usuario inicia sesión.

```
REG ADD "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run" /V "SOC Test" /t REG_SZ /F /D "C:\temp\startup.bat"
```

#### Ataque 2: agregación de usuarios y privilegio elevado

Los atacantes agregarán nuevos usuarios y elevarán el nuevo usuario al grupo de administradores. Esto permite al atacante iniciar sesión con una cuenta diferente con privilegios.

```
net user theusernametoadd /add
net user theusernametoadd ThePassword1!
net localgroup administrators theusernametoadd /add
```

#### Ataque 3: DNS / C2 

El atacante enviará un gran volumen de consultas DNS a un servidor de comando y control (C2). La intención es desencadenar la detección basada en umbral en el número de consultas DNS desde un único sistema de origen o en un único dominio de destino.

```
param(
    [string]$Domain = "microsoft.com",
    [string]$Subdomain = "subdomain",
    [string]$Sub2domain = "sub2domain",
    [string]$Sub3domain = "sub3domain",
    [string]$QueryType = "TXT",
        [int]$C2Interval = 8,
        [int]$C2Jitter = 20,
        [int]$RunTime = 240
)
$RunStart = Get-Date
$RunEnd = $RunStart.addminutes($RunTime)
$x2 = 1
$x3 = 1 
Do {
    $TimeNow = Get-Date
    Resolve-DnsName -type $QueryType $Subdomain".$(Get-Random -Minimum 1 -Maximum 999999)."$Domain -QuickTimeout
    if ($x2 -eq 3 )
    {
        Resolve-DnsName -type $QueryType $Sub2domain".$(Get-Random -Minimum 1 -Maximum 999999)."$Domain -QuickTimeout
        $x2 = 1
    }
    else
    {
        $x2 = $x2 + 1
    }
    if ($x3 -eq 7 )
    {
        Resolve-DnsName -type $QueryType $Sub3domain".$(Get-Random -Minimum 1 -Maximum 999999)."$Domain -QuickTimeout
        $x3 = 1
    }
    else
    {
        $x3 = $x3 + 1
    }
    $Jitter = ((Get-Random -Minimum -$C2Jitter -Maximum $C2Jitter) / 100 + 1) +$C2Interval
    Start-Sleep -Seconds $Jitter
}
Until ($TimeNow -ge $RunEnd)
```


### Tarea 2: entender el modelado de detección

El ciclo de configuración de detección de ataques usado en este laboratorio representa todos los orígenes de datos, aunque solo se centre en dos orígenes de datos específicos.

Para crear una detección, empieza por crear primero una instrucción KQL. Como atacarás a un host, tendrás datos representativos para empezar a compilar la instrucción KQL.


Una vez que tengas la instrucción KQL, crea la regla analítica.

Una vez que la regla se desencadena y crea las alertas e incidentes, investiga para decidir si proporcionas campos que ayuden a los analistas de operaciones de seguridad en su investigación.

Después, realizarás otros cambios en la regla de análisis.

>**Nota:** algunas alertas se desencadenarán en un período más corto solo a los fines de este laboratorio.

## Continúa con el ejercicio 6

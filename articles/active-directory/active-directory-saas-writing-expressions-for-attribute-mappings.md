---
title: Escritura de expresiones para asignaciones de atributos en Azure Active Directory | Microsoft Azure
description: Obtenga información sobre cómo usar asignaciones de expresiones para transformar valores de atributos en un formato aceptable durante el aprovisionamiento automático de objetos de aplicaciones SaaS en Azure Active Directory.
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: mtillman
ms.assetid: b13c51cd-1bea-4e5e-9791-5d951a518943
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2018
ms.author: markvi
ms.openlocfilehash: f1cf83044eb4f001ba341cabd0771b267c3f996d
ms.sourcegitcommit: 59914a06e1f337399e4db3c6f3bc15c573079832
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/20/2018
---
# <a name="writing-expressions-for-attribute-mappings-in-azure-active-directory"></a>Escritura de expresiones para la asignación de atributos en Azure Active Directory
Al configurar el aprovisionamiento para una aplicación SaaS, uno de los tipos de asignaciones de atributos que puede especificar es una asignación de expresiones. En estos casos, debe escribir una expresión similar a un script que permite transformar los datos de los usuarios en formatos más aceptables para la aplicación SaaS.

## <a name="syntax-overview"></a>Información general sobre la sintaxis
La sintaxis de expresiones para asignaciones de atributos recuerda a las funciones de Visual Basic para Aplicaciones (VBA).

* Toda la expresión se tiene que definir en términos de funciones, que constan de un nombre seguido de argumentos entre paréntesis:  <br>
  *NombreDeFunción (<<argumento 1>>,<<argument N>>)*
* Es posible anidar funciones dentro de otras. Por ejemplo:  <br> *FunciónUno(FunciónDos(&lt;<argument1>&gt;))*
* Puede transformar tres tipos diferentes de argumentos en funciones:
  
  1. Atributos, que deben ir entre corchetes. Por ejemplo: [NombreAtributo]
  2. Constantes de cadena, que deben ir entre comillas. Por ejemplo: "Estados Unidos"
  3. Otras funciones. Por ejemplo: FunciónUna(<<argument1>>, FunciónDos(<<argument2>>))
* Para las constantes de cadena, si necesita una barra diagonal inversa (\) o comillas dobles (") en la cadena, se deben convertirse con el símbolo de barra diagonal inversa (\). Por ejemplo: "Company name: \"Contoso\""

## <a name="list-of-functions"></a>Lista de funciones
[Append](#append) &nbsp;&nbsp;&nbsp;&nbsp; [FormatDateTime](#formatdatetime) &nbsp;&nbsp;&nbsp;&nbsp; [Join](#join) &nbsp;&nbsp;&nbsp;&nbsp; [Mid](#mid) &nbsp;&nbsp;&nbsp;&nbsp; [Not](#not) &nbsp;&nbsp;&nbsp;&nbsp; [Replace](#replace) &nbsp;&nbsp;&nbsp;&nbsp; [SingleAppRoleAssignment](#singleapproleassignment)&nbsp;&nbsp;&nbsp;&nbsp; [StripSpaces](#stripspaces) &nbsp;&nbsp;&nbsp;&nbsp; [Switch](#switch)

- - -
### <a name="append"></a>Append
**Función:**<br> Append(source, suffix)

**Descripción:**<br> adopta un valor de la cadena de origen y anexa el sufijo al final de la misma.

**Parámetros:**<br> 

| NOMBRE | Obligatorio/Repetición | Escriba | Notas |
| --- | --- | --- | --- |
| **de origen** |Obligatorio |string |Normalmente el nombre del atributo del objeto de origen |
| **suffix** |Obligatorio |string |La cadena que se va a anexar al final del valor de origen. |

- - -
### <a name="formatdatetime"></a>FormatDateTime
**Función:**<br> FormatDateTime(source, inputFormat, outputFormat)

**Descripción:**<br> adopta una cadena de fecha en un formato y la convierte a un formato distinto.

**Parámetros:**<br> 

| NOMBRE | Obligatorio/Repetición | Escriba | Notas |
| --- | --- | --- | --- |
| **de origen** |Obligatorio |string |Normalmente el nombre del atributo del objeto de origen. |
| **inputFormat** |Obligatorio |string |Formato esperado del valor de origen. Para conocer los formatos admitidos, consulte [http://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx](http://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx). |
| **outputFormat** |Obligatorio |string |Formato de la fecha de salida. |

- - -
### <a name="join"></a>Unión
**Función:**<br> Join(separator, source1, source2, …)

**Descripción:**<br> Join() es similar a Append(), excepto en que puede combinar varios valores de cadena de **source** en una sola cadena, y cada valor estará separado por una cadena de **separator**.

Si uno de los valores de origen es un atributo multivalor, cada valor de ese atributo se une, separado del valor del separador.

**Parámetros:**<br> 

| NOMBRE | Obligatorio/Repetición | Escriba | Notas |
| --- | --- | --- | --- |
| **separator** |Obligatorio |string |Cadena utilizada para separar los valores de origen cuando se concatenan en una sola cadena. Puede ser "" si no es necesario ningún separador. |
| **origen1  … origenN ** |Obligatorio, número variable de veces |string |Valores de cadena que se van a agrupar. |

- - -
### <a name="mid"></a>Mid
**Función:**<br> Mid(source, start, length)

**Descripción:**<br> devuelve una subcadena del valor de origen. Una subcadena es una cadena que contiene sólo algunos de los caracteres de la cadena de origen.

**Parámetros:**<br> 

| NOMBRE | Obligatorio/Repetición | Escriba | Notas |
| --- | --- | --- | --- |
| **de origen** |Obligatorio |string |Normalmente el nombre del atributo. |
| **start** |Obligatorio |integer |Índice de la cadena de **source** donde debe empezar la subcadena. El primer carácter de la cadena tendrá el índice de 1, el segundo carácter tendrá el índice de 2, y así sucesivamente. |
| **length** |Obligatorio |integer |Longitud de la subcadena. Si length acaba fuera de la cadena de **source**, la función devolverá una subcadena desde el índice de **start** hasta el final de la cadena de **source**. |

- - -
### <a name="not"></a>not
**Función:**<br> Not(source)

**Descripción:**<br> Invierte el valor booleano de **source**. Si el valor de **source** es "*True*", devuelve "*False*". De lo contrario, devuelve "*True*".

**Parámetros:**<br> 

| NOMBRE | Obligatorio/Repetición | Escriba | Notas |
| --- | --- | --- | --- |
| **de origen** |Obligatorio |Cadena booleana |Los valores de **source** esperados son "True" o "False". |

- - -
### <a name="replace"></a>Replace
**Función:**<br> Replace(source, oldValue, regexPattern, regexGroupName, replacementValue, replacementAttributeName, template)

**Descripción:**<br>
Reemplaza valores dentro de una cadena. Funciona de forma diferente dependiendo de los parámetros proporcionados:

* Cuando se proporcionan **oldValue** y **replacementValue**:
  
  * Reemplaza todas las ocurrencias de oldValue en el origen por replacementValue
* Cuando se proporcionan **oldValue** y **template**:
  
  * Reemplaza todas las ocurrencias de **oldValue** en **template** por el valor de **source**
* Cuando se proporcionan **regexPattern**, **regexGroupName** y **replacementValue**:
  
  * Reemplaza todos los valores que coinciden en oldValueRegexPattern en la cadena de origen con replacementValue
* Cuando se proporcionan **regexPattern**, **regexGroupName** y **replacementPropertyName**:
  
  * Si **source** no tiene un valor, se devuelve **source**.
  * Si **source** no tiene un valor, usa **regexPattern** y **regexGroupName** para extraer un valor de sustitución de la propiedad con **replacementPropertyName**. El valor de reemplazo se devuelve como resultado

**Parámetros:**<br> 

| NOMBRE | Obligatorio/Repetición | Escriba | Notas |
| --- | --- | --- | --- |
| **de origen** |Obligatorio |string |Normalmente el nombre del atributo del objeto de origen. |
| **oldValue** |Opcional |string |Valor que se va a reemplazar en **source** o **template**. |
| **regexPattern** |Opcional |string |Patrón Regex del valor que se va a reemplazar en **source**. O bien, cuando se utiliza replacementPropertyName, patrón para extraer el valor de la propiedad de reemplazo. |
| **regexGroupName** |Opcional |string |Nombre del grupo dentro de **regexPattern**. Sólo cuando se utilice replacementPropertyName, extraeremos el valor de este grupo como replacementValue de la propiedad de reemplazo. |
| **replacementValue** |Opcional |string |Nuevo valor para  reemplazar uno anterior. |
| **replacementAttributeName** |Opcional |string |Nombre del atributo que se utilizará para el valor de reemplazo, cuando el origen no tiene ningún valor. |
| **template** |Opcional |string |Cuando se proporcione el valor de **template**, buscaremos **oldValue** dentro de la plantilla y lo reemplazaremos por el valor de origen. |

- - -
### <a name="singleapproleassignment"></a>SingleAppRoleAssignment
**Función:**<br> SingleAppRoleAssignment([appRoleAssignments])

**Descripción:**<br> Devuelve una única función appRoleAssignment de la lista de todas las funciones appRoleAssignments asignadas a un usuario para una aplicación determinada. Esta función es necesaria para convertir el objeto appRoleAssignments en una cadena de nombre de rol único. Tenga en cuenta que el procedimiento recomendado consiste en asegurarse de que solo una función appRoleAssignment esté asignada a un usuario a la vez. Si se asignan varios roles, la cadena del rol devuelta podría no ser predecible.

**Parámetros:**<br> 

| NOMBRE | Obligatorio/Repetición | Escriba | Notas |
| --- | --- | --- | --- |
| **[appRoleAssignments]** |Obligatorio |string |Objeto **[appRoleAssignments]**. |

- - -
### <a name="stripspaces"></a>StripSpaces
**Función:**<br> StripSpaces(source)

**Descripción:**<br> quita todos los caracteres de espacio (" ") de la cadena de origen.

**Parámetros:**<br> 

| NOMBRE | Obligatorio/Repetición | Escriba | Notas |
| --- | --- | --- | --- |
| **de origen** |Obligatorio |string |**de origen** que se actualiza. |

- - -
### <a name="switch"></a>Switch
**Función:**<br> Switch(source, defaultValue, key1, value1, key2, value2, …)

**Descripción:**<br> Cuando el valor de **source** coincide con una **key**, devuelve el **value** de dicha **key**. Si el valor de **source** no coincide con ninguna clave, devuelve **defaultValue**.  Los parámetros **key** y **value** siempre deben estar emparejados. La función espera siempre un número par de parámetros.

**Parámetros:**<br> 

| NOMBRE | Obligatorio/Repetición | Escriba | Notas |
| --- | --- | --- | --- |
| **de origen** |Obligatorio |string |**Source** que se actualiza. |
| **defaultValue** |Opcional |string |Valor predeterminado que se usará si el origen no coincide con ninguna clave. Puede tratarse de una cadena vacía (""). |
| **key** |Obligatorio |string |**Key** con que se compara el valor de **source**. |
| **value** |Obligatorio |string |Valor de reemplazo para el **source** que coincide con la clave. |

## <a name="examples"></a>Ejemplos
### <a name="strip-known-domain-name"></a>Seccionar un nombre de dominio conocido
Debe seccionar un nombre de dominio conocido de correo electrónico de un usuario para obtener un nombre de usuario. <br>
Por ejemplo, si el dominio es "contoso.com", puede usar la expresión siguiente:

**Expresión:** <br>
`Replace([mail], "@contoso.com", , ,"", ,)`

**Ejemplo de entrada y salida:** <br>

* **ENTRADA** (mail): "john.doe@contoso.com"
* **SALIDA**: "john.doe"

### <a name="append-constant-suffix-to-user-name"></a>Anexar sufijos constantes a nombres de usuario
Si está utilizando un espacio aislado de Salesforce, deberá anexar un sufijo adicional a los nombres de usuario antes de sincronizarlas.

**Expresión:** <br>
`Append([userPrincipalName], ".test"))`

**Entrada/salida de ejemplo:** <br>

* **ENTRADA**: (userPrincipalName): "John.Doe@contoso.com"
* **ENTRADA**:  "John.Doe@contoso.com.test"

### <a name="generate-user-alias-by-concatenating-parts-of-first-and-last-name"></a>Generar el alias de usuario concatenando partes de nombre y apellidos
Debe generar un alias de usuario con las tres primeras letras del nombre del usuario y las cinco primeras letras del apellido del usuario.

**Expresión:** <br>
`Append(Mid([givenName], 1, 3), Mid([surname], 1, 5))`

**Entrada/salida de ejemplo:** <br>

* **ENTRADA** (givenName): "John"
* **ENTRADA** (surname): "Doe"
* **SALIDA**: "JohDoe"

### <a name="remove-diacritics-from-a-string-and-convert-to-lowercase"></a>Eliminación de los signos diacríticos de una cadena y su conversión a minúsculas
Debe quitar los caracteres especiales de una cadena y convertir los caracteres en mayúsculas a minúsculas.

**Expresión:** <br>
`Replace(Replace(Replace(Replace(Replace(Replace(Replace( Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace( Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace([givenName], , "([Øø])", , "oe", , ), , "[Ææ]", , "ae", , ), , "([äãàâãåáąÄÃÀÂÃÅÁĄA])", , "a", , ), , "([B])", , "b", , ), , "([CçčćÇČĆ])", , "c", , ), , "([ďĎD])", , "d", , ), , "([ëèéêęěËÈÉÊĘĚE])", , "e", , ), , "([F])", , "f", , ), , "([G])", , "g", , ), , "([H])", , "h", , ), , "([ïîìíÏÎÌÍI])", , "i", , ), , "([J])", , "j", , ), , "([K])", , "k", , ), , "([ľłŁĽL])", , "l", , ), , "([M])", , "m", , ), , "([ñńňÑŃŇN])", , "n", , ), , "([öòőõôóÖÒŐÕÔÓO])", , "o", , ), , "([P])", , "p", , ), , "([Q])", , "q", , ), , "([řŘR])", , "r", , ), , "([ßšśŠŚS])", , "s", , ), , "([TŤť])", , "t", , ), , "([üùûúůűÜÙÛÚŮŰU])", , "u", , ), , "([V])", , "v", , ), , "([W])", , "w", , ), , "([ýÿýŸÝY])", , "y", , ), , "([źžżŹŽŻZ])", , "z", , ), " ", , , "", , )`

**Entrada/salida de ejemplo:** <br>

* **ENTRADA** (givenName): "Zoë"
* **SALIDA**: "zoe"

### <a name="output-date-as-a-string-in-a-certain-format"></a>Fecha de resultado como una cadena en un formato determinado
Desea enviar las fechas a una aplicación SaaS con un formato determinado. <br>
Por ejemplo, desea dar formato a las fechas de ServiceNow.

**Expresión:** <br>

`FormatDateTime([extensionAttribute1], "yyyyMMddHHmmss.fZ", "yyyy-MM-dd")`

**Entrada/salida de ejemplo:**

* **ENTRADA** (extensionAttribute1): "20150123105347.1Z"
* **SALIDA**: "2015-01-23"

### <a name="replace-a-value-based-on-predefined-set-of-options"></a>Reemplazar un valor basado en un conjunto predefinido de opciones
Debe definir la zona horaria del usuario según el código de estado almacenado en Azure AD. <br>
Si el código de estado no coincide con ninguna de las opciones predefinidas, use el valor predeterminado de "Australia/Sídney".

**Expresión:** <br>

`Switch([state], "Australia/Sydney", "NSW", "Australia/Sydney","QLD", "Australia/Brisbane", "SA", "Australia/Adelaide")`

**Entrada/salida de ejemplo:**

* **ENTRADA** (state): "QLD"
* **SALIDA**: "Australia/Brisbane"

## <a name="related-articles"></a>Artículos relacionados
* [Índice de artículos sobre la administración de aplicaciones en Azure Active Directory](active-directory-apps-index.md)
* [Automatización del aprovisionamiento y desaprovisionamiento de usuarios para aplicaciones SaaS con Azure Active Directory](active-directory-saas-app-provisioning.md)
* [Personalización de asignaciones de atributos para el aprovisionamiento de usuarios](active-directory-saas-customizing-attribute-mappings.md)
* [Filtros de ámbito para el aprovisionamiento de usuario](active-directory-saas-scoping-filters.md)
* [Uso de SCIM para habilitar el aprovisionamiento automático de usuarios y grupos de Azure Active Directory a aplicaciones](active-directory-scim-provisioning.md)
* [Notificaciones de aprovisionamiento de cuentas](active-directory-saas-account-provisioning-notifications.md)
* [Lista de tutoriales sobre cómo integrar aplicaciones SaaS](active-directory-saas-tutorial-list.md)


---
title: Modelos personalizados
titleSuffix: Azure Digital Twins
description: Descubra cómo Azure Digital Twins usa modelos definidos por el usuario para describir las entidades del entorno.
author: baanders
ms.author: baanders
ms.date: 3/12/2020
ms.topic: conceptual
ms.service: digital-twins
ms.openlocfilehash: ab0b08c01478d1375ec2a234dc0277980312f17c
ms.sourcegitcommit: dabd9eb9925308d3c2404c3957e5c921408089da
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2020
ms.locfileid: "86258279"
---
# <a name="understand-twin-models-in-azure-digital-twins"></a>Descripción de los modelos gemelos de Azure Digital Twins

Una característica clave de Azure Digital Twins es la capacidad de definir su propio vocabulario y crear el grafo de gemelos en los términos de la empresa definidos de manera automática. Esta funcionalidad la proporcionan los **modelos** definidos por el usuario. Puede considerar los modelos como los nombres de una descripción de su mundo. 

Un modelo es similar a una **clase** en un lenguaje de programación orientado a objetos, el que define una forma de datos para un concepto determinado en el entorno de trabajo real. Los modelos tienen nombres (como *Sala* o *SensorDeTemperatura*) y contienen elementos como propiedades, telemetría/eventos y comandos que describen lo que puede hacer este tipo de entidad en el entorno. Más adelante usará estos modelos para crear [**gemelos digitales**](concepts-twins-graph.md) que representen entidades específicas que cumplan con esta descripción de tipo.

Los modelos se escriben con el **lenguaje de definición de gemelos digitales (DTDL)** basado en JSON-LD.  

## <a name="digital-twin-definition-language-dtdl-for-writing-models"></a>Lenguaje de definición de gemelos digitales (DTDL) para escribir modelos

Los modelos de Azure Digital Twins se definen con el lenguaje de definición de gemelos digitales (DTDL). DTDL se basa en JSON-LD y es independiente del lenguaje de programación. DTDL no es exclusivo de Azure Digital Twins, sino que también se usa para presentar datos de dispositivo en otros servicios de IoT, como [IoT Plug and Play](../iot-pnp/overview-iot-plug-and-play.md). Azure Digital Twins usa la *versión 2* de DTDL.

> [!TIP] 
> No todos los servicios que usan DTDL implementan las mismas características exactas de DTDL. Por ejemplo, IoT Plug and Play no usa las características de DTDL que son para los grafos, mientras que Azure Digital Twins no implementa actualmente comandos de DTDL. Para más información sobre las características de DTDL que son específicas para Azure Digital Twins, consulte la sección que aparece más adelante en este artículo sobre los [detalles específicos de la implementación de DTDL de Azure Digital Twins](#azure-digital-twins-dtdl-implementation-specifics).

Para más información sobre DTDL en general, consulte la documentación de especificaciones en GitHub: [Lenguaje de definición de gemelos digitales (DTDL): versión 2](https://github.com/Azure/opendigitaltwins-dtdl/blob/master/DTDL/v2/dtdlv2.md).

## <a name="elements-of-a-model"></a>Elementos de un modelo

Dentro de una definición de modelo, el elemento de código de nivel superior es una **interfaz**. Encapsula todo el modelo y el resto del modelo se define dentro de la interfaz. 

Una interfaz de modelo de DTDL puede contener cero, uno o varios de los campos siguientes:
* **Propiedad**: las propiedades son campos de datos que representan el estado de una entidad (como las propiedades de muchos lenguajes de programación orientados a objetos). A diferencia de la telemetría, que es un evento de datos con límite temporal, las propiedades tienen almacenamiento de seguridad y se pueden leer en cualquier momento.
* **Telemetría**: los campos de telemetría representan medidas o eventos y a menudo se usan para describir las lecturas de los sensores del dispositivo. La telemetría no se almacena en un gemelo digital, sino más bien es similar a una secuencia de eventos de datos lista para enviarla a algún lugar. 
* **Componente**: los componentes permiten compilar la interfaz de modelo como un ensamblado de otras interfaces, si lo desea. Un ejemplo de componente es una interfaz *cámaraFrontal* (y otra interfaz de componente *cámaraPosterior*) que se usa para definir un modelo para un *teléfono*. Primero debe definir una interfaz para *cámaraFrontal* como si fuera su propio modelo y, luego, puede hacer referencia a ella al definir el *Teléfono*.

    Use un componente para describir algo que es una parte integral de la solución, pero no necesita una identidad independiente y no es necesario crearla, eliminarla ni reorganizarla en el grafo de gemelos de forma independiente. Si quiere que las entidades tengan existencias independientes en el grafo de gemelos, represéntelas como gemelos digitales independientes de distintos modelos, conectadas por *relaciones* (consulte la viñeta siguiente).
    
    >[!TIP] 
    >Los componentes también se pueden usar para la organización, a fin de agrupar conjuntos de propiedades relacionadas dentro de una interfaz de modelo. En esta situación, puede considerar cada componente como un espacio de nombres o "carpeta" dentro de la interfaz.
* **Relación**: las relaciones permiten representar cómo un gemelo digital puede estar implicado con otros gemelos digitales. Las relaciones pueden representar distintos significados semánticos, como *contains* ("floor contains room"), *cools* ("hvac cools room"), *isBilledTo* ("compressor is billed to user"), etc. Las relaciones permiten que la solución proporcione un grafo de las entidades interrelacionadas.

> [!NOTE]
> La especificación de DTDL también define **comandos**, que son métodos que se pueden ejecutar en un gemelo digital (como un comando de restablecimiento o un comando para encender o apagar un ventilador). Sin embargo, *en este momento no se admiten comandos en Azure Digital Twins*.

### <a name="azure-digital-twins-dtdl-implementation-specifics"></a>Detalles específicos de la implementación de DTDL de Azure Digital Twins

Para que un modelo de DTDL sea compatible con Azure Digital Twins, debe cumplir estos requisitos.

* Todos los elementos de DTDL de nivel superior de un modelo deben ser de tipo *interfaz*. Esto se debe a que las API del modelo de Azure Digital Twins pueden recibir objetos JSON que representan una interfaz o una matriz de interfaces. Como resultado, no se permite ningún otro tipo de elemento de DTDL en el nivel superior.
* DTDL para Azure Digital Twins no debe definir ningún *comando*.
* Azure Digital Twins solo permite un único nivel de anidamiento de componente. Esto significa que una interfaz que se usa como componente no puede tener ningún componente. 
* Las interfaces no pueden ser definidas insertadas en línea dentro de otras interfaces de DTDL, sino que deben definirse como entidades independientes de nivel superior con sus propios identificadores. A continuación, cuando otra interfaz quiere incluir esa interfaz como componente o a través de la herencia, puede hacer referencia a su identificador.

## <a name="example-model-code"></a>Código de modelo de ejemplo

Los modelos de tipo gemelo se pueden escribir en cualquier editor de texto. El lenguaje DTDL sigue la sintaxis JSON, por lo que debe almacenar los modelos con la extensión *.json*. El uso de la extensión JSON permitirá que muchos editores de texto de programación proporcionen comprobación de sintaxis básica y resaltado para los documentos de DTDL. También hay una [extensión de DTDL](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-dtdl) disponible para [Visual Studio Code](https://code.visualstudio.com/).

Este es un ejemplo de un modelo típico, escrito como una interfaz DTDL. El modelo describe los planetas, cada uno con nombre, masa y temperatura. El planeta puede tener lunas como satélites y puede contener cráteres.

```json
[
  {
    "@id": "dtmi:com:contoso:Planet;1",
    "@type": "Interface",
    "@context": "dtmi:dtdl:context;2",
    "displayName": "Planet",
    "contents": [
      {
        "@type": "Property",
        "name": "name",
        "schema": "string"
      },
      {
        "@type": "Property",
        "name": "mass",
        "schema": "double"
      },
      {
        "@type": "Telemetry",
        "name": "Temperature",
        "schema": "double"
      },
      {
        "@type": "Relationship",
        "name": "satellites",
        "target": "dtmi:com:contoso:Moon;1"
      },
      {
        "@type": "Component",
        "name": "deepestCrater",
        "schema": "dtmi:com:contoso:Crater;1"
      }
    ]
  },
  {
    "@id": "dtmi:com:contoso:Crater;1",
    "@type": "Interface",
    "@context": "dtmi:dtdl:context;2"
  }
]
```

Los campos del modelo son los siguientes:

| Campo | Descripción |
| --- | --- |
| `@id` | Identificador del modelo. Debe tener el formato `dtmi:<domain>:<unique model identifier>;<model version number>`. |
| `@type` | Identifica el tipo de información que se describe. En el caso de una interfaz, el tipo es *Interfaz*. |
| `@context` | Establece el [contexto](https://niem.github.io/json/reference/json-ld/context/) del documento JSON. Los modelos deben usar `dtmi:dtdl:context;2`. |
| `displayName` | [opcional] Permite asignar un nombre descriptivo al modelo, si lo desea. |
| `contents` | Todos los datos restantes de la interfaz se colocan aquí, como una matriz de definiciones de atributo. Cada atributo debe proporcionar un elemento `@type` (*Propiedad*, *Telemetría*, *Comando*, *Relación* o *Componente*) para identificar el tipo de información de interfaz que describe y, luego, un conjunto de propiedades que definen el atributo real (por ejemplo, `name` y `schema` para definir una *Propiedad*). |

> [!NOTE]
> Tenga en cuenta que la interfaz de componente (em este ejemplo, *Cráter*) se define en la misma matriz que la interfaz que la usa (*Planeta*). Los componentes se deben definir de esta manera en las llamadas API para encontrar la interfaz.

### <a name="possible-schemas"></a>Esquemas posibles

Según DTDL, el esquema de los atributos *Propiedad* y *Telemetría* puede ser de tipos primitivos estándar, `integer`, `double`, `string` y `Boolean`, y otros tipos como `DateTime` y `Duration`. 

Además de los tipos primitivos, los campos *Propiedad* y *Telemetría* pueden tener estos tipos complejos:
* `Object`
* `Map`
* `Enum`

Los campos *Telemetría* también admiten `Array`.

### <a name="model-inheritance"></a>Herencia de modelo

En algunas ocasiones, puede que quiera especializar aún más un modelo. Por ejemplo, podría resultar útil tener un modelo genérico *Sala* y las variantes especializadas *SalaDeConferencias* y *Gimnasio*. Para expresar la especialización, DTDL admite la herencia: las interfaces pueden heredar de una o varias interfaces. 

En el ejemplo siguiente se recrea el modelo *Planeta* del ejemplo de DTDL anterior como subtipo de un modelo *CuerpoCelestial* más grande. Primero se define el modelo "primario" y, a continuación, el modelo "secundario" se basa en él mediante el campo `extends`.

```json
[
  {
    "@id": "dtmi:com:contoso:CelestialBody;1",
    "@type": "Interface",
    "@context": "dtmi:dtdl:context;2",
    "displayName": "Celestial body",
    "contents": [
      {
        "@type": "Property",
        "name": "name",
        "schema": "string"
      },
      {
        "@type": "Property",
        "name": "mass",
        "schema": "double"
      },
      {
        "@type": "Telemetry",
        "name": "temperature",
        "schema": "double"
      }
    ]
  },
  {
    "@id": "dtmi:com:contoso:Planet;1",
    "@type": "Interface",
    "@context": "dtmi:dtdl:context;2",
    "displayName": "Planet",
    "extends": "dtmi:com:contoso:CelestialBody;1",
    "contents": [
      {
        "@type": "Relationship",
        "name": "satellites",
        "target": "dtmi:com:contoso:Moon;1"
      },
      {
        "@type": "Component",
        "name": "deepestCrater",
        "schema": "dtmi:com:contoso:Crater;1"
      }
    ]
  },
  {
    "@id": "dtmi:com:contoso:Crater;1",
    "@type": "Interface",
    "@context": "dtmi:dtdl:context;2"
  }
]
```

En este ejemplo, *CuerpoCelestial* aporte un nombre, una masa y una temperatura a *Planeta*. La sección `extends` es un nombre de interfaz o una matriz de nombres de interfaz (lo que permite que la interfaz de extensión herede de varios modelos primarios si lo desea).

Una vez que se aplica la herencia, la interfaz de extensión expone todas las propiedades de toda la cadena de herencia.

La interfaz de extensión no puede cambiar ninguna de las definiciones de las interfaces primarias; solo puede agregar a ellas. Tampoco puede volver a definir una funcionalidad que ya esté definida en ninguna de sus interfaces primarias (incluso si las funcionalidades están definidas para ser iguales). Por ejemplo, si una interfaz primaria define una propiedad `double` *masa*, la interfaz de extensión no puede contener una declaración de *masa*, incluso si también es `double`.

## <a name="validating-models"></a>Validación de modelos

> [!TIP]
> Se recomienda validar los modelos sin conexión antes de cargarlos en la instancia de Azure Digital Twins.

Hay un ejemplo disponible para todos los lenguajes que sirve para validar los documentos del modelo para garantizar que DTDL sea correcto. Se encuentra aquí: [**Ejemplo de validador de DTDL**](https://docs.microsoft.com/samples/azure-samples/dtdl-validator/dtdl-validator).

El ejemplo de validador de DTDL se basa en una biblioteca de analizador de DTDL de .NET, que está disponible en NuGet como una biblioteca de cliente: [**Microsoft.Azure.DigitalTwins.Parser**](https://nuget.org/packages/Microsoft.Azure.DigitalTwins.Parser/). También puede usar la biblioteca directamente para diseñar su propia solución de validación. Al usar la biblioteca del analizador, asegúrese de usar una versión que sea compatible con la versión de Azure Digital Twins que se está ejecutando. Durante la versión preliminar, se trata de la versión *3.7.0*.

Puede obtener más información sobre la biblioteca del analizador, incluidos ejemplos de uso, en [ Análisis y validación de modelos](how-to-use-parser.md).

## <a name="next-steps"></a>Pasos siguientes

Consulte cómo administrar modelos con las API DigitalTwinsModels:
* [Procedimiento: Administración de modelos personalizados](how-to-manage-model.md)

O bien aprenda cómo los gemelos digitales se crean basados en modelos:
* [Conceptos: Gemelos digitales y grafo de gemelos](concepts-twins-graph.md)


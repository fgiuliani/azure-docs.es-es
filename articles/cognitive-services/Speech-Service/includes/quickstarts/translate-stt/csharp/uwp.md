---
title: 'Inicio rápido: Traducción de voz a texto en C# (UWP): servicio de voz'
titleSuffix: Azure Cognitive Services
description: TBD
services: cognitive-services
author: lisaweixu
manager: nitinme
ms.service: cognitive-services
ms.subservice: speech-service
ms.date: 04/04/2020
ms.author: erhopf
ms.topic: include
ms.openlocfilehash: 62993b2e553630edd228228b4faa82de44997063
ms.sourcegitcommit: 67addb783644bafce5713e3ed10b7599a1d5c151
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/05/2020
ms.locfileid: "80671695"
---
## <a name="prerequisites"></a>Prerrequisitos

Antes de comenzar, compruebe lo siguiente:

> [!div class="checklist"]
> * [Ha creado un recurso de Voz de Azure](../../../../get-started.md)
> * [Configuración del entorno de desarrollo y creación de un proyecto vacío](../../../../quickstarts/setup-platform.md?tabs=uwp&pivots=programming-language-csharp)

## <a name="add-sample-code"></a>Incorporación de código de ejemplo

Ahora, agregue el código XAML que define la interfaz de usuario de la aplicación y agregue la implementación de código C# subyacente.

1. En el **Explorador de soluciones**, abra `MainPage.xaml`.

1. En la vista XAML del diseñador, inserte el fragmento de código XAML siguiente en la etiqueta **Cuadrícula** (entre `<Grid>` y `</Grid>`):

   [!code-xml[UI elements](~/samples-cognitive-services-speech-sdk/quickstart/csharp/uwp/translate-speech-to-text/helloworld/MainPage.xaml#StackPanel)]

1. En **Explorador de soluciones**, abra el archivo de código fuente subyacente `MainPage.xaml.cs`. (Se agrupa en `MainPage.xaml`).

1. Reemplace todo el código que contiene por el fragmento siguiente:

   [!code-csharp[Quickstart Code](~/samples-cognitive-services-speech-sdk/quickstart/csharp/uwp/translate-speech-to-text/helloworld/MainPage.xaml.cs#code)]

1. En el controlador `SpeechTranslationFromMicrophone_ButtonClicked` en este archivo, busque la cadena `YourSubscriptionKey` y reemplácela por su clave de suscripción.

1. En el controlador `SpeechTranslationFromMicrophone_ButtonClicked`, busque la cadena `YourServiceRegion` y reemplácela por la [región](~/articles/cognitive-services/Speech-Service/regions.md) asociada a su suscripción. (Por ejemplo, use `westus` para la suscripción de prueba gratuita).

1. En la barra de menús, elija **Archivo** > **Guardar todo** para guardar los cambios.

## <a name="build-and-run-the-application"></a>Compilación y ejecución de la aplicación

Ahora está listo para compilar y probar la aplicación.

1. En la barra de menús, seleccione **Compilar** > **Compilar solución** para compilar la aplicación. El código se debería compilar sin errores ahora.

1. Elija **Depurar** > **Iniciar depuración** o presione **F5** para iniciar la aplicación. Aparece la ventana **HelloWorld**.

   ![Ejemplo de aplicación de traducción de UWP en C#: inicio rápido](~/articles/cognitive-services/Speech-Service/media/sdk/qs-translate-speech-uwp-helloworld-window.png)

1. Seleccione **Habilitar micrófono** y, cuando aparezca la solicitud de permiso de acceso, seleccione **Sí**.

   ![Solicitud de permiso de acceso al micrófono](~/articles/cognitive-services/Speech-Service/media/sdk/qs-csharp-uwp-10-access-prompt.png)

1. Seleccione **Speech recognition with microphone input** (Reconocimiento de voz con entrada de micrófono) y diga una frase en inglés en el micrófono del dispositivo. La aplicación transmite su voz al servicio de voz, que la traduce y la transcribe a texto en otro idioma, en este caso, a alemán. El servicio de voz envía el texto traducido de nuevo a la aplicación, que muestra la traducción en la ventana.

   ![Interfaz de usuario de la traducción de voz](~/articles/cognitive-services/Speech-Service/media/sdk/qs-translate-csharp-uwp-ui-result.png)

## <a name="next-steps"></a>Pasos siguientes

[!INCLUDE [footer](./footer.md)]

---
title: archivo de inclusión
description: archivo de inclusión
services: virtual-machines
author: roygara
ms.service: virtual-machines
ms.topic: include
ms.date: 03/05/2020
ms.author: rogarana
ms.custom: include file
ms.openlocfilehash: 83c391c0d92f8d4a0ed4b44bc3a90273db51b412
ms.sourcegitcommit: 31ef5e4d21aa889756fa72b857ca173db727f2c3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2020
ms.locfileid: "81539562"
---
Las instantáneas incrementales son copias de seguridad en un momento dado de los discos administrados que, cuando se realizan, solo constan de todos los cambios desde la última instantánea. Al intentar descargar o usar una instantánea incremental, se utiliza el VHD completo. Esta nueva funcionalidad para las instantáneas de discos administrados puede permitir que sean más rentables, ya que no es necesario almacenar todo el disco con cada instantánea individual a menos que decida hacerlo expresamente. Al igual que con las instantáneas normales, se pueden usar instantáneas incrementales para crear un disco administrado completo o para realizar una instantánea normal.

Hay algunas diferencias entre una instantánea incremental y una instantánea normal. Las instantáneas incrementales usan siempre el almacenamiento de discos HDD estándar, independientemente del tipo de almacenamiento del disco, mientras que las instantáneas periódicas pueden usar discos SSD Premium. Si usa instantáneas periódicas en Premium Storage para escalar verticalmente implementaciones de máquinas virtuales, le recomendamos que use imágenes personalizadas en el almacenamiento estándar de [Shared Image Gallery](../articles/virtual-machines/linux/shared-image-galleries.md). Le ayudará a lograr una escala más masiva con un costo más bajo. Además, las instantáneas incrementales pueden ofrecer mejor confiabilidad con el [almacenamiento con redundancia de zona](../articles/storage/common/storage-redundancy-zrs.md). Si el almacenamiento con redundancia de zona está disponible en la región seleccionada, una instantánea incremental lo usará automáticamente. Si el almacenamiento con redundancia de zona no está disponible en la región, la instantánea tendrá como valor predeterminado el [almacenamiento con redundancia local](../articles/storage/common/storage-redundancy-lrs.md). Puede invalidar este comportamiento y seleccionar uno manualmente, pero no es recomendable.

Las instantáneas incrementales también ofrecen una funcionalidad diferencial, que está disponible de forma única para los discos administrados. Permiten obtener los cambios entre dos instantáneas incrementales de los mismos discos administrados hasta el nivel de bloque. Puede usar esta funcionalidad para reducir la superficie de los datos al copiar instantáneas entre regiones.  Por ejemplo, puede descargar la primera instantánea incremental como un blob base en otra región. Con las sucesivas instantáneas incrementales, solo puede copiar los cambios desde la última instantánea en el blob base. Después de copiar los cambios, puede tomar instantáneas en el blob base que representen la copia de seguridad a un momento dado del disco en otra región. Puede restaurar el disco desde el blob base o desde una instantánea que este contenga en otra región.

:::image type="content" source="media/virtual-machines-disks-incremental-snapshots-description/incremental-snapshot-diagram.png" alt-text="Diagrama que representa las instantáneas incrementales copiadas entre regiones. Las instantáneas realizan varias llamadas API hasta que finalmente forman blobs en página por cada instantánea.":::

El tamaño usado de las instantáneas se puede ver en el [informe de uso de Azure](https://docs.microsoft.com/azure/billing/billing-understand-your-bill). Por ejemplo, si el tamaño de datos usado de una instantánea es de 10 GiB, el informe de uso **diario** mostrará 10 GiB/(31 días) = 0,3226 como cantidad consumida.

---
title: "aaaDisplaying conteúdo do Javadoc no Eclipse para Olá pacote de bibliotecas do Azure para Java"
description: "Como toodisplay hello conteúdo do Javadoc para bibliotecas do Azure Olá no Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 30f8b6a1-1d76-4d1c-861b-1db478c46e6b
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 8070023a24dc07eca8df906db5b8b662ceed6ccc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="displaying-javadoc-content-in-eclipse-for-hello-azure-libraries-package-for-java"></a>Exibindo o conteúdo do Javadoc no Eclipse para Olá pacote de bibliotecas do Azure para Java
Olá conteúdo do Javadoc para Olá bibliotecas do Azure para Java pode ser exibido em seu ambiente do Eclipse associando toohello conteúdo do Javadoc de saudação bibliotecas do Azure para Java. Olá etapas a seguir mostram como toouse essa funcionalidade no Eclipse.

Este procedimento pressupõe que você já adicionou hello Azure da biblioteca para o caminho de compilação Java tooyour.

## <a name="toodisplay-javadoc-content-in-eclipse-for-hello-azure-libraries-for-java"></a>toodisplay conteúdo do Javadoc no Eclipse para Olá bibliotecas do Azure para Java
* No Explorador de projeto do Eclipse, no hello **bibliotecas referenciadas** seção do projeto, no menu de contexto de saudação aberto para Olá biblioteca do Azure para Java JAR. Por exemplo, **windowsazure microsoft-0.1.0.jar api** (número de versão de hello pode ser diferente, depende de qual versão você instalou).

* Clique em **Propriedades**.

* Dentro de saudação **propriedades** caixa de diálogo, no painel esquerdo do hello, clique em **local do Javadoc**. Olá **local do Javadoc** caixa de diálogo é exibida.

* Você pode especificar uma **URL Javadoc**, ou um **Javadoc no arquivo**.

   * Se você escolher toospecify um **URL do Javadoc**, use Olá URLs como **http://dl.windowsazure.com/javadoc** ou **http://dl.windowsazure.com/storage/javadoc**.

   * Se você escolher toouse **Javadoc no arquivo**, você pode especificar um arquivo externo ou um arquivo de espaço de trabalho.

   Faça sua escolha e procure/valide conforme necessário. Olá exemplo a seguir associa Olá bibliotecas do Azure para Java Olá Javadoc JAR correspondente que foi baixado localmente tooa pasta denominada **c:\MyAzureJARs**.

   ![][ic553487]

* *Etapa Opcional*: clique em **Validar**. Problemas potenciais com hello Javadoc JAR podem ser exibidos aqui.

* Clique em **OK**.

Uma vez associado biblioteca hello, Olá conteúdo do Javadoc deve exibir seu IDE do Eclipse. Por exemplo, se `blob` é definido como o tipo `CloudBlockBlob` dentro de seu código, a seguinte Olá é um exemplo de conteúdo do Javadoc que aparece quando você digita `blob.acquireLease` no código:

![][ic553488]

## <a name="see-also"></a>Consulte também
[Kit de Ferramentas do Azure para Eclipse][Azure Toolkit for Eclipse]

[Criar um aplicativo Hello World para Azure no Eclipse][Creating a Hello World Application for Azure in Eclipse]

[Saudação de instalar o Kit de ferramentas do Azure para Eclipse][Installing hello Azure Toolkit for Eclipse] 

Para obter mais informações sobre como usar o Azure com Java, consulte Olá [Centro de desenvolvedores de Java do Azure][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic553487]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553487.png
[ic553488]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553488.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh698319.aspx -->

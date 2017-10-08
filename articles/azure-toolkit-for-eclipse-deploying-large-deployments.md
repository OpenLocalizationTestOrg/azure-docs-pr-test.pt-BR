---
title: "aaaDeploying grandes implantações"
description: "Saiba como toodeploy grandes implantações usando Olá Kit de ferramentas do Azure para Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 5e18bace-5df0-4af8-ad86-6151ea8bd823
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 6b1d2a7a5e49c78154fc856a221e64ca8dcfbe9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-large-deployments"></a>Implantando Grandes Implantações
Se sua implantação for muito grande toobe contida na pasta de approot saudação padrão, você pode usar um recurso de armazenamento local como a pasta raiz de implantação das Olá para o seu JDK e servidor de aplicativos.

## <a name="toouse-a-local-storage-resource-as-hello-deployment-root-folder-for-large-deployments"></a>um recurso de armazenamento local como pasta Olá de raiz de implantação para grandes implantações de toouse
1. Crie um recurso de armazenamento local novo. nome de saudação do recurso de saudação não importa. Recursos de armazenamento são definidos no nível de função hello. Hello mais rápida maneira tooaccess Olá armazenamento local configuração caixa de diálogo, na qual você pode criar um novo recurso de armazenamento local, é usando Olá etapas a seguir: função de saudação com o botão direito no hello **Explorador de projeto** exibição (expandir seu Nó do projeto Azure se você não vir a função hello), clique em **Azure**e, em seguida, clique em **armazenamento Local**. Dentro de saudação **armazenamento Local** caixa de diálogo, clique em **adicionar** toocreate um novo recurso de armazenamento local.

2. Olá conjunto desejado tooat de tamanho mínimo 2048 MB (nada menor pode causar Olá mesmos problemas de tamanho de arquivo como haveria na approot Olá).

3. Certifique-se de que **Limpar conteúdo hello quando Olá instância de função é reciclada** é verificada; isso ajuda a impedir que Olá lógica de inicialização seja executada em conflitos com os arquivos pré-existentes no recurso Olá Olá quando a função instância é reciclada.

4. Certifique-se de que Olá **armazenar variável do ambiente Olá o caminho do diretório do recurso após a implantação** valor é definido de cadeia de caracteres toohello **DEPLOYROOT**. A caixa de diálogo do recurso de armazenamento local será a aparência a seguir toohello semelhante.

   ![][ic667943]

Como alternativa, se você usar **DEPLOYROOT** como Olá *nome* de seus recursos locais e você não alterar o nome de variável de ambiente gerada automaticamente hello (que será definido muito **DEPLOYROOT_PATH** nesse caso), isso funcionaria para seu aplicativo.

Informações adicionais sobre como criar um recurso de armazenamento local podem ser encontradas em [Propriedades de armazenamento local][Local storage properties].

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
[Local storage properties]: http://go.microsoft.com/fwlink/?LinkID=699525#local_storage_properties

<!-- IMG List -->

[ic667943]: ./media/azure-toolkit-for-eclipse-deploying-large-deployments/ic667943.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268601.aspx -->

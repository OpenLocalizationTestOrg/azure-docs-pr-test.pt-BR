---
title: Ferramentas para trabalhar com o Armazenamento do Azure | Microsoft Docs
description: Uma lista de ferramentas que permite exibir/interagir com os dados do Armazenamento do Azure.
services: storage
documentationcenter: 
author: dineshmurthy
manager: jahogg
editor: tysonn
ms.assetid: e4748642-98c4-437e-b0ed-4f9641c2e894
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: dineshmurthy
ms.openlocfilehash: 620efda06d8225b21b6bb9b104b79061ebb6515c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-storage-client-tools"></a>Ferramentas de Cliente do Armazenamento do Azure
Com frequência, os usuários do Armazenamento do Azure desejam poder exibir/interagir com seus dados usando uma ferramenta de cliente do Armazenamento do Azure. Nas tabelas abaixo, listamos várias ferramentas que permitem que você faça isso. Colocamos um "X" em cada bloco caso a ferramenta forneça a capacidade de enumerar e/ou acessar a abstração de dados. A tabela também mostra se as ferramentas são gratuitas ou não. "Avaliação" indica que há uma avaliação gratuita, mas o produto completo não é gratuito. "S/N" indica que uma versão está disponível gratuitamente, enquanto outra versão está disponível para compra.

Fornecemos somente um instantâneo das ferramentas de cliente do Armazenamento do Azure disponíveis. Essas ferramentas poderão continuar a evoluir e expandir sua funcionalidade. Se houver correções ou atualizações, deixe um comentário para nos contar. O mesmo é verdadeiro se você conhecer ferramentas que deveriam estar aqui – ficaríamos felizes de adicioná-las.

**Ferramentas de Cliente do Armazenamento do Microsoft Azure**

<table>
  <tr>
    <th rowspan="2">Ferramenta de Cliente do Armazenamento do Azure</th>
    <th rowspan="2">Blob de blocos</th>
    <th rowspan="2">Blob de páginas</th>
    <th rowspan="2">Acrescentar blob</th>
    <th rowspan="2">Tabelas</th>
    <th rowspan="2">Filas</th>
    <th rowspan="2">Arquivos</th>
    <th rowspan="2">Grátis</th>
    <th colspan="4">Plataforma</th>
  </tr>
  <tr>
    <td>Web</td>
    <td>Windows</td>
    <td>OSX</td>
    <td>Linux</td>
  </tr>
  <tr>
    <td><a href="https://azure.microsoft.com/features/azure-portal/">Portal do Microsoft Azure</a></td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>S</td>
    <td>X</td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><a href="http://storageexplorer.com/">Gerenciador do Armazenamento do Microsoft Azure</a></td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>S</td>
    <td></td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
  </tr>
  <tr>
    <td><a href="https://www.visualstudio.com/features/azure-tools-vs.aspx">Gerenciador de Servidores do Microsoft Visual Studio</a></td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>S</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</table>

**Ferramentas de Cliente de terceiros do Armazenamento do Azure**

Nós não verificamos a funcionalidade nem a qualidade declarada pelas ferramentas de terceiros indicadas a seguir e sua listagem não implica o endosso da Microsoft.

<table>
  <tr>
    <th rowspan="2">Ferramenta de Cliente do Armazenamento do Azure</th>
    <th rowspan="2">Blob de blocos</th>
    <th rowspan="2">Blob de páginas</th>
    <th rowspan="2">Acrescentar blob</th>
    <th rowspan="2">Tabelas</th>
    <th rowspan="2">Filas</th>
    <th rowspan="2">Arquivos</th>
    <th rowspan="2">Grátis</th>
    <th colspan="4">Plataforma</th>
  </tr>
  <tr>
    <td>Web</td>
    <td>Windows</td>
    <td>OSX</td>
    <td>Linux</td>
  </tr>
  <tr>
    <td><a href="http://www.cloudportam.com/">Cloud Portam</a></td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>Avaliação</td>
    <td>X</td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><a href="http://www.cerebrata.com/products/azure-management-studio/introduction">Cerabrata: Azure Management Studio</a></td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>Avaliação</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><a href="http://www.cerebrata.com/products/azure-explorer/introduction">Cerabrata: Explorador do Azure</a></td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td></td>
    <td>X</td>
    <td>S</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><a href="https://github.com/sebagomez/azurestorageexplorer">Gerenciador de Armazenamento do Azure</a></td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>S</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><a href="http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx">CloudBerry Explorer</a></td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td></td>
    <td></td>
    <td>X</td>
    <td>S/N</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><a href="http://www.gapotchenko.com/cloudcombine">Cloud Combine</a></td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>Avaliação</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><a href="http://clumsyleaf.com">ClumsyLeaf: AzureXplorer, CloudXplorer, TableXplorer</a></td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>S</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><a href="http://www.gladinet.com/Azure-Storage/index.htm">Gladinet Cloud</a></td>
    <td>X</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td>Avaliação</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><a href="http://storageexplorer.codeplex.com/">Navegador do Armazenamento da Web do Azure</a></td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>S</td>
    <td>X</td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><a href="https://zudio.co/">Zudio</a></td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>Avaliação</td>
    <td>X</td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
</table>

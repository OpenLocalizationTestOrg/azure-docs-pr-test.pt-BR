---
title: Criar um arquivo .doc para conectar a um servidor do Azure Analysis Services | Microsoft Docs
description: "Saiba como criar um arquivo de conexão de dados do Office e se conectar e obter dados de um servidor do Analysis Services no Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/23/2017
ms.author: owend
ms.openlocfilehash: 530f3b5c9e90cb45ffb6e12d0d08a35f8d687471
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-office-data-connection-file"></a><span data-ttu-id="0f461-103">Criar um arquivo de conexão de dados do Office</span><span class="sxs-lookup"><span data-stu-id="0f461-103">Create an Office Data Connection file</span></span>

<span data-ttu-id="0f461-104">As informações neste artigo descrevem como você pode, do Excel 2013 ou do Excel 2016 número de versão 16.0.7369.2117 ou anterior, criar um arquivo de conexão de dados do Office para se conectar a um servidor do Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="0f461-104">Information in this article describes how you can create an Office Data Connection file to connect to an Azure Analysis Services server from Excel 2016 version number 16.0.7369.2117 or earlier, or Excel 2013.</span></span> <span data-ttu-id="0f461-105">Um [provedor MSOLAP.7](analysis-services-data-providers.md) atualizado também é necessário.</span><span class="sxs-lookup"><span data-stu-id="0f461-105">An updated [MSOLAP.7 provider](analysis-services-data-providers.md) is also required.</span></span>


1. <span data-ttu-id="0f461-106">Copie o exemplo de arquivo de conexão abaixo e cole-o em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="0f461-106">Copy the sample connection file below and paste into a text editor.</span></span> 

2. <span data-ttu-id="0f461-107">Em `odc:ConnectionString`, altere as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="0f461-107">In `odc:ConnectionString`, change the following properties:</span></span>

    *   <span data-ttu-id="0f461-108">Em `Data Source=asazure://<region>.asazure.windows.net/<servername>;`, altere `<region>` para a região de seu servidor do Analysis Services e `<servername>` para o nome do servidor.</span><span class="sxs-lookup"><span data-stu-id="0f461-108">In `Data Source=asazure://<region>.asazure.windows.net/<servername>;` change `<region>` to the region of your Analysis Services server and `<servername>` to the name of your  server.</span></span>

    *   <span data-ttu-id="0f461-109">Em `Initial Catalog=<database>;`, altere `<database>` para o nome de seu banco de dados.</span><span class="sxs-lookup"><span data-stu-id="0f461-109">In `Initial Catalog=<database>;` change `<database>` to the name of your database.</span></span>

3. <span data-ttu-id="0f461-110">Em `<odc:CommandText>Model</odc:CommandText>`, altere `Model` para o nome de seu modelo ou perspectiva.</span><span class="sxs-lookup"><span data-stu-id="0f461-110">In `<odc:CommandText>Model</odc:CommandText>` change `Model` to the name of your model or perspective.</span></span> 

4. <span data-ttu-id="0f461-111">Salve o arquivo com uma extensão `.odc` na pasta C:\Usuários\\*nome do usuário*\Documentos\Minhas Fontes de Dados.</span><span class="sxs-lookup"><span data-stu-id="0f461-111">Save the file with an `.odc` extension to the C:\Users\\*username*\Documents\My Data Sources folder.</span></span>

5. <span data-ttu-id="0f461-112">Clique com o botão direito do mouse no arquivo e, em seguida, clique em **Abrir no Excel**.</span><span class="sxs-lookup"><span data-stu-id="0f461-112">Right-click the file, and then click **Open in Excel**.</span></span> <span data-ttu-id="0f461-113">Ou no Excel, na faixa de opções **Dados**, clique em **Conexões Existentes**, selecione o arquivo e, em seguida, clique em **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="0f461-113">Or in Excel, on the **Data** ribbon, click **Existing Connections**, select your file, and then click **Open**.</span></span>



<span data-ttu-id="0f461-114">**Exemplo de arquivo de conexão**</span><span class="sxs-lookup"><span data-stu-id="0f461-114">**Sample connection file**</span></span>
```
<html xmlns:o="urn:schemas-microsoft-com:office:office"
xmlns="http://www.w3.org/TR/REC-html40">

<head>
<meta http-equiv=Content-Type content="text/x-ms-odc; charset=utf-8">
<meta name=ProgId content=ODC.Cube>
<meta name=SourceType content=OLEDB>
<meta name=Catalog content="Database">
<meta name=Table content=Model>
<title>AzureAnalysisServicesConnection</title>
<xml id=docprops><o:DocumentProperties
  xmlns:o="urn:schemas-microsoft-com:office:office"
  xmlns="http://www.w3.org/TR/REC-html40">
  <o:Name>SampleAzureAnalysisServices</o:Name>
 </o:DocumentProperties>
</xml><xml id=msodc><odc:OfficeDataConnection
  xmlns:odc="urn:schemas-microsoft-com:office:odc"
  xmlns="http://www.w3.org/TR/REC-html40">
  <odc:Connection odc:Type="OLEDB">
   <odc:ConnectionString>Provider=MSOLAP.7;Data Source=asazure://<region>.asazure.windows.net/<servername>;Initial Catalog=<database>;</odc:ConnectionString>
   <odc:CommandType>Cube</odc:CommandType>
   <odc:CommandText>Model</odc:CommandText>
  </odc:Connection>
 </odc:OfficeDataConnection>
</xml>
<style>
<!--
    .ODCDataSource
    {
    behavior: url(dataconn.htc);
    }
-->
</style>
 
</head>

<body onload='init()' scroll=no leftmargin=0 topmargin=0 rightmargin=0 style='border: 0px'>
<table style='border: solid 1px threedface; height: 100%; width: 100%' cellpadding=0 cellspacing=0 width='100%'> 
  <tr> 
    <td id=tdName style='font-family:arial; font-size:medium; padding: 3px; background-color: threedface'> 
      &nbsp; 
    </td> 
     <td id=tdTableDropdown style='padding: 3px; background-color: threedface; vertical-align: top; padding-bottom: 3px'>

      &nbsp; 
    </td> 
  </tr> 
  <tr> 
    <td id=tdDesc colspan='2' style='border-bottom: 1px threedshadow solid; font-family: Arial; font-size: 1pt; padding: 2px; background-color: threedface'>

      &nbsp; 
    </td> 
  </tr> 
  <tr> 
    <td colspan='2' style='height: 100%; padding-bottom: 4px; border-top: 1px threedhighlight solid;'> 
      <div id='pt' style='height: 100%' class='ODCDataSource'></div> 
    </td> 
  </tr> 
</table> 

  
<script language='javascript'> 

function init() { 
  var sName, sDescription; 
  var i, j; 
  
  try { 
    sName = unescape(location.href) 
  
    i = sName.lastIndexOf(".") 
    if (i>=0) { sName = sName.substring(1, i); } 
  
    i = sName.lastIndexOf("/") 
    if (i>=0) { sName = sName.substring(i+1, sName.length); } 

    document.title = sName; 
    document.getElementById("tdName").innerText = sName; 

    sDescription = document.getElementById("docprops").innerHTML; 
  
    i = sDescription.indexOf("escription>") 
    if (i>=0) { j = sDescription.indexOf("escription>", i + 11); } 

    if (i>=0 && j >= 0) { 
      j = sDescription.lastIndexOf("</", j); 

      if (j>=0) { 
          sDescription = sDescription.substring(i+11, j); 
        if (sDescription != "") { 
            document.getElementById("tdDesc").style.fontSize="x-small"; 
          document.getElementById("tdDesc").innerHTML = sDescription; 
          } 
        } 
      } 
    } 
  catch(e) { 

    } 
  } 
</script> 

</body> 
 
</html>

```




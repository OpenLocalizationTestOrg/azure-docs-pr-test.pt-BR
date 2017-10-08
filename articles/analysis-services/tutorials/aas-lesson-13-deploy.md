---
título: aaa "lição do tutorial do Azure Analysis Services 13: implantar | Descrição de Microsoft Docs": descreve como o tutorial de saudação toodeploy projeto tooAzure Analysis Services.
serviços: documentationcenter do analysis services: ' autor: manager minewiskan: erikre editor: ' marcas: '

MS. AssetID: MS. Service: MS. devlang do analysis services: NA MS. Topic: get-started-article tgt_pltfrm: NA Workload: MS. Date na: 17/07/2017 Author: owend
---
# <a name="lesson-13-deploy"></a>Lição 13: implantar

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Nesta lição, você configurar propriedades de implantação. especificando um tooand de toodeploy de servidor um nome para o modelo de saudação do Azure Analysis Services. Em seguida, implantar toothat instância de modelo a saudação. Depois que o modelo é implantado, os usuários podem se conectar tooit usando um aplicativo cliente de relatório. mais, consulte toolearn [implantar serviços de análise de tooAzure](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy).  
  
Estimado tempo toocomplete nesta lição: **5 minutos**  
  
## <a name="prerequisites"></a>Pré-requisitos  
Este tópico faz parte de um tutorial de modelagem tabular, que deve ser concluído na devida ordem. Antes de executar tarefas de saudação nesta lição, você deverá ter completado lição anterior Olá: [lição 12: analisar no Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).  

> [!IMPORTANT]  
> Você deve ter [permissões de administrador](../analysis-services-server-admins.md) em Olá remoto do Analysis Services server em ordem toodeploy tooit.  

> [!IMPORTANT]  
> Se você instalou o banco de dados de exemplo hello AdventureWorksDW2014 em um SQL Server local e você estiver implantando o servidor do modelo tooan Azure Analysis Services, uma [gateway de dados no local](../analysis-services-gateway.md) é necessária.
  
## <a name="deploy-hello-model"></a>Implantar o modelo de saudação  
  
#### <a name="tooconfigure-deployment-properties"></a>Propriedades de implantação tooconfigure  

  
1.  Em **Gerenciador de soluções**, Olá atalho **de vendas pela Internet AW** do projeto e, em seguida, clique em **propriedades**.  
  
2.  Em Olá **páginas de propriedades de vendas de Internet AW** caixa de diálogo **servidor de implantação**, em Olá **Server** propriedade, digite servidor completo hello.  

    ![aas-lesson13-deploy-property](../tutorials/media/aas-lesson13-deploy-property.png)
  
3.  Em Olá **banco de dados** propriedade, digite **Adventure Works Internet Sales**.  
  
4.  Em Olá **nome do modelo** propriedade, digite **modelo de vendas do Adventure Works Internet**.  
  
5.  Verifique suas seleções e então clique em **OK**.  
  
#### <a name="toodeploy-hello-adventure-works-internet-sales"></a>Olá toodeploy Adventure Works Internet Sales
  
1.  Em **Solution Explorer**, Olá do botão direito do mouse **de vendas pela Internet AW** projeto > **criar**.  

2.  Saudação de atalho **de vendas pela Internet AW** projeto > **implantar**.

    Ao implantar tooAzure Analysis Services, você pode ser solicitado tooenter sua conta. Insira sua conta e senha organizacionais, por exemplo, nancy@adventureworks.com. Essa conta deve estar em Administradores no servidor de saudação.
  
    caixa de diálogo implantar Olá aparece e exibe o status de implantação de saudação de saudação metadados e cada tabela incluído no modelo de saudação.  
    
    ![aas-lesson13-deploy-status](../tutorials/media/aas-lesson13-deploy-status.png)
  
3. Quando a implantação for concluída com êxito, vá em frente e clique em **Fechar**.  
  
## <a name="conclusion"></a>Conclusão  
Parabéns! Você terminou de criar e implantar seu primeiro modelo tabular do Analysis Services. Este tutorial ajudou você a concluir as tarefas mais comuns de saudação na criação de um modelo de tabela. Agora que o modelo do Adventure Works Internet Sales é implantado, você pode usar o modelo de saudação do SQL Server Management Studio toomanage; crie scripts de processo e um plano de backup. Os usuários agora também podem se conectar toohello modelo usando um aplicativo cliente de relatório, como o Microsoft Excel ou Power BI.  

![aas-lesson13-ssms](../tutorials/media/aas-lesson13-ssms.png)
  
  
  
## <a name="whats-next"></a>O que vem a seguir?
[Conecte-se com o Power BI Desktop](../analysis-services-connect-pbi.md)   
[Lição suplementar - Segurança dinâmica](../tutorials/aas-supplemental-lesson-dynamic-security.md)   
[Lição suplementar - Linhas de detalhes](../tutorials/aas-supplemental-lesson-detail-rows.md)   
[Lição Suplementar – hierarquias desbalanceadas](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)   

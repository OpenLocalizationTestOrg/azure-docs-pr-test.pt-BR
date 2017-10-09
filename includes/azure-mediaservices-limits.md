>[!NOTE]
>Você pode pedir para recursos que não são fixas, Olá cotas toobe gerado, abrindo um tíquete de suporte. Fazer **não** criar contas de serviços de mídia do Azure adicionais em uma tentativa de limites maiores tooobtain.

| Recurso | Limite padrão | 
| --- | --- | 
| AMS (Contas de Serviços de Mídia) do Azure em uma única assinatura | 25 (fixo) |
| RUs (Unidades Reservadas) de Mídia por conta AMS |25 (S1, S2)<br/>10 (S3) <sup>(1)</sup> | 
| Trabalhos por conta AMS | 50,000<sup>(2)</sup> |
| Tarefas encadeadas por trabalho | 30 (fixo) |
| Ativos por conta AMS | 1.000.000|
| Ativos por tarefa | 50 |
| Ativos por trabalho | 100 |
| Localizadores exclusivos associados a um ativo simultaneamente | 5<sup>(4)</sup> |
| Canais ao vivo por conta AMS  |5|
| Programas no estado interrompido por canal  |50|
| Programa em estado de execução por canal  |3|
| Pontos de extremidade de streaming no estado “executando” por conta AMS|2|
| Unidades de streaming por ponto de extremidade de streaming |10 |
| Contas de armazenamento | 1,000<sup>(5)</sup> (fixo) |
| Políticas | 1,000,000<sup>(6)</sup> |
| Tamanho do arquivo| Em alguns cenários, há um limite no tamanho de arquivo máximo Olá tem suportado para processamento nos serviços de mídia. <sup>7</sup> |
  
<sup>1</sup> S3 RUs não estão disponíveis na Índia Ocidental. Olá max RU limites redefinidos se o cliente Olá altera o tipo de saudação (por exemplo, de tooS1 S2). 

<sup>2</sup> Esse número inclui trabalhos em fila, concluídos, ativos e cancelados. Ele não inclui trabalhos excluídos. Você pode excluir trabalhos antigos do hello usando **IJob.Delete** ou hello **excluir** solicitação HTTP.

Começando em 1 de abril de 2017, qualquer registro de trabalho em sua conta mais de 90 dias será excluído automaticamente, junto com seus registros de tarefas associados, mesmo se Olá o número total de registros é abaixo de cota máximo hello. Se precisar de informações de trabalho/tarefa Olá tooarchive, você pode usar código Olá descrito [aqui](../articles/media-services/media-services-dotnet-manage-entities.md).

<sup>3</sup> ao fazer uma solicitação de entidades de trabalho toolist, um máximo de 1.000 será retornado por solicitação. Se você precisar acompanhar tookeep de todos os trabalhos enviados, você pode usar top/skip conforme descrito em [opções de consulta OData sistema](http://msdn.microsoft.com/library/gg309461.aspx).

<sup>4</sup> Os localizadores não foram desenvolvidos para gerenciar o controle de acesso por usuário. usuários de tooindividual de direitos de acesso diferentes toogive, usar soluções de gerenciamento de direitos digitais (DRM). Para saber mais, consulte [esta](../articles/media-services/media-services-content-protection-overview.md) seção.

<sup>5</sup> contas de armazenamento Olá devem ser de saudação mesma assinatura do Azure.

<sup>6</sup> há um limite de 1.000.000 políticas para diferentes políticas de AMS (por exemplo, para política de Localizador ou ContentKeyAuthorizationPolicy). 

>[!NOTE]
> Você deve usar Olá Olá a mesma ID de política se você estiver usando sempre mesmo dias / permissões de acesso / etc. Para obter informações e um exemplo, veja [esta](../articles/media-services/media-services-dotnet-manage-entities.md#limit-access-policies) seção.

<sup>7</sup>se você estiver carregando tooan conteúdo ativo no Azure Media serviços com tooprocess intenção Olá-o com um dos processadores de mídia Olá em nosso serviço (ou seja, codificadores como mecanismos de codificador de mídia padrão e de fluxo de trabalho Premium de codificador de mídia ou de análise como o Detector de Face), em seguida, você deve estar ciente da restrição de saudação no tamanho máximo de saudação. 

A partir de 15 de maio de 2017, o tamanho máximo de saudação suportado para um único blob é TB 195 - com arquivo largers que esse limite, a tarefa falhará. Estamos trabalhando tooaddress uma correção esse limite. Além disso, Olá restrição no tamanho máximo de saudação do hello ativo é da seguinte maneira.

| Tipo de Unidade Reservada de Mídia | Tamanho máximo de entrada (GB)| 
| --- | --- | 
|S1 | 325|
|S2 | 640|
|S3 | 260|

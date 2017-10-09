<!--author=SharS last changed: 9/17/15-->

### <a name="upgrade-sharepoint-2010-toosharepoint-2013-and-then-install-hello-storsomple-adapter-for-sharepoint"></a>Atualizar o SharePoint 2010 tooSharePoint 2013 e, em seguida, instalar Olá StorSomple adaptador para SharePoint
> [!IMPORTANT]
> Todos os arquivos que foram movidos anteriormente tooexternal armazenamento via RBS não estarão disponível até que a atualização de saudação for concluída e Olá recurso RBS é habilitado novamente. usuário toolimit afetar, execute qualquer atualização ou reinstalação durante uma janela de manutenção planejada.
> 
> 

#### <a name="tooupgrade-sharepoint-2010-toosharepoint-2013-and-then-install-hello-adapter"></a>tooSharePoint tooupgrade 2010 do SharePoint 2013 e, em seguida, instalar o adaptador de saudação
1. No farm de saudação do SharePoint 2010, a anotação de caminho para Olá do repositório de BLOB de saudação externalizados BLOBs e bancos de dados de conteúdo do Olá para o qual o RBS está habilitado. 
2. Instalar e configurar Olá novo farm do SharePoint 2013. 
3. Mova bancos de dados, aplicativos e conjuntos de sites do farm toohello do SharePoint 2013 novo farm saudação do SharePoint 2010. Para obter instruções, vá muito[visão geral do processo de atualização de saudação tooSharePoint 2013](https://technet.microsoft.com/library/cc262483.aspx).
4. Instale Olá adaptador StorSimple para SharePoint no farm de saudação. Vá muito[Olá instalar adaptador StorSimple para SharePoint](#install-the-storsimple-adapter-for-sharepoint) para procedimentos.
5. Usando informações de saudação que você anotou na etapa 1, habilite o RBS para Olá mesmo conjunto de bancos de dados de conteúdo e fornecer Olá mesmo BLOB armazenar caminho que foi usado na instalação de saudação do SharePoint 2010. Vá muito[configurar RBS](#configure-rbs) para procedimentos. Depois de concluir esta etapa, os arquivos previamente externalizados devem ser acessíveis de novo farm de saudação. 

### <a name="upgrade-hello-storsimple-adapter-for-sharepoint"></a>Saudação de atualização do adaptador StorSimple para SharePoint
> [!IMPORTANT]
> Você agendou essa atualização toooccur durante uma janela de manutenção planejada para Olá motivos a seguir:
> 
> * Previamente externalizado conteúdo não estará disponível até que o adaptador de saudação seja reinstalado.
> * Qualquer conteúdo atualizado toohello site depois de desinstalar a versão anterior de saudação do hello adaptador StorSimple para SharePoint, mas antes de instalar a nova versão de hello, serão armazenados no banco de dados de conteúdo do hello. Você precisará toomove dispositivo StorSimple toohello conteúdo depois de instalar o novo adaptador de saudação. Você pode usar o hello Microsoft` RBS Migrate()` cmdlet do PowerShell incluído com o conteúdo do SharePoint toomigrate hello. Para saber mais, consulte [Migrar o conteúdo para dentro ou fora do RBS](https://technet.microsoft.com/library/ff628255.aspx). 
> 
> 

#### <a name="tooupgrade-hello-storsimple-adapter-for-sharepoint"></a>Olá tooupgrade adaptador StorSimple para SharePoint
1. Desinstale a versão anterior de saudação do adaptador StorSimple para SharePoint.
   
   > [!NOTE]
   > Isso desabilitará automaticamente o RBS nos bancos de dados de conteúdo do hello. No entanto, os BLOBs continuarão no dispositivo do StorSimple hello. Como o RBS está desabilitado e Olá BLOBs não foram migrados toohello back bancos de dados de conteúdo, qualquer solicitação desses BLOBs falhará. 
   > 
   > 
2. Instalar Olá novo adaptador StorSimple para SharePoint. novo adaptador de saudação reconhecerá automaticamente Olá bancos de dados que foram habilitados ou desabilitados para RBS anteriormente e usará as configurações anteriores hello.


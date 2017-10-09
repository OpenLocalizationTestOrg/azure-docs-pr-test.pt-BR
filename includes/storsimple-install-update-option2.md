<!--author=SharS last changed: 03/17/2016-->

#### <a name="tooinstall-update-12-from-hello-azure-classic-portal"></a>tooinstall 1.2 de atualização de saudação portal clássico do Azure
1. No portal clássico do Azure do hello, vá toohello **dispositivos** página e selecione seu dispositivo.
2. Navegue muito**dispositivos** > **configurar**.
3. Em **Interfaces de Rede**, verifique primeiro se você tem pelo menos uma interface de rede que esteja habilitada para iSCSI. Em seguida, localize a interface de rede de saudação (exceto a DATA 0) que tem um gateway atribuído.
4. Desabilitar a interface de rede de saudação que possui um gateway atribuído e salve a configuração modificada hello. Observe as configurações de interface de rede Olá são mantidas e então quando você reativa essa interface de rede posteriormente, portal Olá reverterá as configurações originais do toohello.
5. Agora você pode [usar Olá tooinstall portal clássico do Azure 1.2 atualização](#install-update-12-via-the-azure-classic-portal). Siga as instruções de hello a partir da etapa 3 deste procedimento. Depois de instalar todas as atualizações de hello, você pode habilitar novamente a interface de rede Olá desabilitado.


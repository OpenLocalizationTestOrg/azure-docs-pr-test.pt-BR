<!--author=alkohli last changed: 03/17/16-->

## <a name="troubleshooting-update-failures"></a>Solucionando problemas de falhas na atualização
**Se você receber uma notificação que Olá verificações pré-atualização falha?**

Se uma pré-verificação de falhar, certifique-se de que você já usou a barra de notificação detalhada Olá final Olá Olá página. Isso fornece a orientação como Falha na pré-verificação de toowhich. Olá ilustração a seguir mostra uma instância em que uma notificação aparece. Nesse caso, a verificação de integridade do componente de hardware e de verificação de integridade do controlador Olá tem falhado. Em Olá **Status do Hardware** seção, você pode ver que ambos **controlador 0** e **controlador 1** componentes precisam de atenção.

  ![Falha na pré-verificação](./media/storsimple-install-troubleshooting/HCS_PreUpdateCheckFailed-include.png)

Você precisará toomake se ambos os controladores estão íntegros e online. Você também precisará toomake-se de que todos os componentes de hardware Olá no dispositivo do StorSimple Olá são mostrados toobe Íntegro na página de manutenção de saudação. Em seguida, você pode tentar tooinstall atualizações. Se você não for capaz de toofix problemas de componente de hardware de saudação, você precisará toocontact Microsoft Support para as próximas etapas.

**Se você recebe uma mensagem de erro "Não foi possível instalar as atualizações" e Olá recomendação é toorefer toohello guia toodetermine Olá causa da falha de saudação de solução de problemas?**

Uma causa provável para isso pode ser que você não tenha servidores do Microsoft Update toohello conectividade. Essa é uma verificação manual que precisa toobe executada. Se você perder o servidor de atualização de toohello de conectividade, o trabalho de atualização falhará. Você pode verificar a conectividade de saudação executando Olá cmdlet a seguir na interface do Windows PowerShell de saudação do seu dispositivo StorSimple:

 `Test-Connection -Source <Fixed IP of your device controller> -Destination <Any IP or computer name outside of datacenter>`

Execute o cmdlet de saudação em ambos os controladores.

Se tiver verificado existe conectividade hello e continuar toosee esse problema, entre em contato com o Microsoft Support para as próximas etapas.

**E se houver uma falha de atualização ao atualizar seu dispositivo tooUpdate 4 e ambos os controladores de saudação com atualização 4?**

Iniciando atualização 4, se ambos os controladores Olá Olá executando a mesma versão do software e se houver uma falha de atualização, controladores de saudação não entrar no modo de recuperação. Essa situação pode ocorrer se hello hotfix do software de dispositivo (atualização de 1º de ordem) é aplicado tooboth Olá controladores com êxito, mas outros hotfixes (ordem 2º e 3º ordem) são ainda toobe aplicado. Iniciando atualização 4, controladores de saudação entrará no modo de recuperação somente se os dois controladores de saudação estiver executando versões diferentes do software. 

Se o usuário Olá vê uma falha na atualização, quando ambos os controladores estão executando a atualização 4, recomendamos que aguarde alguns minutos e, em seguida, tente atualizar novamente. Se a repetição de saudação não for bem-sucedida, em seguida, eles devem entrar em contato com Microsoft Support.

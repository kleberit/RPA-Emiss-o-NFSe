▪ Log Orquestrador Prefect
▪ Inicia Instancia do Navegador
▪ Setup de Navegador e Pastas:
# 1. Limpeza: Finaliza instâncias anteriores do Chrome/Chromedriver para evitar bloqueios.  # 2. Diretórios: Organiza e cria automaticamente a pasta de downloads para o mês atual.  # 3. Preferências: Configura o perfil do Chrome e força o download automático de PDFs.  # 4. Patches BotCity: Injeta as customizações do Selenium e auto-maximiza a janela ao navegar.
▪ Pega Data do Sistema
▪ Formata Data
▪ Chamada Api de NFS
▪ Converte Resultado Api Json em Lista
▪ Loop FOR da Lista de NFS

‣ Abre Pág. Portal Nacional NFS
‣ Mapeamento Campos Login
‣ Lista de Mapeamento Login
‣ Map Campo Login
‣ Map Campo Senha
‣ Map Botão Entrar
‣ Aguarda 3s
‣ Preenche Campos Login
‣ Lista de Ações de Login
‣ Preenche o Campo Usuário
‣ Preenche o Campo Senha
‣ Clica no Botão Entrar
‣ Aguarda 3s
‣ Mapeamento Campos NFS
‣ Lista de Mapeamento NFS
‣ Map Campo Data
‣ Map Campo Tomador
‣ Map Campo CNPJ Tomador
‣ Map Botão Avança 1
‣ Map Campo Cód. Serviço
‣ Map Botão Serv. Prestado
‣ Preenche Campos da Nota
‣ Lista de Ações dos Campos da Nota
‣ Clica no Campo Data
‣ Preenche o Campo Data
‣ Envia Tecla TAB
‣ Scroll 10x
‣ Aguarda 2s
‣ Clica Botão Tomador
‣ Aguarda 2s
‣ Preenche Campo CNPJ Tomador
‣ Envia Tecla TAB
‣ Aguarda 2s
‣ Clica Botão Avançar 1
‣ Aguarda 3s
‣ Clica em Município e Preenche
‣ Clica Cód. Serv. Prestado Preenche e Clica no Radio ISSQN
‣ Scroll 1x
‣ Map Campo Observação
‣ Preenche Campo de Observação
‣ Map Botão Avançar 2
‣ Clica Botão Avançar 2
‣ Aguarda 3s
‣ Map Campo Valor
‣ Preenche Campo Valor
‣ Envia Tecla TAB
‣ Scroll 2x
‣ Map Avançar 3
‣ Clica Botão Avançar 3
‣ Aguarda 1.8s
‣ Scroll 5x
‣ Map e Clica Botão Emitir
‣ Aguarda 0.5s
‣ Scroll 1x
‣ Map e Clica Botão Download
‣ Aguarda 2s Para Modal Captcha
‣ Entra no iframe hCaptcha
‣ Cria Variável Oculto como True
‣ While para aguardar até que o Captcha seja Resolvido NopeCaptcha

‣ Dorme 1s
‣ Mapear Sentinela iframe
‣ Verifica se Sentinela existe
‣ Quando Sentinela Existir Altera para False Variável Oculto

‣ Sentinela Existe?
‣ Se Sim, então Executa
‣ Altera Variável Oculto como False
‣ Dorme 2s
‣ Sair do iframe hCaptcha
‣ Map Botão Confirma
‣ Clica Botão Confirma
‣ Aguarda Download acontecer na pasta transitória
‣ Move e Renomeia
‣ Fecha o Navegador

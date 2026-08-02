# RPA de Emissão de NFS-e

Automação completa do ciclo de emissão de Nota Fiscal de Serviço Eletrônica no Portal Nacional, da consulta dos dados via API até o arquivamento do PDF.

**Stack:** Python · Prefect · BotCity · Selenium · NopeCaptcha

---

## Documentação

| Arquivo | Descrição |
|---------|-----------|
| [sequencia_atividades.md](sequencia_atividades.md) | Lista passo a passo das atividades executadas pelo robô |
| [documentation.md](documentation.md) | Documentação completa com MER, fluxogramas, diagrama de sequência e detalhamento técnico |


## Estrutura

```
├── bot.py               # Script principal do robô
├── Bot.xaml             # Workflow UiPath
├── NFS_NEW.jproj        # Projeto UiPath
├── prefect.yaml         # Orquestração Prefect
├── requirements.txt     # Dependências
├── .env                 # Variáveis de ambiente
├── perfil/              # Perfil Chrome (Selenium)
├── nfs/                 # PDFs de teste
├── download/            # PDFs emitidos
├── resources/           # Recursos auxiliares
└── doc_projeto/         # Documentação
```

## Funcionalidades

- Orquestração via Prefect com logs centralizados
- Login e preenchimento automático no Portal Nacional NFS-e
- Resolução automática de hCaptcha via NopeCaptcha
- Download e organização de PDFs por mês
- Tratamento de falhas com fail-safe por nota

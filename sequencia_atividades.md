# Sequência de Atividades do RPA NFS-e

> Ordem cronológica das ações executadas pelo robô no Portal Nacional de NFS-e.

---

## 1. Inicialização

### 1.1 Orquestrador
- Log de início — **Prefect**

### 1.2 Navegador
- Iniciar instância do **Google Chrome** (Chromedriver)

### 1.3 Setup de Navegador e Pastas

| # | Ação | Descrição |
|---|------|-----------|
| 1 | **Limpeza** | Finaliza instâncias anteriores do Chrome/Chromedriver para evitar bloqueios |
| 2 | **Diretórios** | Cria automaticamente a pasta de downloads para o mês atual |
| 3 | **Preferências** | Configura perfil Chrome e força download automático de PDFs |
| 4 | **Patches BotCity** | Injeta customizações do Selenium e auto-maximiza janela ao navegar |

---

## 2. Obtenção dos Dados

| Etapa | Descrição |
|-------|-----------|
| 2.1 | Pega data do sistema operacional |
| 2.2 | Formata data no padrão `dd/mm/aaaa` |
| 2.3 | Chamada à API de NFS |
| 2.4 | Converte resposta JSON em lista de objetos |

---

## 3. Loop de Emissão `FOR EACH`

> Repete os blocos abaixo para cada nota da lista retornada pela API.

### 3.1 Acesso ao Portal

| Ordem | Ação |
|-------|------|
| 1 | Abre página do Portal Nacional NFS-e |

### 3.2 Login

#### Mapeamento
| Elemento | Campo |
|----------|-------|
| Map 1 | Campo Usuário |
| Map 2 | Campo Senha |
| Map 3 | Botão **Entrar** |

#### Execução
| Ordem | Ação |
|-------|------|
| 1 | Aguarda 3s |
| 2 | Preenche campo **Usuário** |
| 3 | Preenche campo **Senha** |
| 4 | Clica no botão **Entrar** |
| 5 | Aguarda 3s |

### 3.3 Mapeamento do Formulário NFS-e

| Elemento | Campo |
|----------|-------|
| Map 1 | Campo **Data** |
| Map 2 | Campo **Tomador** |
| Map 3 | Campo **CNPJ Tomador** |
| Map 4 | Botão **Avançar 1** |
| Map 5 | Campo **Código de Serviço** |
| Map 6 | Botão **Serviço Prestado** |

### 3.4 Preenchimento da Nota

| Ordem | Ação | Espera |
|-------|------|--------|
| 1 | Clica no campo **Data** e preenche | — |
| 2 | Envia tecla `TAB` | — |
| 3 | Scroll ×10 | — |
| 4 | Aguarda | 2s |
| 5 | Clica no botão **Tomador** | — |
| 6 | Aguarda | 2s |
| 7 | Preenche campo **CNPJ Tomador** | — |
| 8 | Envia tecla `TAB` | — |
| 9 | Aguarda | 2s |
| 10 | Clica no botão **Avançar 1** | — |
| 11 | Aguarda | 3s |
| 12 | Clica em **Município** e preenche | — |
| 13 | Clica em **Cód. Serviço**, preenche e seleciona rádio **ISSQN** | — |
| 14 | Scroll ×1 | — |
| 15 | Mapeia e preenche campo **Observação** | — |
| 16 | Mapeia e clica botão **Avançar 2** | — |
| 17 | Aguarda | 3s |
| 18 | Mapeia e preenche campo **Valor** | — |
| 19 | Envia tecla `TAB` | — |
| 20 | Scroll ×2 | — |
| 21 | Mapeia e clica botão **Avançar 3** | — |
| 22 | Aguarda | 1.8s |
| 23 | Scroll ×5 | — |

### 3.5 Emissão e Download

| Ordem | Ação | Espera |
|-------|------|--------|
| 1 | Mapeia e clica botão **Emitir** | — |
| 2 | Aguarda | 0.5s |
| 3 | Scroll ×1 | — |
| 4 | Mapeia e clica botão **Download** | — |
| 5 | Aguarda abertura do modal captcha | 2s |

### 3.6 Resolução de hCaptcha

> A resolução do captcha é feita via **NopeCaptcha** (serviço externo).

```
  Entra no iframe hCaptcha
      │
      ▼
  Variável Oculto = True
      │
      ▼
  ┌─────────────────────┐
  │ While Oculto == True │
  │                     │
  │  Dorme 1s           │
  │  Mapeia Sentinela   │
  │  Sentinela existe?  │
  │    ├─ Não → volta   │
  │    └─ Sim → Oculto = False
  └─────────────────────┘
      │
      ▼
  Dorme 2s
      │
      ▼
  Sai do iframe hCaptcha
      │
      ▼
  Mapeia e clica botão Confirmar
```

### 3.7 Finalização da Nota

| Ordem | Ação |
|-------|------|
| 1 | Aguarda conclusão do download na pasta transitória |
| 2 | Move arquivo PDF para pasta do mês |
| 3 | Renomeia PDF conforme padrão definido |

---

## 4. Encerramento

| | |
|---|---|
| 4.1 | Fecha o navegador |
| 4.2 | Prefect registra log de conclusão |

# 🛡️ Governança e Matriz de Implementação de GPOs (Group Policy Objects)

Este documento centraliza a arquitetura, o padrão de governança e a **Matriz Corporativa de GPOs** aplicada no ambiente *On-Premise* do laboratório `Lab-suporte-infra`.

A estratégia adotada visa garantir a aplicação do **Princípio da Responsabilidade Única** (Single Responsibility Principle) e o modelo de **Privilégio Mínimo** (Least Privilege), separando rigorosamente políticas direcionadas a objetos de **Computador** de políticas direcionadas a objetos de **Usuário**.

---
## 📐 Padrão de Nomenclatura e Arquitetura

Para evitar o surgimento de "GPOs Monolíticas" e facilitar o processo de auditoria e *troubleshooting* via CLI (`gpresult`), adotou-se o padrão estrito de nomenclatura baseado em escopo e função:

* **`CGPO_` (Computer Group Policy Object):** Aplicadas exclusivamente no escopo de **Computador** (`Computer Configuration`). Impactam a máquina independentemente de quem realize o logon.
* **`UGPO_` (User Group Policy Object):** Aplicadas exclusivamente no escopo de **Usuário** (`User Configuration`). Impactam as permissões e o ambiente do colaborador independentemente da estação utilizada.

```text
[Sufixo Escopo] _ [Categoria Ação] _ [Descrição Recurso]
Exemplo: CGPO_SEC_Bloqueio_USB
```

## 📌 Matriz de GPOs Corporativos

Abaixo está a lista de políticas ativas no domínio. **Clique no nome ou no link de documentação da GPO** para acessar o sub-repositório contendo a exportação técnica (`.xml`), o caminhamento exato no GPMC e os prints de evidência técnica:

| **Identificador da GPO**               | **Escopo** | **Categoria**    | **Finalidade / Objetivo Técnico**                                  | **Documentação Detalhada**                                       |
| -------------------------------------- | ---------- | ---------------- | ------------------------------------------------------------------ | ---------------------------------------------------------------- |
| **`CGPO_SEC_Bloqueio_USB`**            | Computador | Segurança        | Bloqueio de leitura/escrita em mídias removíveis (DLP)             | [Acessar Guia 🔗](https://www.google.com/search?q=./&authuser=1) |
| **`UGPO_SEC_Restricao_CMD_Regedit`**   | Usuário    | Hardening        | Restrição de acesso interativo ao Prompt e Editor do Registro      | [Acessar Guia 🔗](https://www.google.com/search?q=./&authuser=1) |
| **`UGPO_MAP_Pastas_Compartilhadas`**   | Usuário    | Produtividade    | Mapeamento dinâmico de drivers SMB via _Item-Level Targeting_      | [Acessar Guia 🔗](https://www.google.com/search?q=./&authuser=1) |
| **`CGPO_SYS_WSUS_Config`**             | Computador | Gestão/Patch     | Apontamento e janelas de atualização via servidor WSUS interno     | [Acessar Guia 🔗](https://www.google.com/search?q=./&authuser=1) |
| **`CGPO_SEC_Bloqueio_Tela_Timeout`**   | Computador | Segurança Física | Bloqueio automático de sessão por inatividade após 5 minutos       | [Acessar Guia 🔗](https://www.google.com/search?q=./&authuser=1) |
| **`UGPO_SEC_Firewall_Regras_Locais`**  | Usuário    | Hardening        | Bloqueio de alteração e exceções no Windows Defender Firewall      | [Acessar Guia 🔗](https://www.google.com/search?q=./&authuser=1) |
| **`CGPO_SEC_LAPS_Admin_Local`**        | Computador | Credenciais      | Rotatividade automática e complexidade de senha via LAPS           | [Acessar Guia 🔗](https://www.google.com/search?q=./&authuser=1) |
| **`UGPO_ENV_Redirecionamento_Pastas`** | Usuário    | Backup           | Redirecionamento de Área de Trabalho/Documentos para o File Server | [Acessar Guia 🔗](https://www.google.com/search?q=./&authuser=1) |
| **`CGPO_SEC_Desativar_SMBv1`**         | Computador | Hardening        | Mitigação de vulnerabilidades e desativação do protocolo SMBv1     | [Acessar Guia 🔗](https://www.google.com/search?q=./&authuser=1) |
| **`UGPO_ENV_Papel_Parede_Corp`**       | Usuário    | Identidade       | Padronização e travamento do plano de fundo institucional          | [A](https://www.google.com/search?q=./&authuser=1)               |

## 🔄 Fluxo de Aplicação e Precedência

As políticas estão vinculadas às Unidades Organizacionais (OUs) seguindo a hierarquia abaixo:

Plaintext

```
techcorp.local (Domínio)
 └── OU=Empresa_TECHCORP
      ├── OU=Computadores (Aplica todas as CGPOs)
      └── OU=Usuarios     (Aplica todas as UGPOs)
```

1. **Ordem de Processamento:** Local $\rightarrow$ Site $\rightarrow$ Domain $\rightarrow$ Organizational Unit (LSDOU).
    
2. **Filtragem de Segurança:** As UGPOs utilizam _Security Filtering_ e _Item-Level Targeting (ILT)_ para garantir que apenas os grupos autorizados (ex: `GRP_RH_Users`) recebam configurações específicas sem necessidade de novas OUs.
    

## 🛠️ Validação Técnica e Auditoria

Para validar a correta aplicação do conjunto de diretrizes acima no ambiente de testes, utilize os comandos de auditoria no terminal da máquina cliente:

PowerShell

```
# Verificar todas as GPOs aplicadas ao Computador e Usuário atual
gpresult /r

# Gerar relatório detalhado em HTML para auditoria
gpresult /h C:\Logs\GPO_Report.html
```

> ⬅️ **Voltar para o passo a passo de AD DS:** [README etapas-ad-ds](https://www.google.com/search?q=../&authuser=1)
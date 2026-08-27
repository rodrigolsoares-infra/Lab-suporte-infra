### Etapa 6: Auditoria de Pré-Migração e Validação "Entra ID Ready"

Este repositório documenta a etapa final de preparação da infraestrutura *On-Premise*. Antes de realizar a migração ou sincronização com o **Microsoft Entra ID (Azure AD)**, um Analista N2 precisa garantir a integridade dos serviços do Active Directory local e realizar a sanitização da base de identidades.

---
## 📋 Visão Geral da Etapa 6

| Atividade / Teste              | Ferramenta Utilizada | Finalidade / Objetivo                                             | Status de Validação                   |
| :----------------------------- | :------------------- | :---------------------------------------------------------------- | :------------------------------------ |
| **Diagnóstico do AD DS**       | `dcdiag.exe` (CLI)   | Testes de integridade em DNS, SYSVOL e Netlogon                   | `PASSED` (Aprovado)                   |
| **Sanitização de Identidades** | Microsoft IdFix Tool | Identificar conflitos de UPN, caracteres inválidos e duplicidades | `Clean / Ready`                       |
| **Checkpoint Final**           | Hyper-V Manager      | Ponto de restauração limpo e pronto para o ambiente Híbrido       | `CKP-ETAPA6-ADDS-HEALTHY-ENTRA-READY` |

---
## ⚙️ Procedimento de Execução

### 1. Diagnóstico do Active Directory DS (`dcdiag`)
Abertura do terminal PowerShell como Administrador no controlador de domínio `DC01-CORP` e execução dos testes essenciais de saúde do sistema:

```powershell
dcdiag /v /test:dns /test:sysvol /test:netlogon
```
- **Itens Auditados:**
    
    - **Test: DNS:** Validação de resolução de nomes, registros SRV e delegação interna.
        
    - **Test: SYSVOL:** Verificação do compartilhamento e integridade de pastas de sistema.
        
    - **Test: Netlogon:** Checagem da disponibilidade do serviço de autenticação do domínio.
        

### 2. Sanitização de Objetos para Nuvem (Microsoft IdFix)

Instalação e execução do **Microsoft IdFix** para varredura do diretório `techcorp.local`. A ferramenta analisa todos os usuários e grupos em busca de incompatibilidades com os critérios de sincronização do Entra Connect.

- **Ações de Correção:**
    
    - Confirmação do sufixo UPN roteável `@techcorp.com.br` para todas as contas ativas (ex: `rodrigo.soares@techcorp.com.br`).
        
    - Remoção de espaços em branco e caracteres especiais não suportados no atributo `sAMAccountName` e nomes de exibição.
        

#### 📸 Evidências Visuais:
<details>
<p align="center">
  <img src=".github/assets/15-dhcp-scope-active.png" alt="Resultado do Diagnóstico dcdiag no Terminal." width="500"><br>
  <i>Figura 1: Resultado do Diagnóstico dcdiag no Terminal.</i>
</p>
<p align="center">
  <img src=".github/assets/16-file-server-folders.png" alt="Varredura de Identidades com a Ferramenta Microsoft IdFix." width="500"><br>
  <i>Figura 1: Varredura de Identidades com a Ferramenta Microsoft IdFix.</i>
</p>
</details>

## 🛠️ Relatório de Casos de Troubleshooting (Sanitização Pré-Nuvem)

- **Sintoma:** Ao rodar a varredura inicial no IdFix, a conta do usuário `Rodrigo Soares` foi sinalizada com o tipo de alerta _ERROR: Invalid UPN Domain_.
    
- **Causa Raiz:** O usuário havia sido cadastrado com o sufixo padrão de instalação `.local` (`rodrigo.soares@techcorp.local`), que não pode ser validado em locatários de nuvem.
    
- **Solução Aplicada:**
    
    1. Acesso ao console `dsa.msc` na OU `TI`.
        
    2. Ajuste na aba _Conta (Account)_ alterando o sufixo do nome de logon para `@techcorp.com.br`.
        
    3. Re-execução da consulta (`Query`) no IdFix, confirmando a resolução do conflito.
        
## 🎯 Estado Final do Laboratório On-Premise

Com a conclusão desta etapa, o ambiente local atinge a maturação necessária para operar em ambiente de produção e está tecnicamente aprovado (**Entra ID Ready**) para os seguintes cenários:

1. **Sincronização Híbrida:** Instalação e configuração do Microsoft Entra Connect.
    
2. **Federated Identity / SSO:** Integração de identidades para login único em aplicações SaaS.
    
3. **Migração para Azure:** Extensão do Domain Controller para uma máquina virtual no Microsoft Azure.
    
## ➡️ Próximos Passos (Continuação para Nuvem Híbrida)

A infraestrutura mantida neste repositório representa o estado final do ambiente _On-Premise_. O próximo repositório da trilha documenta a extensão das identidades locais para o ambiente de nuvem da Microsoft:

👉 **Próximo Laboratório:** [Lab-infra-cloud](https://www.google.com/search?q=https://github.com/seu-usuario/Lab-infra-cloud&authuser=1) _(Integração com Microsoft Entra ID via Entra Connect, Licenciamento e Gestão Híbrida)_.
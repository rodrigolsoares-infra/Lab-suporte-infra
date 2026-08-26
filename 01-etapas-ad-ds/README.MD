# Implementação de Infraestrutura Active Directory (AD DS)
## 🏢 Problema do Negócio
A empresa não possuía uma gestão centralizada de usuários, computadores e políticas de segurança. Sem um domínio corporativo, a administração de credenciais e permissões era realizada individualmente em cada máquina, gerando brechas de segurança, falta de auditoria de acessos e alto impacto operacional na rotina do suporte N1.
## 🛠️ Solução Implementada
Promoção do servidor `SRV-DC01` a Controlador de Domínio (DC) da floresta `techcorp.local`. Foi estruturada uma hierarquia de Unidades Organizacionais (OUs) dividida por departamentos e criadas as contas de usuários e grupos de segurança seguindo o modelo RBAC (*Role-Based Access Control*).

---
## 💻 Informações do Servidor (DC)
* **Nome do Servidor:** `SRV-DC01`
* **Domínio FQDN:** `techcorp.local`
* **NetBIOS:** `TECHCORP`
* **Endereço IP Static:** `192.168.10.10/24`
* **DNS Primary:** `127.0.0.1`
* **Virtual Switch:** `LAB-TECHCORP` (Hyper-V)
## 📋 Pré-requisitos
* Servidor: Windows Server 2019/2022 com a função AD DS instalada.
* Permissões: Privilégios de Administrador Local (para promoção) ou Domain Admin (pós-promoção).
* Rede: Endereço IP estático configurado na interface do servidor.

---
## 📋 Visão Geral da Topologia

| Ativo / VM | Sistema Operacional | Função / Hostname | Endereço IP |
| :--- | :--- | :--- | :--- |
| **Domain Controller** | Windows Server 2022 Standard | `DC01.techcorp.local` | `192.168.10.10 /24` |
| **Estação de Trabalho 01** | Windows 11 Pro | `CLI-TI-01` | `DHCP (192.168.10.50)` |
| **Gateway / Router** | pfSense / Router Virtual | `GW-CORP` | `192.168.10.1 /24` |

---
## 📐 Diagrama da Arquitetura
```text
+-----------------------------------------------------------------------+

| REDE CORPORATIVA (192.168.10.0/24) |
| :--- |
| +-------------------------+             +-------------------------+ |
|  | DC01-SERVER |  | CLI01-WIN11 |  |
|  | Windows Server 2022 |  | Windows 11 Pro |  |
| :--- | :--- | :--- | :--- | :--- |
|  | • AD DS (corp.local) | Conexão | • Ingressado no Domínio |  |
|  | • DNS Server | <=========> | • Mapeamentos via GPO |  |
|  | • DHCP Server | Ethernet | • Restrições Aplicadas |  |
|  | • File Server (SMB) |  |  |  |
|  | IP: 192.168.10.10 |  | IP: 192.168.10.50 (DHCP) |  |
| +-------------------------+             +-------------------------+ |

+-----------------------------------------------------------------------+ ```

---
## 🏗️ Estrutura de Unidades Organizacionais (OUs) e Grupos

### Unidade Organizacional Raiz: `TechCorp`

| Sub-OU | Função / Descrição | Grupos Associados |
| :--- | :--- | :--- |
| `OU_TI` | Equipe de Tecnologia e Administração | `GRP_TI_Admins` |
| `OU_Financeiro` | Setor Financeiro e Contabilidade | `GRP_Financeiro_RW` |
| `OU_RH` | Recursos Humanos e Pessoal | `GRP_RH_RW` |
| `OU_Vendas` | Equipe Comercial | `GRP_Vendas_RW` |
| `OU_Diretoria` | Gestão Executiva | - |
| `OU_Computadores` | Estações de trabalho ingressadas | - |
| `OU_Grupos` | Armazenamento de Grupos de Segurança | Todos os grupos |

## 📐 Diagrama da Estrutura de Domínio
```mermaid
graph TD
    A[Dominio: techcorp.local] --> B[OU: techcorp]
    A --> C[OU: OU_Computadores]
    A --> D[OU: OU_Grupos]
    
    B --> E[Usuario: mariana.costa]
    D --> F[Grupo: GRP_RH_RW]
    F -->|Atribuido a| E
```

## 🖼️ Evidências de Implantação

### 1. Promoção do Servidor a Controlador de Domínio
![Dominio Promovido](img/01-dominio-promovido.png)

### 2. Estrutura de OUs e Objetos de Usuários
![Estrutura OUs e Usuarios](img/02-estrutura-ous-usuarios.png)




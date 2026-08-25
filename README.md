# 🖥️ Lab-suporte-infra | Infraestrutura On-Premise, Active Directory DS & GPOs
### Este repositório documenta a implementação prática de uma infraestrutura de rede corporativa *On-Premise* do zero. O objetivo deste laboratório é simular cenários reais de administração de servidores, gestão de identidades com Active Directory Domain Services (AD DS), aplicação de políticas de grupo (GPOs), elaboração de POPs (Procedimentos Operacionais Padrão) e resolução de incidentes (troubleshooting) de Suporte N1/N2.
---
## 📝 Projetos
### [Etapas de Implementação AD DS](./)
   * Configuração de servidor Active Directory, Unidades Organizacionais (OUs) e GPOs no Windows Server.
### [Configurando serviços de rede DHCP, DNS e Servidor de arquivos NTFS](./)
   * Configuração de Servidor DHCP e Resolução Reversa DNS e implementação de File Server com Permissões Compartilhadas e NTFS.
### [Aplicação de políticas de grupo (GPO)](./)
   * Criando, aplicando e testando políticas de grupos básicas.
### [Procedimento Operacional Padrão (POP)](./)
   * POP de Backup básico e Retenção de Dados (VSS & Cobian Reflector)
   * POP de Gestão de Print Server e Manutenção do Spooler de Impressão.
### [5. Resolução de incidentes (Troubleshooting)](./)
   * KBA

---
## 📋 Visão Geral da Topologia

| Ativo / VM | Sistema Operacional | Função / Hostname | Endereço IP |
| :--- | :--- | :--- | :--- |
| **Domain Controller** | Windows Server 2022 Standard | `DC01.corp.local` | `192.168.10.10 /24` |
| **Estação de Trabalho 01** | Windows 11 Pro | `CLI01-WIN11` | `DHCP (192.168.10.50)` |
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

+-----------------------------------------------------------------------+
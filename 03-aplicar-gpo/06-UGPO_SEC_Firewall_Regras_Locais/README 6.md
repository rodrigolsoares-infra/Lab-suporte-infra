## 🛠️ Detalhamento e Passo a Passo da GPO

#### Implementação de Políticas de Grupo (GPOs) A infraestrutura foi configurada com um modelo de governança baseado em separação de escopos (`CGPO_` para Computador e `UGPO_` para Usuário). Para visualizar a **Matriz de GPOs Corporativos**, a arquitetura de linkagem nas OUs e acessar a documentação individual de cada uma das 10 políticas aplicadas, acesse: 
## 👉 **[Acessar a Matriz e Documentação de GPOs](./aplicar-gpo.md)** 

### 6. `UGPO_SEC_Firewall_Regras_Locais`

- **Objetivo:** Bloquear a alteração e criação de exceções no Windows Defender Firewall por usuários.
    
- **Link da OU:** `OU=Usuarios,OU=Empresa_CORP`
    
- **Caminho no GPMC:** `User Configuration -> Policies -> Administrative Templates -> Network -> Network Connections`
    
- **Passo a Passo:**
    
    1. Habilitar `Prohibit access to properties of components of a LAN connection`.
        
    2. Habilitar `Prohibit use of Internet Connection Firewall on your DNS domain network` (opcional conforme politica).
        
- **Evidência Visual (Link do Print):**
    
    Markdown
    
    ```
    ![Evidência Firewall Travado](.github/assets/gpo-ugpo-sec-firewall-lock.png)
    ```
    
    _(Sugestão de print: Interface do Windows Defender Firewall indicando que o controle é mantido pelo administrador)_
    
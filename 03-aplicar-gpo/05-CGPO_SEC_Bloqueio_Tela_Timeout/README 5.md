## 🛠️ Detalhamento e Passo a Passo da GPO

#### Implementação de Políticas de Grupo (GPOs) A infraestrutura foi configurada com um modelo de governança baseado em separação de escopos (`CGPO_` para Computador e `UGPO_` para Usuário). Para visualizar a **Matriz de GPOs Corporativos**, a arquitetura de linkagem nas OUs e acessar a documentação individual de cada uma das 10 políticas aplicadas, acesse: 
## 👉 **[Acessar a Matriz e Documentação de GPOs](./aplicar-gpo.md)** 

### 5. `CGPO_SEC_Bloqueio_Tela_Timeout`

- **Objetivo:** Forçar o bloqueio da estação de trabalho por inatividade após 5 minutos.
    
- **Link da OU:** `OU=Computadores,OU=Empresa_CORP`
    
- **Caminho no GPMC:** `Computer Configuration -> Policies -> Administrative Templates -> Control Panel -> Personalization`
    
- **Passo a Passo:**
    
    1. Habilitar `Enable screen saver`.
        
    2. Habilitar `Password protect the screen saver`.
        
    3. Habilitar `Screen saver timeout` -> Definir valor em segundos: `300`.
        
- **Evidência Visual (Link do Print):**
    
    Markdown
    
    ```
    ![Evidência Proteção de Tela](.github/assets/gpo-cgpo-sec-screensaver-lock.png)
    ```
    
    _(Sugestão de print: Painel de Controle de Proteção de Tela com os campos esmaecidos/bloqueados para edição)_
    
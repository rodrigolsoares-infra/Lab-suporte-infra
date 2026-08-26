## 🛠️ Detalhamento e Passo a Passo da GPO

#### Implementação de Políticas de Grupo (GPOs) A infraestrutura foi configurada com um modelo de governança baseado em separação de escopos (`CGPO_` para Computador e `UGPO_` para Usuário). Para visualizar a **Matriz de GPOs Corporativos**, a arquitetura de linkagem nas OUs e acessar a documentação individual de cada uma das 10 políticas aplicadas, acesse: 
## 👉 **[Acessar a Matriz e Documentação de GPOs](./aplicar-gpo.md)** 

### 10. `UGPO_ENV_Papel_Parede_Corp`

- **Objetivo:** Fixar o plano de fundo institucional corporativo e impedir a troca por imagens pessoais.
    
- **Link da OU:** `OU=Usuarios,OU=Empresa_CORP`
    
- **Caminho no GPMC:** `User Configuration -> Policies -> Administrative Templates -> Desktop -> Desktop`
    
- **Passo a Passo:**
    
    1. Habilitar `Desktop Wallpaper` -> Inserir em _Wallpaper Name_ o caminho UNC: `\\DC01\NETLOGON\wallpapers\corp-wallpaper.png` (Style: _Fill_).
        
    2. Habilitar `Prevent changing wallpaper`.
        
- **Evidência Visual (Link do Print):**
    
    Markdown
    
    ```
    ![Evidência Wallpaper Corporativo](.github/assets/gpo-ugpo-env-wallpaper-lock.png)
    ```
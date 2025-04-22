## Guia de Referência Rápida: Git Básico Local

Este guia reúne os conceitos e comandos essenciais do Git que discutimos, focando no uso local para versionar seu projeto (como o `meu_guia_git`).

<u>**Conceitos Fundamentais (Baseados em Nossas Conversas):**</u>

1. **O Que é um Repositório Git?**
   
   * É uma pasta comum do seu computador que você "ensinou" a rastrear seu próprio histórico usando o comando `git init`.
   * A mágica acontece em uma subpasta oculta chamada `.git` criada dentro do seu diretório. Pense nela como o "caderno de registros" ou o "cérebro" do Git para aquele projeto. Você não interage diretamente com ela, mas ela guarda todo o histórico.

2. **Git Não Salva Automaticamente (É Deliberado):**
   
   * Diferente de um "Salvar" no editor, o Git não registra versões automaticamente quando você salva um arquivo, cria ou copia algo.
   * O versionamento no Git é um processo **manual** em duas etapas: `git add` (preparar) e `git commit` (registrar). Isso garante que cada "versão" (commit) no histórico seja significativa e represente um conjunto lógico de mudanças.

3. **Os Três "Espaços" do Git:**
   
   * **Diretório de Trabalho (Working Directory):** Sua pasta normal (`meu_guia_git`) com os arquivos que você vê e edita (sua "mesa de trabalho").
   * **Área de Preparação (Staging Area / Index):** Uma área intermediária onde você coloca as mudanças específicas que deseja incluir no *próximo* commit (`git add`). É como colocar os papéis prontos em uma "bandeja para arquivar".
   * **Repositório (.git Directory):** Onde o Git armazena permanentemente o histórico completo do projeto, incluindo todos os commits (as "fotos arquivadas" na pasta `.git`).

4. **Commits são "Fotos" Completas (Snapshots):**
   
   * Cada `git commit` tira uma "foto" (snapshot) do estado de *todos os arquivos rastreados* naquele momento, conforme preparados na Staging Area.
   * Ele **não sobrescreve** o histórico anterior; ele adiciona um novo ponto na linha do tempo, preservando todas as versões passadas. Você não perde o histórico ao fazer novos commits.

5. **Ignorando Arquivos (`.gitignore`):**
   
   * Você pode (e deve) dizer ao Git para ignorar certos arquivos ou pastas que não precisam fazer parte do histórico (arquivos temporários, logs, configurações pessoais, etc.).
   * Isso é feito criando um arquivo de texto chamado `.gitignore` na raiz do seu repositório e listando nele os padrões a serem ignorados. Arquivos ignorados não são rastreados e, portanto, não entram nos commits nem nos backups do Git.

6. **Visualizando o Passado Sem Perder o Presente:**
   
   * Comandos como `git checkout <ID_do_commit>` permitem "viajar no tempo" e ver seus arquivos exatamente como estavam em um commit anterior.
   * Isso **restaura temporariamente** os arquivos na sua pasta de trabalho para aquele estado antigo.
   * Importante: Os commits mais recentes **não são perdidos**. Eles continuam existindo no histórico. Você pode sempre voltar ao estado mais atual usando `git checkout main` (ou `master`).

<u>**Comandos Essenciais (Compilados):**</u>

* `cd /caminho/para/sua/pasta`
  
  * **O que faz:** Navega pelo terminal até o diretório do seu projeto.
  * **Quando usar:** Sempre antes de rodar comandos Git, para garantir que está operando na pasta correta.

* `git init`
  
  * **O que faz:** Inicializa um repositório Git na pasta atual. Cria a subpasta oculta `.git`.
  * **Quando usar:** Uma única vez, no início, para transformar uma pasta comum em um repositório Git.

* `git status`
  
  * **O que faz:** Mostra o estado atual do seu repositório: quais arquivos foram modificados, quais estão na Staging Area (prontos para commit), quais são novos e ainda não rastreados (`untracked`).
  * **Quando usar:** **MUITO FREQUENTEMENTE!** Antes de adicionar, antes de commitar, depois de commitar... é seu principal comando para entender o que está acontecendo.

* `git add <nome_do_arquivo>` ou `git add .`
  
  * **O que faz:** Adiciona as mudanças do arquivo especificado (ou todas as mudanças no diretório atual e subdiretórios, se usar `.`) à Staging Area. Prepara as mudanças para o próximo commit.
  * **Quando usar:** Depois de modificar/criar arquivos e antes de fazer `git commit`. Use `.` como um atalho comum para adicionar tudo que mudou.

* ***NOVO*** `git restore --staged <nome_do_arquivo>`
  
  * **O que faz:** Remove um arquivo da Staging Area (o "desfaz" do `git add`). O arquivo continua modificado no seu Diretório de Trabalho, mas não está mais preparado para o próximo commit. (Em versões mais antigas do Git, `git reset HEAD <nome_do_arquivo>` tinha um efeito similar para este caso).
  * **Quando usar:** Quando você usou `git add` em um arquivo por engano e decidiu que ele *não* deve fazer parte do próximo commit. Útil para "limpar" a Staging Area antes de commitar.

* `git commit -m "Sua mensagem descritiva aqui"`
  
  * **O que faz:** Grava permanentemente no histórico do repositório um snapshot de tudo que está na Staging Area. A mensagem (`-m`) é **obrigatória** e crucial para descrever *o que* foi feito neste commit.
  * **Quando usar:** Após usar `git add` para preparar as mudanças que formam uma unidade lógica de trabalho.

* ***NOVO*** `git commit --amend`
  
  * **O que faz:** Permite **alterar o commit mais recente**. 
  * **Usos comuns:**
    * **Corrigir a mensagem do último commit:** Abre o editor de texto configurado no Git para você editar a mensagem. Se quiser apenas mudar a mensagem sem adicionar arquivos, pode usar `git commit --amend -m "Nova mensagem correta"`.
    * **Adicionar arquivos esquecidos ao último commit:** Se você commitou e logo depois percebeu que esqueceu de adicionar um arquivo (`git add arquivo_esquecido.txt`), pode adicioná-lo agora e rodar `git commit --amend`. Ele será incluído no commit anterior.
    * **Importante:** Este comando **reescreve** o último commit. O commit original é descartado e um *novo* commit (com um novo ID/hash) é criado em seu lugar. É seguro para commits que ainda estão apenas no seu repositório local.
    * **Quando usar:** **Imediatamente após** fazer um commit, ao perceber um erro na mensagem ou que esqueceu de incluir pequenas alterações que pertencem logicamente àquele commit.

* `git log`
  
  * **O que faz:** Exibe o histórico de commits, mostrando cada commit com seu ID (hash), autor, data e mensagem. O commit mais recente aparece no topo.
  * **Quando usar:** Para ver a linha do tempo do seu projeto, encontrar IDs de commits antigos, entender o progresso. (Pressione `q` para sair da visualização do log se ele ocupar a tela toda).

* `git show [<ID_do_commit>]`
  
  * **O que faz:** Por padrão (sem argumentos), mostra informações detalhadas sobre o **commit mais recente** (HEAD). Isso inclui seu ID completo, autor, data, a mensagem e, crucialmente, as **alterações exatas (o "diff")** que esse commit introduziu nos arquivos. Se um `<ID_do_commit>` for fornecido, mostra os detalhes daquele commit específico em vez do último.
  * **Quando usar:** Para **inspecionar rapidamente o que foi feito no último commit**: ver sua mensagem completa e, mais importante, quais linhas foram adicionadas/removidas nos arquivos. É muito útil para confirmar se o commit contém exatamente o que você esperava. Também é a forma padrão de ver os detalhes e as mudanças de **qualquer commit antigo** no histórico, usando seu ID (obtido com `git log`).

* `touch .gitignore` (ou crie via editor)
  
  * **O que faz:** Cria o arquivo `.gitignore`. Edite-o com um editor de texto para adicionar os padrões a ignorar.
  * **Quando usar:** Quando precisar instruir o Git a não rastrear certos arquivos/pastas. Lembre-se de adicionar e commitar o próprio `.gitignore`!

* `git checkout <ID_do_commit_ou_nome_do_branch>`
  
  * **O que faz (uso básico):** Restaura os arquivos da pasta de trabalho para o estado de um commit específico (usando o ID obtido com `git log`) ou muda para outro branch (como `main` ou `master`).
  * **Quando usar:** Para inspecionar um estado anterior do projeto ou para retornar ao estado mais recente (`git checkout main`). Use com cuidado inicial, sabendo que ele altera seus arquivos visíveis (mas não perde histórico).

---

**Diretriz Passo a Passo: Seu Primeiro Repositório e Commit**

Vamos aplicar isso na prática no seu diretório `/home/skygastech/Workspace/meu_guia_git`.

**(Sobre o Terminal: Qt Terminal vs. VS Code)**
Para estes comandos básicos, **tanto faz**. Ambos funcionam exatamente da mesma maneira porque apenas invocam o programa `git` instalado no seu sistema. **Use o Qt Terminal do Linux, como você prefere.** Ele é perfeito para isso e evita adicionar a complexidade do VS Code por enquanto.

**Passos:**

1. **Abra o Qt Terminal.**

2. **Navegue até seu diretório:**
   
   ```bash
   cd /home/skygastech/Workspace/meu_guia_git
   ```
   
   *(Confirme com `pwd` se quiser ter certeza)*

3. **Inicialize o Repositório:**
   
   ```bash
   git init
   ```
   
   *(Você verá a mensagem "Initialized empty Git repository...")*

4. **Crie seu arquivo guia inicial:** Abra o Mark Text (ou outro editor) e crie o arquivo `ComandosLinux.md` dentro de `/home/skygastech/Workspace/meu_guia_git`. Adicione algum conteúdo inicial (ex: `# Meu Guia de Comandos Linux`) e **salve o arquivo**.

5. **Verifique o Status:** Volte ao terminal e digite:
   
   ```bash
   git status
   ```
   
   *(O Git deve listar `ComandosLinux.md` na seção "Untracked files" (arquivos não rastreados), pois ele é novo e o Git ainda não foi instruído a cuidar dele).*

6. **Adicione o Arquivo à Staging Area:**
   
   ```bash
   git add ComandosLinux.md
   ```
   
   *(Alternativa comum: `git add .` que adicionaria este e quaisquer outros arquivos novos/modificados no diretório)*

7. **Verifique o Status Novamente:**
   
   ```bash
   git status
   ```
   
   *(Agora, `ComandosLinux.md` deve aparecer em "Changes to be committed" (mudanças prontas para commit), indicando que está na Staging Area).*

8. **Faça seu Primeiro Commit:**
   
   ```bash
   git commit -m "Commit inicial: Adiciona arquivo base ComandosLinux.md"
   ```
   
   *(Escolha uma mensagem clara! Você verá uma confirmação sobre o commit).*

9. **Verifique o Status Final:**
   
   ```bash
   git status
   ```
   
   *(Agora deve dizer algo como "nothing to commit, working tree clean", indicando que tudo está salvo no histórico e não há mudanças pendentes).*

10. **Visualize sua Linha do Tempo!**
    
    ```bash
    git log
    ```
    
    *(Você verá a entrada para o seu primeiro commit, com o ID longo (hash), seu nome/email como autor, a data e a mensagem que você escreveu! Pressione `q` para sair se necessário).*

**Parabéns! Você acabou de criar seu primeiro repositório Git local e registrar sua primeira versão!**

**Próximo Passo Pertinente (Para Fixar o Ciclo):**

11. **Modifique o Arquivo:** Abra `ComandosLinux.md` novamente, adicione mais conteúdo (ex: a explicação do comando `pwd`), e salve.
12. **Verifique o Status:** `git status` (mostrará `ComandosLinux.md` como "modified").
13. **Adicione as Mudanças:** `git add ComandosLinux.md` (ou `git add .`)
14. **Faça o Segundo Commit:** `git commit -m "Adiciona explicação do comando pwd"`
15. **Veja o Histórico Atualizado:** `git log` (agora você verá *dois* commits na sua linha do tempo!).

---

Salve este texto! Use-o como referência e, mais importante, **pratique** esses comandos no seu terminal. A repetição desse ciclo (`status` -> modificar -> `add` -> `status` -> `commit` -> `log`) é a chave para internalizar o fluxo básico do Git.

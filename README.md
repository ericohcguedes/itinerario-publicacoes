# Itinerário de Publicações — Jardim do Vale

Página única (`index.html`), sem servidor, sem instalação — só abrir no navegador.
Transforma a planilha original em um painel interativo: em vez de digitar "1", você **clica no carimbo** para marcar Sentinela, Sentinela (letra grande), Apostila, cada bimestre e "Cancelado". Tem também um resumo com os totais no topo, uma barra de progresso por bimestre, sincronização em tempo real entre dispositivos e login com e-mail e senha (ambos opcionais — veja abaixo).

## Como publicar no GitHub (para outras pessoas acessarem pelo link)

1. Crie um repositório novo no GitHub (ex.: `itinerario-publicacoes`), público.
2. Envie os arquivos desta pasta (`index.html` e este `README.md`) para o repositório.
   - Pelo site do GitHub: botão **Add file → Upload files**, arraste o `index.html` e clique em **Commit changes**.
3. Vá em **Settings → Pages** (barra lateral esquerda).
4. Em **Branch**, selecione `main` e a pasta `/ (root)`, depois **Save**.
5. Espere ~1 minuto. O GitHub mostrará o link, algo como:
   `https://SEU-USUARIO.github.io/itinerario-publicacoes/`
6. Compartilhe esse link com quem precisar acessar.

Qualquer atualização: basta editar o `index.html` no GitHub (ou subir uma nova versão) — o site atualiza sozinho em cerca de 1 minuto.

## Como os dados são salvos

Por padrão (sem configurar nada), cada marcação fica salva **só no navegador de quem está usando** (localStorage). Isso quer dizer que marcar algo no celular não aparece automaticamente no computador de outra pessoa — é preciso Exportar/Importar manualmente (veja abaixo).

Se você quer que **todo mundo veja e edite as mesmas marcações, ao vivo**, siga a seção "Ativar sincronização em tempo real" logo abaixo. É opcional, mas é o "site de verdade" — sem depender de planilha nenhuma.

### Ativar sincronização em tempo real (Firebase — grátis)

O `index.html` já vem preparado para isso; falta só criar um banco gratuito e colar uma chave de configuração. Leva uns 10 minutos, sem precisar programar.

1. Acesse **console.firebase.google.com**, entre com uma conta Google e clique em **Criar um projeto** (pode ser o mesmo Google que já usam). Dê um nome, ex.: `itinerario-jardim-do-vale`. O plano gratuito ("Spark") é suficiente.
2. No menu lateral, vá em **Compilação → Firestore Database → Criar banco de dados**.
   - Escolha **modo de produção**.
   - Na região, selecione **southamerica-east1 (São Paulo)**.
3. Clique na aba **Regras** dentro do Firestore e substitua o conteúdo por:
   ```
   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       match /itinerario/{doc} {
         allow read, write: if request.auth != null;
       }
     }
   }
   ```
   Clique em **Publicar**. Essa regra (`request.auth != null`) exige que a pessoa esteja logada para ler ou editar — é a que combina com o login e senha configurados no passo 3.5 abaixo.

### 3.5. Criar o login (e-mail e senha)

1. No menu lateral do Firebase, vá em **Compilação → Authentication → Vamos começar (Get started)**.
2. Na lista de provedores, clique em **E-mail/senha** e **ative** a primeira opção ("E-mail/senha"). Salve.
3. Vá na aba **Users** (Usuários) → **Adicionar usuário**.
4. Cadastre um e-mail e uma senha para quem vai controlar o itinerário — por exemplo `jardimdovale@algumprovedor.com` com uma senha só do grupo. Pode cadastrar mais de um usuário aqui, um para cada pessoa que precisa editar (repita este passo).
5. Esse e-mail/senha é o que a pessoa vai digitar na tela de login do site — não precisa ser um e-mail real, só um identificador (ex.: `superintendente@jardimdovale.local` funciona, já que o Firebase não manda nada para essa caixa de entrada).
4. Volte à tela inicial do projeto → ícone de **engrenagem → Configurações do projeto** → aba **Geral** → role até "Seus apps" → clique no ícone **`</>`** (Web) → dê um apelido e **registre o app** (não precisa marcar Firebase Hosting).
5. O Firebase vai mostrar um bloco de código com `apiKey`, `authDomain`, `projectId`, etc. Copie esses valores.
6. Abra o `index.html` num editor de texto, procure por `FIREBASE_CONFIG` (perto do topo do `<script>`) e cole os valores no lugar de cada `"COLE_AQUI"`.
7. Suba o arquivo atualizado no GitHub (substituindo o antigo). Espere ~1 minuto e pronto: o site vai pedir **e-mail e senha** antes de mostrar qualquer coisa (use o que você cadastrou no passo 3.5), e o rodapé vai mostrar **"● Sincronizado"** depois de logar. Qualquer marcação passa a aparecer para todo mundo que estiver logado, na hora.

**Para dar acesso a mais pessoas:** repita o passo 3.5 (Authentication → Users → Adicionar usuário) para cada pessoa. Para tirar o acesso de alguém, exclua o usuário dela ali mesmo — não precisa mexer no site.

**Se esquecer a senha:** em Authentication → Users, clique nos três pontinhos ao lado do usuário → "Redefinir senha" (ou apague e recrie o usuário).

Se algum dia quiser desativar, é só deixar `FIREBASE_CONFIG` como estava (com `"COLE_AQUI"`) — o site volta a funcionar em modo local, sozinho.

### Exportar / Importar (backup manual, com ou sem Firebase)

- **Exportar dados** → baixa um arquivo `.json` com tudo que está marcado (bom para backup, mesmo com a sincronização ativada).
- **Importar dados** → carrega um `.json` exportado antes, substituindo os dados atuais (no modo local) ou os dados de todos (no modo sincronizado).
- **Restaurar planilha original** → volta para a lista de nomes da planilha do Google, zerando as marcações de bimestre.

## O que dá para fazer na página

- **Adicionar publicador** (+ botão no topo): escolhe o grupo (ou digita um novo), nome, e já marca o tipo de publicação.
- **Editar o nome**: clique no nome do publicador na lista e digite; ele salva ao sair do campo.
- **Remover** um publicador: ✕ no fim da linha.
- **Buscar/filtrar**: por nome, por grupo, ou por tipo de publicação/cancelados.
- **Expandir/recolher** grupos, um por um ou todos de uma vez.
- **Imprimir** (ou salvar como PDF) usando o botão Imprimir.

## Testar localmente antes de publicar

Basta dar duplo clique no arquivo `index.html` — abre direto no navegador (Chrome, Edge, etc.), sem precisar de internet nem instalação.

## Processo para alterações no projeto

Toda mudança no site (`index.html`, `README.md` etc.) segue esta ordem, **sempre nessa sequência**:

1. **Registrar no `CHANGELOG.md`** — antes de subir qualquer alteração, adicione uma entrada no topo desse arquivo descrevendo o que mudou (o que foi Adicionado / Alterado / Removido / Corrigido). O `CHANGELOG.md` já tem um modelo pronto pra copiar.
2. **Abrir um Pull Request (PR)** em vez de subir direto na branch `main`. Passo a passo pelo site do GitHub:
   - Vá em **Add file → Upload files**.
   - Antes de arrastar os arquivos, troque a branch (o seletor que normalmente mostra `main`) por **"Create a new branch"**, dê um nome curto (ex.: `atualizacao-2026-08-13`).
   - Arraste os arquivos atualizados (incluindo o `CHANGELOG.md` com a entrada nova) e confirme o commit nessa branch nova.
   - O GitHub vai oferecer um botão **"Compare & pull request"** — clique nele, confira a descrição (pode citar a entrada do changelog) e clique em **"Create pull request"**.
   - Revise as mudanças na aba "Files changed" e, quando estiver tudo certo, clique em **"Merge pull request"** → **"Confirm merge"**.
3. Só depois do merge o GitHub Pages atualiza o site (~1 minuto).

Isso cria um pequeno "histórico revisável" de tudo que já foi feito, em vez de sobrescrever direto o arquivo principal.

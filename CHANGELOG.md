# Histórico de alterações — Itinerário de Publicações

Todas as mudanças relevantes no `index.html` (e nos demais arquivos do projeto) devem ser registradas aqui **antes** de abrir o Pull Request. Formato: mais recente no topo.

Ao abrir um PR, inclua no título ou na descrição a referência da entrada correspondente deste arquivo (ex.: "Ref: Não versionado — 2026-08").

---

## [Não versionado] — 2026-08-13 (tarde)
### Alterado
- Barras de progresso (Sentinela — entrega mensal / Apostila — entrega bimestral) trocadas de lista empilhada (uma barra por linha) para **grid compacto** de blocos lado a lado — reduz de ~18 linhas para 2–3 linhas de altura, mantendo a mesma informação.

## [Não versionado] — 2026-08-13
### Adicionado
- Coluna **Status** (🟡 Pendente / 🟢 Entregue) na aba Pedidos Especiais, calculada automaticamente a partir da Data de entrega.
- Nome do publicador **fixo** ao rolar a tabela horizontalmente (`position: sticky`).
### Alterado
- Cabeçalho (hero) mais compacto: menos padding, títulos e cards de estatística menores.
### Removido
- Tentativa de cabeçalho de tabela fixo verticalmente — descartada após teste real mostrar incompatibilidade com a rolagem horizontal por grupo (limitação de CSS, não de implementação).

## [Não versionado] — 2026-08 (mais cedo)
### Alterado
- **Sentinela / Sentinela Letra G.**: controle passou de bimestral para **mensal** (Jan–Dez).
- **Apostila**: mantido o controle **bimestral** (Jan-Fev, Mar-Abr...), agora em bloco separado na tabela.
- Barra de progresso duplicada: uma para entrega mensal (Sentinela), outra para bimestral (Apostila), calculadas apenas sobre quem recebe cada publicação.
### Adicionado
- Filtro por **Publicador** na barra de busca (além dos já existentes de Grupo e Tipo de publicação).
- Rolagem horizontal na tabela (ficou mais larga com as 12 colunas mensais).

## [Não versionado] — 2026-07 (final do mês)
### Adicionado
- Aba **"Pedidos Especiais"**, com tabela própria: Publicador, Tipo de publicação (combo: Índice das Publicações da Torre de Vigia / Examine as Escrituras Diariamente — 2027 / idem Letras Grandes), Data solicitação, Data entrega.
- Dashboard de métricas específico da aba Pedidos Especiais (total, por tipo, aguardando entrega).
- Menu compacto (☰) no canto superior esquerdo, reunindo Imprimir, Importar/Exportar dados, Adicionar publicador, Gerenciar acesso e Sair.
### Alterado
- Reordenação dos itens do menu e textos do cabeçalho.
- Divisores visuais entre blocos de colunas (Publicador | Tipo de publicação | Bimestre/Mês).

## [Não versionado] — 2026-07 (meio do mês)
### Adicionado
- **Login com e-mail e senha** (Firebase Authentication), com "Esqueci minha senha" e opção de mostrar/ocultar senha.
- Painel **"Gerenciar acesso"** dentro do próprio site, para criar login de novas pessoas sem precisar abrir o console do Firebase.
### Alterado
- Regras do Firestore atualizadas para exigir autenticação (`allow read, write: if request.auth != null`).

## [Não versionado] — 2026-07 (início)
### Adicionado
- Versão inicial do site (`index.html`), convertendo a planilha do Google em página interativa.
- Sincronização em tempo real via Firebase Firestore (todos os dispositivos logados veem as mesmas marcações).
- Estrutura de dados migrada das duas abas da planilha original (Sentinela e Apostila) para um único modelo por publicador.
- Checkboxes (carimbos) no lugar do "1" da planilha, agrupamento por grupo com expandir/recolher, painel de estatísticas, exportar/importar backup em JSON, impressão.

---

## Como registrar uma nova alteração
1. Antes de subir o arquivo atualizado, adicione uma entrada no topo deste arquivo (pode usar `[Não versionado] — AAAA-MM-DD`).
2. Liste em **Adicionado / Alterado / Removido / Corrigido** o que mudou, em linguagem simples.
3. Só então abra o Pull Request (veja o passo a passo no `README.md`).

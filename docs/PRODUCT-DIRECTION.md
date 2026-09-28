# ImpactTube — direção de produto e UX

## Decisão visual

A direção escolhida é **tema escuro premium**, com identidade **musical**, usando claymorphism refinado: superfícies macias, elevação baixa, controles táteis e sombras difusas, sem textura de argila ou aparência infantil. A paleta permanece tokenizada para permitir tema claro/adaptativo em uma fase posterior.

## 1. Diagnóstico resumido

O NewPipe entrega uma base madura de descoberta, reprodução, fila, downloads, histórico e playlists, mas expõe bastante complexidade técnica na navegação e nas telas de detalhe/configuração. O código mantém separação relevante entre `app`, `extractor`, `database`, `player` e `shared`, portanto a evolução deve ser incremental.

## 2. Problemas de usabilidade prioritários

- Hierarquia visual inconsistente entre descoberta, detalhe, player e downloads.
- Ações secundárias competem com reproduzir e baixar.
- Estados de download e erro exigem interpretação técnica.
- Biblioteca, histórico e playlists precisam de agrupamento mais óbvio.
- Mini player e fila devem ter acesso persistente e previsível.
- Acessibilidade precisa ser critério de cada componente, não um acabamento.

## 3. Navegação proposta

Barra inferior com **Início, Explorar, Pesquisar, Biblioteca e Downloads**. O mini player fica acima da barra quando ativo. Configurações, sobre e licenças continuam em um destino secundário; os créditos dos criadores do NewPipe permanecem visíveis no Sobre.

## 4. Fluxos principais

1. Descobrir → abrir detalhe → reproduzir/baixar → mini player.
2. Pesquisar → filtrar por tipo → ação rápida em resultado.
3. Reproduzir → abrir player → fila → salvar fila como playlist.
4. Downloads → filtrar estado → pausar/retomar/abrir/compartilhar.
5. Biblioteca → histórico, salvos, playlists, inscrições e downloads.

## 5. Design system

Tokens de superfície, texto, destaque, sucesso, alerta e erro; escala tipográfica acessível; espaçamento 4/8; raios 12/20/28dp; elevação 0–4; ícones Material; componentes com estados padrão, pressionado, selecionado, desabilitado, carregando, erro, concluído e foco. Sombras devem usar uma única direção de luz. A paleta final deve ser validada em contraste WCAG.

## 6. Telas

Início modular, Explorar, Pesquisa, Detalhe de mídia/canal/playlist, Player completo, Fila, Downloads, Biblioteca, configurações e Sobre/FAQ/licenças.

## 7–9. Componentes e estados

`MediaCard`, `MediaListItem`, `FilterChip`, `PrimaryAction`, `MiniPlayer`, `PlayerControls`, `DownloadRow`, `QueueSheet`, `EmptyState`, `ErrorState`, `Skeleton`, `Toast` e `BottomSheet`. Todo carregamento tem skeleton; erro informa causa e ação de recuperação; vazio explica o próximo passo.

## 10. Player

Controles principais grandes e acessíveis; progresso, velocidade, repetição, aleatório, fila, temporizador, qualidade, áudio/vídeo, legendas, tela cheia, minimizar e gesto de fechar. Reprodução em segundo plano e controles existentes não devem ser removidos.

## 11. Downloads

Abas ou filtros para ativos, concluídos, pausados e erro; cada item exibe progresso, velocidade, tamanho, formato, qualidade e resolução. Ações individuais e em lote devem diferenciar arquivo indisponível e armazenamento insuficiente.

## 12. Acessibilidade

Alvos mínimos de toque, descrições semânticas, conteúdo alternativo, foco visível, ordem lógica, contraste, fonte ampliada, não depender apenas de cor, redução de movimento/efeitos 3D e suporte a retrato, paisagem e telas compactas.

## 13. Implementação gradual

Preservar extractor, player, downloads, banco e contratos existentes. Primeiro criar tokens e componentes compartilhados; depois shell de navegação e mini player; então telas de descoberta/pesquisa; por fim detalhe, player, downloads e biblioteca. Evitar dependências novas sem justificativa e medir desempenho em aparelhos de baixo custo.

## 14. Fases

- **F0:** build reproduzível, identidade, créditos e CI.
- **F1:** tokens, acessibilidade base, navegação e componentes.
- **F2:** Início, Explorar, Pesquisa e detalhe.
- **F3:** mini player, player completo e fila.
- **F4:** downloads e biblioteca.
- **F5:** temas adaptativos, refinamento, testes e performance.

## 15. Critérios de aceitação

APK Debug e Release unsigned publicados como artefatos; funcionalidades atuais preservadas; instalação verificada; CI executa lint/test/build; créditos NewPipe no Sobre; ações críticas alcançáveis em até três toques; estados de rede, vazio, erro e download cobertos; contraste e toque auditados.

## 16. Código

Não foi incluído código de redesign prematuro. A próxima implementação deve começar pelos tokens/componentes após validar os fluxos com usuários e manter a lógica de negócio intacta.

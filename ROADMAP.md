# Kavro — Roadmap técnico

O roadmap registra **prioridades e critérios de validação**, sem prometer datas ou anunciar funcionalidades como prontas. O projeto está em fase experimental.

**Legenda:**
- **Em desenvolvimento:** trabalho ativo ou protótipo em evolução; não implica validação integral.
- **Pesquisa:** arquitetura e experimentos ainda sem escopo final consolidado.
- **Planejado:** objetivo definido, implementação ainda não verificada.

> O repositório público contém atualmente documentação introdutória. Builds e fontes completos não estão publicados aqui; os itens abaixo descrevem objetivos e pesquisa, não recursos disponíveis para instalação.

## P0 — Semântica, correção e confiabilidade

**Situação: Em desenvolvimento · Prioridade máxima**

- [ ] Definir regras formais para tipos, inferência, mutabilidade, parâmetros, retornos, coerções e erros.
- [ ] Eliminar inconsistências entre checagem estática e execução, com casos de regressão para retornos de tipo desconhecido.
- [ ] Estabelecer os comportamentos compartilhados entre a VM de testes e o backend nativo: inteiros, overflow, booleanos e erros.
- [ ] Automatizar testes positivos, negativos e diferenciais; ampliar fuzzing quando houver infraestrutura adequada.
- [ ] Documentar limites de segurança da VM, do compilador e dos executáveis gerados.

**Critério de conclusão:** semântica documentada, suíte de regressão reproduzível e ausência de divergências conhecidas nos recursos declarados como suportados.

## P1 — Backend nativo e desempenho

**Situação: Pesquisa e desenvolvimento experimental**

- [ ] Validar executáveis x86-64 no Windows real, incluindo convenções de chamada, saída, falhas e segurança do binário.
- [ ] Evoluir a representação intermediária para etapas de compilação efetivas, com lowering e alocação de registradores.
- [ ] Expandir o conjunto de operações e estruturas suportadas pelo backend nativo.
- [ ] Avaliar uma ferramenta de compilação autocontida e a redução de dependências de runtime durante a compilação.
- [ ] Executar benchmarks com programas equivalentes, ferramentas identificadas e metodologia reproduzível.

**Critério de conclusão:** execução nativa demonstrada e documentada, testes de ABI e medições reproduzíveis sem extrapolações sobre desempenho.

## P2 — Kavro Studio

**Situação: Protótipos em desenvolvimento**

- [ ] Validar abertura, edição, salvamento, abas, seleção, Unicode e undo/redo no Windows real.
- [ ] Melhorar navegação, Explorer, diagnósticos e suporte a sugestões/autocompletar.
- [ ] Verificar comportamento do editor com documentos grandes, redimensionamento e diferentes configurações de tela.
- [ ] Implementar testes de integração e cenários fim a fim para as funções principais da IDE.
- [ ] Refinar acessibilidade, organização visual e consistência de animações sem comprometer fluidez.

**Critério de conclusão:** fluxos de edição e compilação testados em ambiente Windows, com falhas conhecidas registradas e testes reexecutáveis.

## P3 — Programação de sistemas

**Situação: Planejado**

- [ ] Definir modelo de memória, ponteiros, tempo de vida e regras de segurança.
- [ ] Projetar interoperabilidade com bibliotecas nativas e FFI com contratos bem definidos.
- [ ] Avaliar Assembly inline, depuração e ferramentas de inspeção com regras explícitas.
- [ ] Testar casos adversariais e limites de segurança de recursos de baixo nível.

**Critério de conclusão:** especificação pública dos comportamentos suportados e cobertura por testes de integração representativos.

## P4 — Distribuição, testes e ecossistema

**Situação: Em evolução**

- [ ] Automatizar builds reproduzíveis e verificações de integridade.
- [ ] Padronizar cada pacote de avaliação com pasta `TESTE/`, instruções, amostras, roteiro e relatório de feedback sem dados pessoais obrigatórios.
- [ ] Disponibilizar documentação e exemplos vinculados à versão correspondente.
- [ ] Definir política de versões, compatibilidade, contribuições, licença e publicações.
- [ ] Estabelecer critérios de release e validação em CI e no ambiente-alvo.

**Critério de conclusão:** distribuição auditável com documentação coerente, verificações automatizadas e critérios públicos de compatibilidade.

## Princípios de atualização

1. Um protótipo local não é uma funcionalidade estável nem uma release pública.
2. Um item só deve ser marcado como concluído com evidências de teste adequadas ao que ele promete.
3. Resultados de Linux, análise estática e cross-compilation não substituem execução real no Windows.
4. Mudanças de sintaxe e arquitetura devem considerar compatibilidade, ergonomia, custo e alternativas.
5. Documentação pública deve conter apenas informações técnicas necessárias, sem dados pessoais, documentos privados, segredos ou material confidencial.

[Voltar ao README](README.md)

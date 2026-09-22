# Governança de Repositórios — Tecenda Tecnologia

Este documento estabelece o padrão oficial para criação, organização, segurança e manutenção dos repositórios da Tecenda Tecnologia.

## 1. Política de visibilidade

### Repositórios públicos

Um repositório pode ser público quando contiver somente:

- Perfil e documentação institucional.
- Projetos demonstrativos sem dados reais de clientes.
- Templates genéricos destinados à divulgação ou reutilização.
- Bibliotecas e ferramentas cuja publicação tenha sido aprovada.
- Documentação criada especificamente para acesso público.

### Repositórios privados

Devem permanecer privados:

- Sites, sistemas, automações e integrações de clientes.
- Código de produção que não tenha publicação expressamente aprovada.
- Propostas, contratos, documentos comerciais e informações financeiras.
- Infraestrutura, configurações internas, backups, logs e relatórios.
- Dados pessoais, dados de clientes ou qualquer conteúdo sujeito à LGPD.
- Projetos em desenvolvimento que ainda não passaram por revisão para publicação.

**Regra padrão:** todo novo repositório nasce privado. A publicação é uma exceção e exige revisão prévia.

## 2. Gestão de secrets

Nunca devem ser gravados em arquivos, commits, issues, pull requests ou logs:

- Senhas e códigos de autenticação.
- Tokens de acesso.
- Chaves de API.
- Chaves privadas e certificados.
- Strings de conexão de bancos de dados.
- Credenciais de e-mail, hospedagem, CRM ou serviços externos.
- Dados pessoais ou informações confidenciais de clientes.

### Armazenamento aprovado

- **GitHub Actions Secrets — Repository:** secrets usados por um único projeto.
- **GitHub Environments:** secrets separados entre `staging` e `production`.
- **Organization Secrets:** somente quando o mesmo secret precisar ser compartilhado por vários repositórios previamente autorizados.
- **Hostinger ou plataforma de produção:** variáveis próprias do ambiente, quando aplicável.

### Regras obrigatórias

1. Incluir `.env` e variações locais no `.gitignore`.
2. Manter somente um `.env.example` com nomes e valores fictícios.
3. Aplicar menor privilégio e limitar cada secret ao serviço necessário.
4. Rotacionar imediatamente secrets expostos, suspeitos ou compartilhados incorretamente.
5. Revisar secrets e acessos pelo menos trimestralmente.
6. Revogar acessos de usuários, integrações e fornecedores que não sejam mais necessários.
7. Exigir MFA para contas administrativas.

### Resposta a exposição

Quando um secret for exposto:

1. Revogar ou rotacionar imediatamente.
2. Verificar logs e atividades relacionadas.
3. Remover o valor do histórico Git quando necessário.
4. Registrar o incidente e a ação corretiva.
5. Validar novamente o serviço antes de encerrar o incidente.

## 3. Padrão de nomes

Usar letras minúsculas, números e hífens no formato `kebab-case`.

Prefixos oficiais:

- `site-` — sites institucionais e landing pages.
- `sistema-` — sistemas e aplicações personalizadas.
- `automacao-` — fluxos e rotinas automatizadas.
- `integracao-` — conectores entre plataformas e APIs.
- `template-` — modelos reutilizáveis e demonstrações.
- `infra-` — infraestrutura, deploy e observabilidade.
- `docs-` — documentação e padrões internos.

Exemplos:

- `site-modelo-clinica`
- `sistema-gestao-atendimento`
- `automacao-follow-up-crm`
- `integracao-zoho-formulario`
- `template-site-cartorio`

Evitar nomes genéricos como `teste`, `novo`, `projeto-final` ou `repo-1`.

## 4. Estrutura mínima

Cada repositório deve possuir, quando aplicável:

- `README.md` com objetivo, instalação, execução e responsável.
- `.gitignore` adequado à tecnologia utilizada.
- `.env.example` sem valores reais.
- `LICENSE` quando o projeto público permitir reutilização.
- `docs/` para documentação complementar.
- `SECURITY.md` em projetos públicos ou críticos.
- Descrição e tópicos preenchidos no GitHub.

## 5. Branches e commits

### Branches

- `main` — versão estável.
- `feature/<nome-curto>` — nova funcionalidade.
- `fix/<nome-curto>` — correção.
- `chore/<nome-curto>` — manutenção técnica.
- `docs/<nome-curto>` — documentação.

### Commits

Usar mensagens claras e objetivas:

- `feat:` nova funcionalidade.
- `fix:` correção.
- `docs:` documentação.
- `chore:` manutenção.
- `refactor:` refatoração.
- `test:` testes.
- `security:` melhoria de segurança.

## 6. Acessos e permissões

- Administrador somente para proprietários responsáveis.
- Colaboradores recebem apenas o nível de acesso necessário.
- Repositórios de clientes não devem ser compartilhados com terceiros sem autorização.
- Novos usuários devem usar MFA.
- Acessos devem ser revisados trimestralmente.
- Usuários, aplicativos e chaves inativos devem ser removidos.

## 7. Ciclo de vida

Classificar os projetos como:

- **Ativo:** desenvolvimento ou operação em andamento.
- **Manutenção:** estável, recebendo correções e atualizações.
- **Arquivado:** encerrado, substituído ou sem manutenção prevista.

Antes de arquivar:

1. Atualizar o README.
2. Confirmar backup e documentação.
3. Revogar secrets e acessos desnecessários.
4. Registrar o motivo do encerramento.

## 8. Checklist antes de tornar público

- [ ] Nenhum secret ou credencial presente.
- [ ] Nenhum dado pessoal ou de cliente.
- [ ] Histórico Git revisado.
- [ ] README atualizado.
- [ ] Licença definida quando aplicável.
- [ ] Configurações e domínios sensíveis removidos.
- [ ] Logs, backups e arquivos temporários removidos.
- [ ] Publicação aprovada pelo responsável da Tecenda.

---

**Responsável:** Tecenda Tecnologia  
**Revisão:** trimestral ou sempre que houver mudança relevante de ferramentas, equipe ou requisitos de segurança.

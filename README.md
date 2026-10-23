# MEGAHUNT — Controle de Torres

Site para registrar a captura de torres no MEGAMU por mapa, servidor, jogador e horário. Mostra os próximos horários, contadores regressivos e filtros. Layout responsivo, todo em português.

## 1. Publicar grátis no GitHub Pages

1. Faça login no github.com e crie um repositório chamado `megahunt-torres` (público para GitHub Pages no plano grátis).
2. Faça upload do arquivo `index.html` (na raiz do repositório). Pode também enviar este README.
3. Em **Settings > Pages > Build and deployment**, escolha **Deploy from a branch**, branch **main**, pasta **/(root)** e salve.
4. A URL terá o formato `https://SEU-USUARIO.github.io/megahunt-torres/`.

**Importante:** antes de configurar o Firebase, a página funciona **apenas em modo local**. Cada usuário verá registros próprios, que não são compartilhados com a guild.

## 2. Sincronizar registros em tempo real — Firebase

1. Acesse https://console.firebase.google.com/ e crie um projeto.
2. Em **Build > Firestore Database**, crie o banco no modo produção (escolha uma região). Não deixe as regras padrão bloqueando o acesso; instale as regras do passo 5.
3. Em **Build > Authentication > Sign-in method**, ative **Anonymous**. O usuário não precisará fazer login para registrar torres.
4. No painel do projeto, clique em **Project settings > Your apps > Web (ícone </>)** e registre um app Web. Copie os dados de `firebaseConfig` para o objeto com o mesmo nome que fica perto do final do `index.html`. Os campos normalmente incluem `apiKey`, `authDomain`, `projectId`, `storageBucket`, `messagingSenderId` e `appId`. Você pode adicionar os campos extras ao objeto.
5. Em **Firestore Database > Rules**, substitua as regras pelas instruções presentes no arquivo `firestore.rules` e clique em **Publish**.
6. Envie o `index.html` editado para o seu repositório e abra o link do Pages. O cabeçalho deve mostrar `Online • sincronizado com a guild`.
7. Envie o link a seus colegas. Todos verão as alterações em tempo real.

**Segurança:** esta versão é indicada para uma guild confiável. Qualquer visitante do site pode entrar anonimamente e modificar/excluir registros e configurações. O link não é senha. Para controle estrito por membro, é necessário criar login e regras específicas (por exemplo, uma lista de UIDs autorizados). As regras oferecidas limitam as operações aos dois grupos de documentos usados no app, mas **não** diferenciam membros da guild de visitantes.

**Custo:** GitHub Pages costuma atender esse site gratuitamente. Firebase possui uma camada gratuita com limites de leitura, gravação e armazenamento; monitore o painel de consumo se houver muitos usuários.

## 3. Ajustar mapas e tempo de espera

Abra **Parâmetros do evento** dentro do site:

- Um mapa por linha: `Nome|minutos`, como `Nix|90`.
- Informe servidores separados por vírgula: `1,2,3,4,5`.
- Clique em **Salvar parâmetros**. Com o Firebase ativo, os parâmetros serão compartilhados.

**ATENÇÃO:** os mapas iniciais e o prazo de **60 minutos são valores de demonstração**, NÃO são valores confirmados do evento MEGAMU. Insira os tempos oficiais do evento antes do uso real.

### Como funciona o cálculo

Horário da próxima liberação = horário registrado + tempo de espera configurado para o mapa. A lista ordena os registros pelo horário previsto. Após passar do horário, o item vira `Liberada`; o registro não desaparece automaticamente. Você pode excluir o registro anterior depois de tomar a próxima torre.

Os registros usam timestamp em UTC por baixo e mostram horário no fuso local de cada visitante. A pessoa que registra deve usar o horário do próprio dispositivo.

## Arquivos

- `index.html`: página completa (HTML, CSS e JavaScript)
- `firestore.rules`: regras de acesso do banco para o modo aberto
- `README.md`: este guia

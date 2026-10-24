# Farm Tower — Acesso somente por senha

## Como funciona
A tela pública pede **apenas uma senha**. Por trás, o sistema utiliza o email fixo de uma única conta do Firebase Authentication e a senha digitada. O visitante **não precisa digitar nem conhecer o email**. O email configurado no HTML é público, mas **a senha nunca deve aparecer no código**.

## 1. Criar conta da guild
Firebase Console → FarmTower → Authentication → Método de login → **Email/Senha** → Ativar e Salvar. Depois, em **Usuários**, crie **uma única conta** para a guild, com um email que você controle e senha forte. Copie o UID da conta. Não ative login anônimo nem criação pública de contas.

## 2. Configurar o HTML
Abra `index.html` no editor e localize:

`const guildLoginEmail = 'COLOQUE_EMAIL_DA_CONTA_AQUI';`

Substitua somente o texto entre aspas pelo email da conta criada no Firebase. Isso não faz o email aparecer na tela de login, apenas no código-fonte público.

A configuração `firebaseConfig` do projeto `farmtower-93c81` e o UID autorizado já foram preenchidos neste pacote. Não precisa ativar Firebase Hosting: o site já usa GitHub Pages. Os valores de `firebaseConfig` não são segredos. **Nunca escreva a senha no HTML**.

Verifique em Authentication → Configurações → Domínios autorizados se `rkiffer.github.io` aparece; se necessário, adicione-o.

## 3. Proteger o Firestore
O arquivo `firestore.rules` já está preenchido com o UID autorizado `FT1jZTxqXrZgjq5zrfnSXUner682`. Firebase Console → Firestore Database → Regras → copie o conteúdo corrigido e clique **Publicar**. Enviar apenas `firestore.rules` ao GitHub não publica as regras. Mantenha regras restritivas até finalizar.

## 4. Publicar
Substitua somente o `index.html` no repositório público `rkiffer/FarmTower` e confirme **Commit changes**. Abra https://rkiffer.github.io/FarmTower/ e teste com a senha criada. O login permanece ativo até clicar em **Sair**.

## Segurança
- GitHub Pages é público; a proteção **real** dos registros é Firebase Authentication + Firestore Rules.
- Todos que souberem a senha entram com a mesma identidade e podem modificar/excluir registros. Se alguém deixar a guild, altere a senha no Firebase Authentication.
- O Firestore inicia protegido; nunca publique regras `allow read, write: if true`.
- O horário da torre é capturado no instante de clicar em Registrar torre, conforme relógio do dispositivo.

## Estado deste pacote
Apenas o email da conta compartilhada ainda precisa ser preenchido no `index.html`; não coloque a senha no arquivo. As regras precisam ser publicadas manualmente no console do Firebase e o HTML enviado ao GitHub.

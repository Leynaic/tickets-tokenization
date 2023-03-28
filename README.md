# tickets-tokenization

Application de tokenization de billets de concert sur la blockchain Tezos.

# Exigences

- Taqueria `v28.0 minimum` (https://taqueria.io/)
- Node.js `v16.16 minimum` (https://nodejs.org/)
- Esy `v0.6 minimum` (https://esy.sh/)

# Installation

```bash
taq init
npm install
taq install @taqueria/plugin-ligo
```

# Compilation des contrats

```bash
taq compile ticket_nft.jsligo
taq compile concert.jsligo
```

# Deploiement du contrat usine

```bash
taq deploy concert.tz -e "testing"
```

# Documentation des contrats

## Contrat usine : Concert

Ce contrat permet de déployer les contrats permettant de gérer les NFTs pour un concert. Ce contrat possède deux entrypoints.

### `createConcert`
#### Paramètres

- `capacity` `nat` : La capacité d'un concert soit le nombre maximum de NFT autorisé.
- `ticket_price` `mutez` : Le prix pour un NFT, attention 1 mutez vaut 0.000001 tez.

#### Action

Déploie un nouveau contrat sur la blockchain Tezos.

#### Remarque

- Vous devez ajouter une certaine somme en Tezos lors de la transaction pour pouvoir déployer le contrat.

### `nothing`

Ne fait rien.

## Contrat enfant : Ticket NFT

Ce contrat est unique pour un concert. Il permet la vente des tickets, l'annulation d'un concert, le burn d'un ticket, le remboursement des tickets, et la validation (withdraw) d'un concert. Il possède dix entrypoints

### add_administrator

#### Paramètres

- `address` `address` : Addresse de la personne à ajouter en tant qu'administration

#### Action

Ajout un administrateur à la liste des administrateurs.

#### Remarque

- L'adresse appelant ce endpoint doit être administrateur.

### burn_ticket

#### Paramètres

- `token_id` `nat` : Token du jeton (NFT) à brûler.

#### Action

Transfère la propriété du NFT à l'adresse de BURN de la blockchain tezos.

#### Remarque

- Le NFT doit exister.
- Vous devez détenir le NFT sur lequel l'action est effectué.

### buy_ticket

#### Paramètres

- `token_id` `nat` : Token du jeton (NFT) à acheter.

#### Action

Transfère la propriété du NFT à l'adresse de l'envoyeur.

#### Remarque

- Le NFT doit exister.
- Le NFT ne doit pas être déjà acheté.
- Vous payez la somme en MUTEZ du prix du ticket.

### pre_mint

#### Paramètres

- `name` `bytes` : Nom du concert, sera le nom du NFT.
- `description` `bytes` : Descrition du concert, sera la description du NFT.

#### Action

MINT le nombre de NFT équivalent à la capacité du concert.

#### Remarque

- Cette entrypoint doit être appelé en premier (avant `mint`)
- Il est appelable qu'une seul fois.
- Vous devez être administrateur.

### refund

#### Paramètres

Aucun.

#### Action

Rembourse tout les propriétaires de ticket, qui n'ont pas été BURN.

#### Remarque

- Bloque les achats.
- Il est appelable qu'une seul fois.
- Vous devez être administrateur.

### withdraw



#### Paramètres

Aucun.

#### Action

Le totalité de la somme récolté lors des achats de ticket (balance du contrat) est envoyé au porte-monnaie du créateur.

#### Remarque

- Bloque les achats.
- Il est appelable qu'une seul fois.
- Vous devez être le créateur du concert.

### mint

- Présent pour la norme FA2.
- Pas utile.

### transfer

- Présent pour la norme FA2.
- Pas utile.

### update_operators

- Présent pour la norme FA2.
- Pas utile.

### balance_of

- Présent pour la norme FA2.
- Pas utile.

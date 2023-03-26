# tickets-tokenization

Application de tokenization de billets de concert sur la blockchain Tezos.

## Exigences

- Taqueria `v28.0 minimum` (https://taqueria.io/)
- Node.js `v16.16 minimum` (https://nodejs.org/)
- Esy `v0.6 minimum` (https://esy.sh/)

## Installation

```bash
taq init
npm install
taq install @taqueria/plugin-ligo
```

## Compilation des contrats

```bash
taq compile ticket_nft.jsligo
taq compile concert.jsligo
```

## Deploiement du contrat usine

```bash
taq deploy concert.tz -e "testing"
```

## Documentation des contrats

### Concert

// TODO

### Ticket NFT

// TODO

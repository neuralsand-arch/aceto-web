# aceto-web

Pagine pubbliche di **Aceto**, servite da GitHub Pages **in attesa del sito ufficiale**
(che sarà in Next.js, vedi `docs/PIANO-SVILUPPO-SAAS.md` §2 nel repo principale).

| Pagina | A cosa serve |
|---|---|
| `reset-password/` | dove atterra il link di reimpostazione della password inviato per mail |
| `account-deletion/` | l'URL pubblico di cancellazione dell'account, che Google Play pretende |

## Perché il reset è una pagina web

Il link della mail si apre nel **browser**, non nell'app: con il flusso PKCE il verificatore
resterebbe nel portachiavi dell'app e il giro morirebbe lì. Perciò l'app chiede il reset con
`flowType: 'implicit'` e il token arriva nel frammento dell'URL, che questa pagina usa per chiamare
`PUT /auth/v1/user`.

La **chiave pubblicabile** di Supabase è scritta nella pagina: è fatta per stare in pagine pubbliche,
la sicurezza la fanno RLS e le policy. La chiave **segreta** non compare qui e non deve comparire mai.

## Da fare prima della pubblicazione sugli store

- [ ] Sostituire il progetto Supabase di sviluppo (`aceto-dev`) con quello di produzione.
- [ ] Aggiungere un indirizzo di contatto per chi non ha più accesso all'app: Google Play chiede che la
      cancellazione si possa chiedere anche senza installarla.
- [ ] Verificare che le due pagine siano elencate in *Authentication → URL Configuration* su Supabase.

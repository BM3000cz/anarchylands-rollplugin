# Známé omezení — RollPlugin 1.2.4

## Předměty z duelu po náhlém pádu serveru
Po přijetí duelu plugin odebere oba vklady a drží je v paměti do ukončení duelu.
Náhlý pád serveru/JVM, nucené ukončení procesu nebo výpadek hostitele v této době
může způsobit ztrátu obou vkladů.

Pokud server spadne během doručování předmětů nebo ukládání hráčských dat,
mohou po restartu předměty také chybět nebo být duplicitní.

Při běžném vypnutí/restartu se plugin pokusí aktivní vklady vrátit. Vratky, které
nelze okamžitě doručit, ukládá do `pending-duel-refunds.yml` a zkouší je doručit při
připojení hráče s volným místem v inventáři. Tento soubor neobsahuje všechny aktivní
vklady. Restart ani `/rollreload` nedokáže obnovit neuložený vklad.

Nepřijaté výzvy předměty zatím neodebírají.

# bpmorc Project

Questo progetto usa quarkus e fornisce le API per la gestione del dossier
e i suoi flussi integrando i sottoprocessi necessari.

Dividiamo il problema in unità più piccole:

dossiermanager: Gestisce la validazione dell'input prima di avviare i sottoprocessi e definisce la risposta ai client dopo aver ricevuto l'esito dai sottoprocessi.
createdossier: Gestisce l'intero processo di creazione del dossier con l'eventuale integrazione di servizi esterni REST.

Il processo include un'attività di script per la scrittura di informazioni di debug e un'attività di chiamata per richiamare un processo secondario,
utilizzando un oggetto dati FEUDossier estensione del common-data-model:dossier

Sarà presente un processo di orchestrazione per consentire ai clienti di creare casi di supporto/attivazione
che verrà assegnato agli ingegneri in base alla famiglia di prodotti e al nome utilizzando una tabella di decisione DMN.
Se non è possibile un'assegnazione automatica, verrà creata un attività di assegnazione manuale.

Una volta assegnato, il caso di supporto verrà impostato sul significato di stato `WAITING_FOR_OWNER`
che l'ingegnere deve lavorare sul caso e fornire una soluzione o aggiungere a
commento chiedendo maggiori informazioni.

In qualsiasi momento i clienti o gli ingegneri possono aggiungere commenti fino a quando non si risolve il caso
`CHIUSO`.

Il caso può essere impostato come "RISOLTO" da un tecnico o da un cliente. Una volta
ciò accade un compito Questionario sarà messo a disposizione del cliente
può fornire un feedback sulla risoluzione del caso.

Dopo l'invio del Questionario, il caso sarà "CHIUSO" e il processo
terminerà.

Un servizio di regole per convalidare il fatto "LoanApplication". Le regole sono scritte come una tabella decisionale.

Gli endpoint REST sono generati dalle regole di query. È possibile inserire i fatti "LoanApplication" e interrogare un risultato tramite gli endpoint REST. Le risorse delle regole vengono assemblate come RuleUnit.


Sulla base di questi processi e delle configurazioni dell'applicazione, questo servizio di esempio espone le operazioni REST per
creare nuovi ordini, elencare ed eliminare ordini attivi.



## Running the application in dev mode

You can run your application in dev mode that enables live coding using:
```shell script
./mvnw compile quarkus:dev
```

> **_NOTE:_**  Quarkus now ships with a Dev UI, which is available in dev mode only at http://localhost:8080/q/dev/.

## BODY for testing the application

{
    "dossier": {
		"number": 99999555
	}
}


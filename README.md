<h1 align="center">Nodeliad 🤖</h1>
<img src="https://img.shields.io/badge/docker-ready-brightgreen.svg"/>

Nodeliad è un bot Telegram realizzato in Node.js per monitorare i consumi della propria linea Iliad.

<p align="center">
  <img src="https://i.imgur.com/Djysc5G.png" width="30%">
</p>

Il progetto è nato per via della mancanza di un'app ufficiale per iOS che costringe gli utenti a controllare i consumi dal PC o attraverso il sito sotto rete Iliad per evitare di dover effettuare il login.

### Features
* 💰 controllo del credito residuo
* 🇮🇹 controllo dei consumi effettuati in Italia
* 🌎 controllo dei consumi effettuati all'estero
* 💶 controllo costi extra in Italia
* 💵 controllo consumi e costi extra all'estero

### Installazione
1. Clonare il repository con ```git clone https://github.com/Nicuz/Nodeliad.git``` oppure cliccando sul bottone in alto a destra ```Clone or Download```
2. Entrare nella directory di Nodeliad
3. Installare le dipendenze con ```npm install```
4. Rinominare il file ```config.json.template``` in ```config.json```e modificarlo inserendo i propri dati di accesso al sito di Iliad, il token del vostro bot fornito da [BotFather](https://telegram.me/BotFather) e il vostro nickname di Telegram senza la @ iniziale. Il nickname viene utilizzato per fare un controllo sull'utente che invia un comando, il bot fornirà i dettagli sulla linea solo all'utente col nickname specificato.
5. Avviare il bot con ```node bot.js```

### PM2
Se volete gestire il bot tramite [PM2](https://github.com/Unitech/pm2) dopo aver creato il file `config.json` eseguite il comando ```pm2 start pm2-ecosystem.config.js```

### Docker container
Dopo aver clonato il repository e modificato il `config.js` effettuare una docker build

```docker build . -t nodeliad```

Terminata la build avviate il bot

```docker run -it --name=nodeliad-bot nodeliad```


### Avvio automatico con systemd
1. Lanciare il comando ```whereis node``` per trovare il binario di node, nel mio caso ```/usr/local/bin/node```
2. ```sudo nano /etc/systemd/system/nodeliad.service``` e incollare il testo seguente avendo l'accortezza di modificare il path del binario di node e quello dello del bot.

```[Unit]
Description=Nodeliad Bot
After=network.target

[Service]
Type=idle
ExecStart=/path/binario/node /path/nodeliad/bot.js

[Install]
WantedBy=multi-user.target
```

3. ```sudo systemctl daemon-reload```
4. ```sudo systemctl enable nodeliad```
5. ```sudo systemctl start nodeliad```

Se tutto è stato configurato correttamente, lanciando il comando ```sudo systemctl status nodeliad``` vedrete che il servizio è in esecuzione 💪

### Changelog

#### ```[0.0.2] - 11/06/2018```
##### Aggiunto
* [cheerio](https://github.com/cheeriojs/cheerio)
* comandi ```/costiextra``` e ```/costiextraestero```

##### Rimosso
* striptags

##### Cambiato
* Ricerca dei tag tramite cheerio, regex rimosse
* Salvataggio dati in un oggetto e non più in array

#### ```[0.0.1] - 09/06/2018```
* Release iniziale

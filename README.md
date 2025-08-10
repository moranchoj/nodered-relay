# Node-RED Relay Control per Venus OS amb victron-input-relay

Aquest projecte mostra com controlar el RELAY1 de Venus OS utilitzant Node-RED i el node oficial **victron-input-relay** de Victron Energy. Aquesta solució proporciona una integració nativa i robusta amb el sistema Venus OS.

## Hardware

- Raspberry Pi amb Venus OS (Victron Energy)
- RELAY1 integrat del sistema Venus OS
- Connexió D-Bus per control del sistema

## Funcionament

La nova integració utilitza el node oficial **victron-input-relay** que es comunica directament amb el sistema D-Bus de Venus OS. Això proporciona:

- **Integració nativa**: Utilitza l'API oficial de Venus OS
- **Fiabilitat**: Control directe a través del sistema D-Bus 
- **Seguretat**: Respecta les polítiques de seguretat de Venus OS
- **Mantenibilitat**: Compatible amb futures actualitzacions del sistema

## Requisits previs

1. **Venus OS v2.80 o superior** amb Node-RED habilitat
2. **Node-RED Dashboard** instal·lat
3. **Victron Node-RED nodes** instal·lats (inclou victron-input-relay)

## Instal·lació

### 1. Instal·lació dels nodes Victron

Accedeix a la palette de Node-RED i instal·la:
```
node-red-contrib-victron
```

### 2. Importació del flow

1. **Descarrega** el fitxer `flow.json` d'aquest repositori
2. **Obre Node-RED** al teu sistema Venus OS: `http://<ip-venus>:1880`
3. **Importa el flow**: `Menú > Importa > Selecciona fitxer > flow.json`
4. **Deploy** el flow

### 3. Accés al dashboard

**Accedeix al dashboard**: `http://<ip-venus>:1880/ui`

## Detalls tècnics del nou flow

### Arquitectura
- **UI Switch**: Interfície d'usuari per activar/desactivar el relé
- **victron-input-relay**: Node oficial que es connecta al D-Bus de Venus OS
- **D-Bus path**: `/Relay/0/State` al servei `com.victronenergy.system`

### Avantatges de la nova solució

| Aspecte | Solució anterior (rpigpiosetup) | Nova solució (victron-input-relay) |
|---------|--------------------------------|-----------------------------------|
| **Integració** | Script extern | API nativa de Venus OS |
| **Fiabilitat** | Depèn de scripts de tercers | Sistema oficial de Victron |
| **Manteniment** | Pot trencar-se amb actualitzacions | Compatible amb actualitzacions |
| **Seguretat** | Execució de scripts externs | API segura del sistema |
| **Rendiment** | Sobrecàrrega d'exec | Comunicació directa D-Bus |

## Per què usar victron-input-relay?

### 1. **Integració oficial**
El node `victron-input-relay` forma part de l'ecosistema oficial de Victron Energy i està dissenyat específicament per Venus OS.

### 2. **Comunicació D-Bus nativa**
Utilitza el sistema D-Bus de Venus OS, la forma recomanada per interactuar amb els components del sistema.

### 3. **Millor rendiment**
Eliminiem la sobrecàrrega d'executar scripts externs, obtenint un control més directe i eficient.

### 4. **Compatibilitat futura**
Al ser una solució oficial, es mantindrà compatible amb futures versions de Venus OS.

### 5. **Seguretat millorada**
No requereix l'execució de scripts externs ni permisos especials, respectant les polítiques de seguretat del sistema.

## Configuració avançada

### Personalització del D-Bus path
Si necessites controlar altres relés o personalitzar la configuració:

```javascript
// Per RELAY2:
/Relay/1/State

// Per obtenir l'estat actual:
/Relay/0/State (lectura)
```

### Monitorització d'estat
Pots afegir nodes de lectura per monitoritzar l'estat actual del relé en temps real.

## Troubleshooting

### El relé no respon
1. **Verifica** que el node `victron-input-relay` està correctament instal·lat
2. **Comprova** la connexió D-Bus: `dbus -system`
3. **Revisa** els logs de Node-RED per errors de connexió

### Node victron-input-relay no disponible
1. **Instal·la** el paquet: `node-red-contrib-victron`
2. **Reinicia** Node-RED després de la instal·lació
3. **Verifica** la versió de Venus OS (mínim v2.80)

### Errors de permisos D-Bus
1. **Comprova** que Node-RED s'executa amb els permisos adequats
2. **Verifica** la configuració del servei Node-RED a Venus OS

## Migració des de versions anteriors

Si tens la versió anterior amb `rpigpiosetup`:

1. **Fes backup** del flow actual
2. **Elimina** els nodes antics (`exec`, `function`)
3. **Importa** el nou `flow.json`
4. **Configura** el node `victron-input-relay`
5. **Testa** la funcionalitat

## Contribucions

Aquest projecte està obert a millores i suggeriments. Si trobes problemes o tens idees per millorar la integració:

1. **Obre una issue** descrivint el problema o suggeriment
2. **Proposa canvis** via pull request
3. **Comparteix** la teva experiència amb altres usuaris

---

**Desenvolupat per la comunitat Venus OS amb el suport dels nodes oficials de Victron Energy**
---
author:
- Nicolas Vadkerti Quentin Risdorfer
title: MONITOR YOUR INFRA
---

<https://github.com/SlaynPool/CR_MONITOR_YOUR_INFRA>

Utilisation de SNMP comme vecteur de monitoring
===============================================

Installez le client SNMP sous Linux
-----------------------------------

-   ``` {#commande/1.txt .default caption="Installation d'un Client" label="commande/1.txt" style="Style1"}
    apt-get update
    apt-get install snmp snmp-mibs-downloader
    #Remplacez la ligne dans /etc/snmp/snmp.conf par
    mibs +ALL
    # Remplacer la mib qui genere une erreur ( dangereux ne pas faire en prod) :
    wget http://pastebin.com/raw.php?i=p3QyuXzZ -O /usr/share/snmp/mibs/ietf/SNMPv2-PDU
    ```

<!-- -->

-   ``` {#commande/2.txt .default caption="Test d'interogation" label="commande/2.txt" style="Style1"}
    # Pour recuperer Les OID de registry.iutbeziers.fr
    snmpwalk  -v  2c -c publicbeziers registry.iutbeziers.fr 
    SNMPv2-MIB::sysDescr.0 = STRING: Linux registry 4.9.0-8-amd64 #1 SMP Debian 4.9.130-2 (2018-10-27) x86_64
    SNMPv2-MIB::sysObjectID.0 = OID: NET-SNMP-MIB::netSnmpAgentOIDs.10
    DISMAN-EVENT-MIB::sysUpTimeInstance = Timeticks: (1320059745) 152 days, 18:49:57.45
    SNMPv2-MIB::sysContact.0 = STRING: Moa  <jean-marc.pouchoulon@iutbeziers.fr>
    SNMPv2-MIB::sysName.0 = STRING: registry
    SNMPv2-MIB::sysLocation.0 = STRING: iutbeziers

    # Pour  le switch :
    [slaynpool@MiniZbeub]~$ snmpwalk  -v  2c -c publicbeziers 10.255.255.253
    SNMPv2-MIB::sysDescr.0 = STRING: HP Comware Platform Software, Software Version 5.20.99 Release 2220P09
    HP A5500-24G EI Switch with 2 Interface Slots
    Copyright (c) 2010-2013 Hewlett-Packard Development Company, L.P.
    SNMPv2-MIB::sysObjectID.0 = OID: SNMPv2-SMI::enterprises.25506.11.1.24


    # Pour L'ad (Oui c'est la mauvaise communate )

    [slaynpool@MiniZbeub]~$ snmpwalk  -v  2c -c public 10.6.0.1
    SNMPv2-MIB::sysDescr.0 = STRING: Hardware: x86 Family 15 Model 4 Stepping 3 AT/AT COMPATIBLE - Software: Windows Version 5.2 (Build 3790 Multiprocessor Free)
    SNMPv2-MIB::sysObjectID.0 = OID: SNMPv2-SMI::enterprises.311.1.1.3.1.3
    DISMAN-EVENT-MIB::sysUpTimeInstance = Timeticks: (2020700073) 233 days, 21:03:20.73
    SNMPv2-MIB::sysContact.0 = STRING: M. Duban
    SNMPv2-MIB::sysName.0 = STRING: SERVER-RT
    SNMPv2-MIB::sysLocation.0 = STRING: Salle des serveurs
    SNMPv2-MIB::sysServices.0 = INTEGER: 78
    IF-MIB::ifNumber.0 = INTEGER: 3
    ```

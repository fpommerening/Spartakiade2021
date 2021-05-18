# Beispiel für Kubernetes Probes

Die Demo-Anwendung wurde mit .NET Core 3.1 erstellt. Die Probe-Endpunkte bzw. Pfade werden auf den normalen HTTP-Endpunkt gelegt. Sie können deshalb auch extern abgefragt werden.

Über den Pfad /order/ können die Aufträge angezeigt werden. Mit HTTP-PUT auf /order/ und einer JSON-Struktur wird ein neuer Auftrag erzeugt. Ist bereits ein Auftrag aktiv kommt eine Fehlermeldung. Die Abarbeitungszeit ist mit 2 Miunten fest codiert.

```
{
    "Product" : "Kaffee schwarz"
}
```

## Liveness - Probe
Die Liveness - Probe nutzt den Pfad /probe/alive. Im Normalfall wird http 200 zurückgegeben.
Mit einem HTTP-PUT auf den Pfad /probe/alive/{state} kann der Status geändert werden.
Dabei entspricht State = true dem Status HTTP 200 und State = false dem Status HTTP 500.
Wurde die Liveness - Probe aktiviert, beendet Kubernetes nach etwa 45 Sekunden die Pod und startet neu.

## Readiness-Probe
Die Readiness - Probe verwendet den Pfad /probe/ready. Sobald ein Auftrag erstellt wird, liefert die Anwednung HTTP 503. 
Ist die Readiness - Probe aktiv, kann nur kurze Zeit (ca. 5 Sekunden) per Service zugeriffen werden. Erst nach Abschluss wird wieder Datenverkehr an den Pod geleitet.

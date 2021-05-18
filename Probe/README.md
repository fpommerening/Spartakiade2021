# Beispiel für Kubernetes Probes

Die Demo-Anwendung wurde mit .NET Core 3.1 erstellt. Die Probe-Endpunkte bzw. Pfade werden auf den normalen HTTP-Endpunkt gelegt. Sie können deshalb auch extern abgefragt werden.

## Liveness - Probe
Die Liveness - Probe nutzt den Pfad /probe/alive. Im Normalfall wird http 200 zurückgegeben.
Mit einem HTTP-PUT auf den Pfad /probe/alive/{state} kann der Status geändert werden.
Dabei entspricht State = true dem Status HTTP 200 und State = false dem Status HTTP 503.
Wurde die Liveness - Probe aktiviert, beendet Kubernetes nach etwa 45 Sekunden die Pod und startet neu.

## Readiness-Probe

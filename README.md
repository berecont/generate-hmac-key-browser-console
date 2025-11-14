# generate-hmac-key-browser-console
## Anleitung um einen HMAC-Schlüssel in der Browser-Konsole zu erstellen  

In den meisten modernen Webbrowsern kann über die Entwicklertools (developer tools) ein HMAC-Schlüssel generiert werden. Die Entwicklertools bieten eine Konsole, in der JavaScript-Code ausgeführt werden kann.  
Man kann den `crypto` Web API nutzen, um einen sicheren, zufälligen Schlüssel zu generieren.  

### Schritte zur Generierung eines HMAC-Schlüssels in der Browser-Konsole:  
- **Entwickertool öffnen**  
Dies kann über das Menü genöffnet werden, oder mit Rechtsklick und `Untersuchen` auswählen oder durch Drücken von `F12` bzw. `Ctrl`+`Shift`+`I` (Windows) bzw. `Cmd`+`Opt`+`I` (Mac)
- **Konsole** in den Enticklertools öffnen
- **JavaScript-Code** einfügen und aussführen

```Javascript
// Generiert einen 256-bit (32 Byte) langen Schlüssel und gibt ihn als hexadezimalen String aus
window.crypto.subtle.generateKey(
    {name: "HMAC", hash: {name: "SHA-256"}},
    true,
    ["sign", "verify"]
).then(key => {
    window.crypto.subtle.exportKey("raw", key).then(exportedKey => {
        const keyHex = Array.from(new Uint8Array(exportedKey))
            .map(b => b.toString(16).padStart(2, '0'))
            .join('');
        console.log(`HMAC Key: ${keyHex}`);
    });
});
```

Dieser Code verwendet die Web Cryptography API (`window.crypto.subtle`), um einen kryptographisch sicheren, zufälligen Schlüssel für HMAC mit SHA-256 als Hash-Funktion zu generieren. Anschliessend wird der Schlüssel in ein exportierbares Format konvertiert (als "raw" Schlüssel), in ein Byte-Array umgewandelt und schliesslich als hexadezimaler String ausgegeben.  

Die Verfügbarkeit und Funktionalität kann je nach Browser und dessen Version variieren.

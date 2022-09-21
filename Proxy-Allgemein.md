Proxy Server:

-> Wird zwischen den Client und das Ziel-Server geschaltet

-> Client sendet Anfrage, kommt diese zunächst beim Proxy-Server an. Das Proxy server sendet die Anfragen dann mit seiner eigenen IP-Adresse weiter. Die Antwort auf Client's Anfragen vom Ziel-Server werden an den Proxy-Server zurückgeschickt und dann zu dem Client weitergeleitet.

Aufgaben:
1. Identität verbergen/verschleiern. Anfragen werden nicht mit Cliet's IPs an das Ziel-Server gesendet, sondern die vom Proxy-Server.
2. Cache speichern (webseite, die oft benötigt werden, können auf dem Proxy-Server gespeichert werden)
3. Das Ziel-Server vorgaukeln, also glauchen machen, dass die Anfragen nicht aus Deutschland kämen, falls der Proxy-Server im Ausland ist. 
4. Filtern für den Datenverkehr, um bestimmte Webinhalte für Clients zu blockieren.

-> Forward-Proxy(Schutz des Clients), um die Client's IP zu verbergen
Forward-Proxys senden ausgehende Anfragen anstelle des Benutzers oder Netzwerks. Der Forward-Proxy empfängt dann die Antworten auf diese Anfragen und leitet sie an den Proxy-Benutzer zurück. Forward-Proxys können so konfiguriert werden, dass sie den Internet-Verkehr auswerten oder überprüfen und die Anfragen anhand bestimmter Kriterien verarbeiten. Zum Beispiel können einige ausgehende Anfragen blockiert werden.

-> Reverse-Proxy(Schutz des Servers), um die Ziel-Server IP zu verbergen
Reverse-Proxys nehmen Client-Anfragen im Namen eines Servers oder einer Gruppe von Servern entgegen und leiten diese Anfragen dann bei Bedarf an die Server weiter. Dadurch wird verhindert, dass jemand direkt mit den Servern kommuniziert, und gleichzeitig wird die Leistung durch Lastausgleich verbessert, bei dem der eingehende Datenverkehr auf mehrere Server statt nur auf einen verteilt wird.

Arten der Proxy-Server:

1. Application-Level-Proxy: hat eine Funktion, um Datenpackete zu analysieren und je nach vorkonfigurierten Regeln zu blockieren, zu ändern und weiterzuleiten.

2. Circuit-Level-Proxy: kann keine Datenpackete analysieren. wird als Firewall-Filtermodul eingesetzt und filtert Datenpackete über Ports und IP-Adresse. Packete werden entwider durchgelassen oder blockiert

Dedizierter Proxy (nur für ein Kommunikationsprotokoll zuständig) vs. Generischer Proxy (für mehrere/alle Kommunikationsprotokolle zuständig)


Bei einer Public-Key-Infrastruktur erstellt man nicht nur einen Schlüssel, sondern stattdessen zwei: einen öffentlichen und einen privaten. Der öffentliche Schlüssel für die Verschlüsselung und der private für die Entschlüsselung. 

Der Browser erhält dann den öffentlichen Schlüssel über das Zertifikat und zum Verschlüsseln verwenden.

Zur Codierung der Informationen gibt es unterschiedliche Verfahren. Alle notwendige Informationen erhält der Brower über das Zertifikat. Bsp. AES mit SHA256


-> TLS ist auf SSL basiert und aufgrund der mehrere Schwachstellen in SSLv3, würde der TLS mit SSL ersetzt.

-> Der TLS verschlüsselt nachrichten und signiert sie auch (um veränderungen zu entdecken)

ASymmetrisch ist sicherer aber langsamer (2 Schlüsseln)

Symmetrisch ist schneller aber nicht sicherer (1 Schlüssel)





SSL/TLS Handshake:
https://www.youtube.com/watch?v=iQsKdtjwtYI
https://www.youtube.com/watch?v=q1OF_0ICt9A
https://www.youtube.com/watch?v=qXLD2UHq2vk
https://www.youtube.com/watch?v=cuR05y_2Gxc

How SSL works:
1. client connect to server
2. client ask the webserver to identify itself
3. webserver send a copy of its SSL certificate with the public key in the response
4. client check if the signature of the SSL certificate is trusted. to do this, browser will check his trusted store locally.
5. webserver then send a digitally signed acknowledgment using the public key to start an SSL encrypted session
6. Encrypted communication will be started


User (Private key, public key, user identification) 

-> user will request to CA

CA (Verify user identification, Build certificate for user)

Certificate for user (Public key, CA identification, User identification) this will be sent to the user.



Types of SSL certificate:
1. Extended Validation certificates (EV SSL)
2. Organization Validated certificates (OV SSL)
3. Domain Validated certificates (DV SSL)
-> less expensive and quick to obtain. It used for non-collection-/payments websites. It has lower assurance and minimal encryption
4. Wildcard SSL certificates -> secure many subdomains
5. Multi-Domain SSL certificates (MDC) -> secure many domains and subdomains.
6. Unified Communications Certificates (UCC) -> like UCC, but it initially designed to secure Microsoft Exchange and Live Communications servers.


### DER vs. CRT vs. CER vs. PEM ###

encodings:
-> .DER = The DER extension is used for binary DER encoded certificates. It called a "DER encoded certificate"

-> .PEM = The PEM extension is used for different types of X.509v3 files which contain ASCII (Base64)

both are synonymous

extensions:
-> .CRT = The CRT extension is used for certificates. encoded as binary (.DER) or as base64 (.PEM). 

-> .CER = alternate form of .crt (Microsoft Convention) for Microsoft application  You can use MS to convert .crt to .cer 

-> .KEY = The KEY extension is used both for public and private PKCS#8 keys. The keys may be encoded as binary DER or as ASCII PEM.

Common OpenSSL Certificate Manipulations:
There are four basic types of certificate manipulations. View, Transform, Combination , and Extraction.

1. Viewing
-> .PEM encoded certificates are ASCII they are not human readable.  to show the certificate in human readable form:

openssl x509 -in cert.pem -text -noout

openssl x509 -in cert.cer -text -noout

openssl x509 -in cert.crt -text -noout

You may not be able to view it, you will get some errors.

-> To view .DER encoded certificates

openssl x509 -in certificate.der -inform der -text -noout

2. Transform
-> PEM to DER
openssl x509 -in cert.crt -outform der -out cert.der

-> DER to PEM
openssl x509 -in cert.crt -inform der -outform pem -out cert.pem



### PAC Files ###

NOTE: The "isInNet", "isResolvable", and "dnsResolve" functions query a DNS server


Examples:


1. The "isPlainHostName(host)" function checks, if there are any dots in the hostname. If so, it returns false; otherwise, the function returns true.

2. The "localHostOrDomainIs(host, anydomainToCompare)" function is executed only for URLs in the local domain.

3. The "dnsDomainIs" function returns true if the domain of the hostname matches the domain given.

4. The "isInNet(host, pattern, mask)" function compares a given IP address pattern and mask with the hostname. The mask indicates which part of the IP address to match (255=match, 0=ignore). It is useful if certain hosts in a subnet should be connected directly and others should be connected using a proxy. 

5. The "shExpMatch(str, shexp)" function returns true if str matches the shexp using shell expression patterns

6. parameter.substring(start, end)

7. The "myIpAddress()" function returns the IP address (in integer-dot format) of the host that the browser is running on.

8. The "dnsDomainLevels()" function returns an integer equal to the number of dots in the hostname






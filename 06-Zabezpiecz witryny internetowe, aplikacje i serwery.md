# Sheet n°6: Zabezpiecz strony internetowe, aplikacje oraz serwery 

#### Zasady bezpieczeństwa "zgodne ze sztuką" należy zastosować do wszystkich stron internetowych, webaplikacji oraz serwerów, nie tylko na poziomie komunikacji sieciowej, ale też w odniesieniu do uwierzytelnienia czy komponentów infrastuktury.

## Bezpieczeństwo komunikacji

* **Zastosuj TLS w wersji 1.2 or 1.3** ("zamiennik" SSL-a) w przypadku wszystkich stron internetowych i w przypadku wymiany danych z aplikacjami mobilnymi. Można skorzystać z darmowych certyfikatów [LetsEncrypt](https://letsencrypt.org/). Należy pamiętać, aby sprawdzić, czy zostały prawidłowo zainstalowane. 

* **TLS obowiązkowe** w każdym przypadku i w całości dla aplikacji i witryn. 

* **Ogranicz porty** jedynie do tego, co potrzebne do funkcjonowania aplikacji. If access to a web server is only possible using the HTTPS protocol, only ports 443 and 80 of this server must be accessible, all other ports can be blocked by the firewall.

* **The OWASP has published on its website some cheatsheets** for exemple to [correctly implement TLS](https://cheatsheetseries.owasp.org/cheatsheets/Transport_Layer_Protection_Cheat_Sheet.html) or to [secure a webservice](https://cheatsheetseries.owasp.org/cheatsheets/Web_Service_Security_Cheat_Sheet.html).

## Securing Authentications

* **Follow [the CNIL recommendation on passwords](https://www.cnil.fr/fr/node/23803)**. In particular, remember to limit the number of access attempts.

* **Never store passwords in clear text**. Store them as a hash using a proven library, such as [bcrypt](https://en.wikipedia.org/wiki/Bcrypt).

* **If cookies are used for authentication**, it is recommended:

    * to force the use of HTTPS via [HSTS](https://en.wikipedia.org/wiki/HTTP_Strict_Transport_Security);

    * to use the `secure` flag;

    * use the `HttpOnly` flag.

* **Test the cryptographic suites installed on the systems** and disable obsolete ones (RC4, MD4, MD5 etc.). Encourage the use of AES256. [Read the OSWAP note on the subject](https://cheatsheetseries.owasp.org/cheatsheets/Cryptographic_Storage_Cheat_Sheet.html).

* **Adopt a specific password policy for administrators**. Change the passwords, at least, each time an administrator leaves and in case of suspected breach. Encourage strong authentication when possible.

* **Limit access to administration tools and interfaces to qualified staff.** Encourage the use of lower-privilege accounts for day-to-day operations.

* **Remote access to administration interfaces should be subject to increased security measures.** For example, for internal servers, implementing a VPN with strong authentication of the user and the workstation he or she is using may be a good solution.

## Securing infrastructures

* **Make backups, if possible encrypted and checked regularly**. This is especially useful in case of a ransomware attack on your systems as having backups for all your systems will be the only measure that will allow you to restore your systems.

* **Limit the size of the software stack used,** and for each element of the stack:

    * **Install critical updates** without delay by scheduling an automatic weekly check;
    * **Automate a vulnerability watch** by subscribing to the [NVD Data Feeds](https://nvd.nist.gov/vuln/data-feeds) for example.

* **Use vulnerability detection tools** for the most critical processes to detect possible security breach. Systems for detecting and preventing attacks on critical systems or servers can also be used. These tests must be conducted regularly and before any new software version is put into production.

* **Restrict or fordbid physical and software access to diagnostic and remote configuration ports.** For example, you can list all open ports using the *netstat* tool.

* **Protect the databases you make available on the Internet**, at least by restricting access as much as possible (for example, by IP filtering) and by changing the default password for the administrator account.

* In terms of database management, good practices include:

    * **using nominative accounts** for database access and create specific accounts for each application;
    * **revoking the administrative privileges** of user or application accounts to avoid modification to database structure (table, vues, process, etc);
    * having protection against SQL or script injection attacks;
    * encouraging at rest disk and database encryption.

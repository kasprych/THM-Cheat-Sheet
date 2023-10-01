# THM-Cheat-Sheet-
Zbiór zasobów i przydatnych polecen:

1. [Bash](#bash)
   1. [Pozostaw Bash bez historii](#bash-no-history)
   1. [Ukryj swoje polecenia](#bash-hide-command)

<a id="bash"></a>
# BASH


<a id="bash-no-history"></a>
## 1. Pozostaw Bash bez historii
Zmiana ustawiń powłoki Bash, aby używał */dev/null* zamiast *~/.bash_history*. Jest to pierwsze polecenie, które wykonujemy w każdej powłoce. Zatrzyma ono rejestrowanie poleceń przez Bash.
(Czyścimy również zmienne SSH_* na wypadek, gdybyśmy zalogowali się przez SSH. W przeciwnym razie każdy uruchomiony przez nas proces otrzyma kopię naszego IP w /proc/self/environ).
```sh
export HISTFILE=/dev/null
unset SSH_CONNECTION SSH_CLIENT
```
Dobrą praktyką jest "zabice wszystkich procesów" podczas wychodzenia z powłoki:
```sh
alias exit='kill -9 $$'
```
Każde polecenie zaczynające się od " " (spacja) [nie zostanie zapisane w historii].
```
$  id
```
<a id="bash-hide-command"></a>
## 2 Ukryj swoje polecenia
Ukryj jako "syslogd".

```shell
(exec -a syslogd nmap -T0 10.0.2.1/24) # Zwróć uwagę na nawiasy '(' and ')'
```

Uruchomienie ukrytego procesu w tle:
```
(exec -a syslogd nmap -T0 10.0.2.1/24 &>nmap.log &)
```

Start within a [GNU screen](https://linux.die.net/man/1/screen):
```
screen -dmS MyName nmap -T0 10.0.2.1/24
### Dołącz z powrotem do procesu nmap
screen -x MyName
```

Alternatywnie, jeśli nie ma Bash:
```sh
cp `which nmap` syslogd
PATH=.:$PATH syslogd -T0 10.0.2.1/24
```
W tym przykładzie wykonujemy *nmap*, ale pozwalamy mu pojawić się z nazwą *syslogd* na liście procesów *ps alxwww*.

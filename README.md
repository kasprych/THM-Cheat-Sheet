# THM-Cheat-Sheet-
Zbiór zasobów i przydatnych polecen:

1. [Bash](#bash)
   1. [Pozostaw Bash bez historii](#bash-no-history)
   1. [Ukryj swoje polecenia](#bash-hide-command)
1. [SSH](#ssh)
1. [Przydatne serwisy](#serwisy)

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

<a id="ssh"></a>
# SSH

Przeszukania wszystkich katalogów domowych pod obecność katalogu o nazwie .ssh
```
for dir in $(awk -F: '{print $6}' /etc/passwd);do if [ -d $dir ];then find $dir -maxdepth 1 -type d -name .ssh;fi;done
```
<a id="serwisy"></a>
# PRZYDATNE SERWISY
1. **THC's favourite Tips, Tricks & Hacks (Cheat Sheet)** [https://tinyurl.com/thctips](https://tinyurl.com/thctips)
1. **Hack Tricks** [https://book.hacktricks.xyz](https://book.hacktricks.xyz) - wiki, gdzie znajdziesz wszystkie hakerskie sztuczki/techniki/whatever
1. **GTFOBins** [https://gtfobins.github.io](https://gtfobins.github.io) - GTFOBins to wyselekcjonowana lista uniksowych plików binarnych, których można użyć do ominięcia lokalnych ograniczeń bezpieczeństwa w źle skonfigurowanych systemach.
1. **LOLBas** [https://lolbas-project.github.io](https://lolbas-project.github.io) - Celem projektu LOLBAS jest udokumentowanie każdego pliku binarnego, skryptu i biblioteki, które można wykorzystać w technikach Living Off The Land. 
1. **Generator reverse shell** [https://www.revshells.com](https://www.revshells.com)
1. **Bash scripting cheatsheet** [https://devhints.io/bash](https://devhints.io/bash)
